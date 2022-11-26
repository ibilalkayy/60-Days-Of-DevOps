On the twenty-seventh day, I learned the following things about Kubernetes.

# **Jobs, Init containers and Pod lifecycle**

## **Jobs**

- Jobs is another object but it's purpose is different from pod.

- We have replicasets,, daemonsets, and deployments etc. They all share one common property. They always make sure that the pod is running. The controller restarts or reschedules the pod to make sure the application in a pod always keeps running.

- There is another object that is called Jobs. It is not bound to be running every time. Instead, if the task is completed, the jobs will stop. The pod can be recreted again if required but the jobs will stop if the work is finished.

- You can schedule it and it will be created and deleted multiple times.

- `sleep 5` will stop the container after 5 seconds. It will not delete the job.

      apiVersion: batch/v1
      kind: Job
      metadata:
        name: myjob
      spec:
        template:
          metadata:
            name: myjob
          spec:
            containers:
              - name: c01
                image: centos:7
                command: ["bin/bash", "-c", "echo Bilal Khan; sleep 5"]
            restartPolicy: Never

- `watch kubectl get pods` will give you the jobs with Ready 1/1 but after 5 seconds completion, it will show you the Ready 0/1 because the container is now deleted and it is not created again and the status is completed.

- Jobs will not get deleted by itself. You have to delete it by writing `kubectl delete -f file.yml`.

### **Parallelism**

- It will create multiple pods and run them parallely and delete them after some given time.

      apiVersion: batch/v1
      kind: Job
      metadata:
        name: testjob
      spec:
        parallelism: 5
        activeDeadlineSeconds: 10
        template:
          metadata:
            name: testjob
          spec:
            containers:
              - name: c01
                image: centos:7
                command: ["bin/bash", "-c", "echo Bilal Khan; sleep 30"]
            restartPolicy: Never

- `parallelism: 5` will run 5 pods parallely.

- `sleep 30` will terminate the containers after 30 seconds.

- `activeDeadlineSeconds: 10` will delete the pods after 40 seconds. The container will be deleted after 30 seconds and after 10 seconds of container deletion, the pods will also be deleted.

- After applying, if you type `watch kubectl get pods`, you will see that all the pods are deleted after 40 seconds.

### **CronJob**

    apiVersion: batch/v1
    kind: CronJob
    metadata:
      name: bilal
    spec:
      schedule: "* * * * *"
      jobTemplate:
        spec:
          template:
            spec:
              containers:
                - image: ubuntu
                  name: bilal
                  command: ["/bin/bash", "-c", "echo Bilal Khan; sleep 5"]
              restartPolicy: Never

- The `* * * * *` in the `schedule` shows the minutes. Each star represents one minute. It means that new pod will be created after every one minute and the container inside that pod will be terminated after every 5 seconds.

- After applying this file, type `watch kubectl get pods` and you will see that new pod is created after every one minute and from 0 to 5 seconds the Ready state will be equal to  1/1 but after 5 seconds, the Ready state will be equal to 0/1. It means that the container is deleted after 5 seconds.

## **Init Container**

- Init container is an initialized or the starting container that will run and is required before running the main container. Let's say that the main container is an application but Init container is the process to first install that application, log in and then run that application in the main container.

- You can specify the processes in init container before creating the main container. When the main container is created, the init container will be deleted.

- If the init container fails then kubernetes will repeatedly create it again until it is succeeded.

### **Use cases**

- Making a format of the database before inserting the values in it.

- Delaying the applications to launch until the dependencies are ready.

- Clone the git repository into the volume to get the necessary files.

      apiVersion: v1
      kind: Pod
      metadata:
        name: initcontainer
      spec:
        initContainers:
          - name: c1
            image: centos
            command: ["/bin/sh", "-c", "echo LIKE AND SUBSCRIBE BILAL KHAN > /tmp/xchange/testfile; sleep 30"]
            volumeMounts:
              - name: xchange
                mountPath: "/tmp/xchange"
        containers:
          - name: c2
            image: centos
            command: ["/bin/bash", "-c", "while true; do echo `cat /tmp/data/testfile`; sleep 5; done"]
            volumeMounts:
              - name: xchange
                mountPath: "/tmp/data"
        volumes:
          - name: xchange
            emptyDir: {}

- After applying this file, type `watch kubectl get pods`. It will show you `init:(0/1)`. It will show you that the container is first initializing. Then it will give you the Ready message `1/1` that the container is running.

- After that, type `kubectl logs -f pods/pod-name` to print the message after every 5 seconds.

- Type `kubectl describe pod/initcontainer`, you can get the condition of the pod that first this happened and then this happened and so on.

- Type `kubectl describe pod/initcontainer | grep -A 5 Conditions` will only show you the conditions.

## **Pod lifecycle**

There are different phases of a pod.

- Pending
- Running
- Succeeded
- Failed
- Unknown
- Completed

### **Pending**

- The pod has been accepted by k8s system but it is in the process and not running yet.

- One or more of the container images are still downloading.

- If the resources are not found then it will search them and give you the success or failure message.

### **Running**

- If the pod is successfully created in the node.

- All the containers have been created.

- Atleast one container is still running or is in the process of starting or restarting.

### **Succeeded**

- All the containers have successfully completed their required task and are going to be terminated and will not be restarted.

### **Failed**

- All the containers in the pod have been terminated and atleast one container has terminated.

- The container either exited with non-zero status or was terminated by the system.

### **Unknown**

- The master does not know the state of the pod.

- Typically due to an error in network or communicating with the host of the pod.

### **Completed**

- The pod has run and completed the task and there is no need to keep it running.

## **Pod conditions**

These are possible types.

- **PodScheduled** - The master has scheduled a pod to a node.

- **Ready** - The pod is created successfully and the container(s) is also running in it.

- **Initialized** - All init containers have started successfully.

- **Unscheduled** - The scheduler cannot schedule the pod right now due to the lack of resources.

- **ContainerReady** - All containers are ready in the pod.

## **Explaining it in a video**

Here you can get an explanation in a video. [27/60 Day of DevOps Challenge]()