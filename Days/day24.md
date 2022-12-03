On the twenty-forth day, I learned the following things about Kubernetes.

## **Labels and Selectors**

- Labels are attached to an object and it will identify it while the selector selects an object to fetch it with the help of commands.

- Labels are the mechanism you use to organize the kubernetes objects.

- A label is a key-value pair without any predefined meaning that can be attached to any object not just pod but node also.

- It is used for quick reference.

- You're free to choose labels as you need it to refer an environment which is used for development, testing, or production. Refer a product group like DevelopmentA, DevelopmentB, CompanyC, etc.

- Multiple labels can be added to a single object.

## **There are two methods for writing a label**

### 1. **Declarative method:** You can write a label inside your manifest file.

      kind: Pod
      apiVersion: v1
      metadata:
        name: testpod
        labels:
          env: developments
          class: pods
      spec:
        containers:
          - name: c00
            image: ubuntu
            command: ["/bin/bash", "-c", "while true; do echo Hello-Bilal; sleep 5; done"]


- After creating a pod, apply it in kubectl by writing `kubectl apply -f pod.yml`, and write `kubectl get pods --show-labels`. It will show you the labels of the pod.

### 2. **Imperative method:** If you want to add a label to an existing pod without updating the manifest file then type in the terminal `kubectl label pods pod-name label-key=label-value`. After that, run `kubectl get pods --show-labels` to show the labels.

- `kubectl get pods -l label-key=label-value` will give you the list of pods that are having the specified key and value.

- `kubectl get pods -l label-key!=label-value` will give you the list of pods that are not having the specified value.

- `kubectl delete pod -l label-key!=label-value` will delete the pods based on labels. It won't delete the pods that are the specified.

- Unlike name/UIDs, labels do not provide uniqueness, as in general we can expect many objects to carry the same label.

- Once labels are attached to an object, we would need filters to narrow down and these are called as label selectors.

- The API currently supports two types of selectors. Equality based selector and set based selector.

    **Example of equality based selector:** [=, !=]
    
    - ` kubectl get pods -l key-label=value-label` will find a pod according to the given key and value.
    - `kubectl get pods -l key-label!=value-label` will not find the pods according to the given key and value.

    **Example of set based selector:** [in, notin, exists]
    
    - `kubectl get pods -l 'key-label in (value-label1, value-label2, ...)'` will the find all the pods relevant to the specified keys and values. Even if a single value is found in a pod, it will fetch that pod and show you.
    - `kubectl get pods -l 'key-label notin (value-label1, value-label2, ...)'` will ignore all those pods that do not contain these values.
    
### **Node selector**

- Generally the schedular will do a reasonable placement to place a pod to any random node but you can specify the pod to run on a specific node based on a label.

- Once the node is labelled, you can use the label selector to specify the pods to run on a specific node.

- We can use labels to tag nodes.

- First give a label to the node. Then use a node selector to run a pod on a specific worker node.

      kind: Pod
      apiVersion: v1
      metadata:
        name: nodelabels
        labels:
          env: developments
      spec:
        containers:
          - name: c00
            image: ubuntu
            command: ["/bin/bash", "-c", "while true; do echo Hello-Bilal; sleep 5; done"]
        nodeSelector:
          hardware: t2-medium

- `kubectl describe pod nodelabels` will give you the information of a node.

- Check the kubectl nodes by typing `kubectl get nodes`

- `kubectl label nodes node-name node-key=node-value` will give a label to the node and the pod will be assigned to that node due to the label.

- `kubectl get pods` will show you the pods that are running.

## **Scaling and Replication**

- By default, kubernetes does not provide scaling and replication feature. But we do have the objects that give us this kind of functionality.

- The old pod won't restart after termination. Instead a new pod will be created with the same features of the previous pod.

- Kubernetes was designed to orchestrate multiple containers and replication.

- Need for multiple containers/replication helps us with

- **Reliability:** If one pod is failed then another will be automatically created to make the process reliable.

- **Load Balancing:** If one node is overloaded then the remaining pods will transferred to another node to balance the load.

- **Scaling:** If a movie is played and many users came then an application requires more containers to manage an application. In this case, kubernetes will automatically create the containers and if the movie came to an end and the users are gone then the kuberentes will delete those containers. It will also create the nodes/instances if required so that other pods are adjusted there.

### **Replication Controller**

- A replication controller is an object that enables you to create multiple pods, so that the pods always exist. If you set `replicas=2` and one pod is crashed then it will automatically create a new pod and maintain the state of the pod equal to 2.

- If a pod is created using RC, then it will automatically replace other pods if they crashed, failed, or terminated.

- It is not a default object of kubernetes. You have to manually write it yourself in your YAML file.

- RC should be minimum set to 1 or 2(so that a copy is always present) and you can extend the number of it also.

**Example**

    kind: ReplicationController ---> It creates an object of replication type.
    apiVersion: v1
    metadata:
      name: myreplica
    spec:
      replicas: 2 ---------> It defines the desired number of pods.
      selector: -----------> It selects and tells the controllers, which pods to watch/belong to this RC.
        myname: Bilal -----> It watches the labels.
      template: -----------> It defines a template to launch a new pod.
        metadata:
          name: testpod2
          labels: -----------> The above selector value needs to be matched with this label value.
            myname: Bilal
        spec:
          containers:
            - name: c00
              image: ubuntu
              command: ["/bin/bash", "-c", "while true; do echo Hello-Bilal; sleep 5; done"]

- `kubectl get rc` will give you the details of replication controller like name, desired, current etc.

- `kubectl describe rc replica-name` will show you the brief details of replica set.

- By writing `kubectl get pods`, you will get 2 pods because `replicas:2`. If you delete any of the pod by writing `kubectl delete pod pod-name`, another one will be automatically created.

- `kubectl scale --replicas=5 rc -l myname=label-name` will scale up/increase the size of replicas to 5.

- `kubectl scale --replicas=1 rc -l myname=label-name` will scale down/decrease the size of replicas to 1.

- You can't delete the replica pod, because it wlll automatically create a new pod. Instead you have to delete the file by typing `kubectl delete -f file-name.yml`.

### **Replica Set**

- Replica set is the advanced version of the replication controller.

- The replication controller only supports equality-based selector whereas the replica set supports both equality-based and set-based selectors i.e. filtering according to the set of values.

**Example**

    kind: ReplicaSet
    apiVersion: apps/v1
    metadata:
      name: myrs
    spec:
      replicas: 2
      selector:
        matchExpressions:   --> these must match the labels
          - {key: myname, operator: In, values: [Bilal, Khan]}
          - {key: env, operator: NotIn, values: [production]}
      template:
        metadata:
          name: testpod4
          labels:
            myname: Bilal
        spec:
          containers:
            - name: c00
              image: ubuntu
              command: ["/bin/bash", "-c", "while true; do echo Hello-Bilal; sleep 5; done"]

- `kubectl get rs` will give you the details of replica set like name, desired, current etc.

- After creating the pod, delete it and you will see another pod automatically created.

- `kubectl describe rs replicaset-name` will show you the brief details of replica set.

- `kubectl scale --replicas=2 rs/myrs` will scale up and down the replicas.

- `kubectl delete rs/myrs` will delete the replica set.

## **Explaining it in a video**

Here you can get an explanation in a video. [24/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=KgrE-ZauahY&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=22)