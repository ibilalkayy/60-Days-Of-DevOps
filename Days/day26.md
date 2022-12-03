On the twenty-sixth day, I learned the following things about Kubernetes.

## **Kubernetes Networking**

Kubernetes networking addresses four concerns.

- Containers within a pod use networking to communicate via loopback.

- Cluster networking provides communication b/w different pods.

- The container in a pod of node1 will not talk to the container in a pod of node2. Both the containers should be in the same pod to talk to each other.

- The service lets you expose an application running in pods to be reachable from outside cluster/browser or internet.

- You can also use service to publish services only for consumption inside your cluster.

### **Container to container communication**

- Container to container communication on the same pod happens through localhost within the containers.

                                              Localhost
                                                  | 
                        --------------------------|---------------------------
                        |   ----------------------|-----------------------   |-------> Node    
                        |   |   -------------     |     -------------    |---|-------> Pod    
                        |   |   |    C00    | <-------> |    C01    |----|---|-------> Container  
                        |   |   -------------           -------------    |   |                     
                        |   ----------------------------------------------   |
                        ------------------------------------------------------


- One pod containers will not be present in different nodes. Instead they will be in the same node.

      kind: Pod
      apiVersion: v1
      metadata:
        name: testipod
      spec:
        containers:
          - name: c00
            image: ubuntu
            command: ["/bin/bash", "-c", "while true; do echo Hello-Bilal; sleep 5; done"]
          - name: c01
            image: httpd
            ports:
              - containerPort: 80

- After creating the pod, type `kubectl exec pod-name -it -c container-name -- /bin/bash`. It will take you inside the container that is present in a pod.

- `apt update && apt install curl` will update and install the curl package inside your container.

- `curl localhost:80` will show you a message that it works. It will show you that two containers are communicating successfully.

### **Pod to pod communication**

- Pod to pod communication on the same worker node happens through ip address. 
    - If you provided a pod A ip address, you'll communicate with pod A and vice versa.
    - If container A wants to access container B in another pod, then to go inside the container A, give an ip address and it will redirect you to container B. 

- By default, pod's ip address will not be accessible outside the node.


                                IP address                    IP address
                                    |                             |  
                        ------------|-----------------------------|------------
                        |   --------|----------         ----------|--------   |-------> Node    
                        |   |  -------------  |         |  -------------  |---|-------> Pod    
                        |   |  |    C00    |  | <-----> |  |    C01    |--|---|-------> Container  
                        |   |  -------------  |         |  -------------  |   |                     
                        |   -------------------         -------------------   |
                        -------------------------------------------------------
**First file**

    kind: Pod
    apiVersion: v1
    metadata:
      name: testpod1
    spec:
      containers:
        - name: c01
          image: nginx
          ports:
            - containerPort: 80

**Second file**

    kind: Pod
    apiVersion: v1
    metadata:
      name: testpod2
    spec:
      containers:
        - name: c02
          image: httpd
          ports:
            - containerPort: 80

- After making pods, type `kubectl get pods -o wide` to take the ip address.

- `kubectl exec pod-name -it -c container-name -- /bin/bash` will take you inside the container that is present isn a pod.

- `apt update && apt install curl` will update and install curl incase if it is not installed in the pod terminal.

- `curl ip-address:80` will give you the details of that ip address. Type this command inside the pod terminal.

### **Node to node communication**

**Service object**

- When using RC, pods are terminated and created during scaling or replication operations.

- When using deployments while updating the image version, the pods are terminated and new pods take the place of other pods.

- Pods are dynamic. i.e. They come and go on the k8s cluster and on any of the available nodes and it would be difficult to access the pods as the pods IP changes once it is recreated.

  - **Problem**

    Each pod gets its own ip address, however in a deployment the set of pods running could be different in one moment from the set of pods running in another moment. This leads to a problem that if a pod & it's ip address is not permanent to its place and is changing everytime, how would another pod keep track of the ip address of the target pod?

  - **Solution**

    - The solution is the service object that is a logical bridge b/w pods and the end users which provides virtual ip address(VIP) and with the help of VIP, the communication will happen even if the pod's ip addresses are changing.
    - Each object will have its own virtual ip address.
    - Service allows clients to reliably connect to the containers running in the pod using the VIP.
    - The VIP is not an actual IP address connected to the network interface but the purpose is to forward traffic to one or more pods.
    - Kube proxy will keep the mapping b/w the VIP and pod's ip address. If a pod new ip address is created, then kube proxy will map it with the VIP to build the connection.

  - **Problem**

    Although each pod has a unique ip address, these ip addresses are not exposed outside the cluster. They can only communicate inside the cluster.

  - **Solution**

    - Services help to expose the VIP(that is mapped to the pods) and allow application to receive traffic outside the cluster (browser etc).
    - You have to define labels on both pod side and services side that will select the specific pods(from thousands of pods) to put under a service.
    - Creating a service will create an endpoint that will access the pods/application in it.
    - Services can be exposed in four different ways by specifying a type in the service specification.
      1. Cluster IP
      2. NodePort
      3. LoadBalancer
      4. Headless
    - By default, service can only run b/w ports 30,000 - 32,767.
    - The set of pods targeted by a service is usually determined by a selector.
    - NodePort is an upper layer of the cluster ip and Load balancer is the upper layer of the nodeport and headless is top part.

**1. Cluster IP**

                                    Cluster IP: ip-address:port-number 
                      ---------------------------------------------------------------
                      |   --------------------               --------------------   |----> Cluster
                      |   |   ------------   |               |   ------------   |---|----> Node    
                      |   |   |          |---|---------------|-->|          |---|---|----> Pod    
                      |   |   |   Pod1   |   |               |   |   Pod2   |   |   |  
                      |   |   |          |<--|---------------|---|          |   |   |                  
                      |   |   ------------   |               |   ------------   |   |
                      |   --------------------               --------------------   |
                      ---------------------------------------------------------------

- The nodes will be mapped with a VIP(it is fixed) so that the pod A from the node A can communicate with the pod B of the node B without needing to identify the specific ip addresses of each pods.
- Cluster IP exposes VIP to be reachable only from within the cluster. VIP can't be accessed outside the cluster.

**deployment.yml**

    kind: Deployment
    apiVersion: apps/v1
    metadata:
      name: mydeployments
    spec:
      replicas: 1
      selector:
        matchLabels:
          name: deployment
      template:
        metadata:
          name: testpod2
          labels:
            name: deployment
        spec:
          containers:
            - name: c00
              image: httpd
              ports:
                - containerPort: 80

- After creating a pod, write `kubectl get pods -o wide` to see the ip address of the pod.

- `kubectl exec pod-name -it -c container-name -- /bin/bash` will take you inside the container that is present in a pod.

- `apt update && apt install curl` will update and install curl incase if it is not installed in the pod terminal.

- `curl ip-address:80` will give you the details of that ip address. Type this command inside the pod terminal.

**service.yml**

    kind: Service			    --> Defines to create service type object
    apiVersion: v1
    metadata:
      name: demoservice
    spec:
      ports:
        - port: 80			    --> Containers port exposed
          targetPort: 80		--> Pods port
      selector:
        name: deployment	    --> Apply this service to any pods which has the specific label
      type: ClusterIP		    --> Specifies the service type i.e. ClusterIP or NodePort

- `kubectl apply -f file-name.yml` will apply the changes.

- After creating a pod, type `kubectl run any-pod-name --image=curlimages/curl -i --tty -- sh`. It will fetch the curl image from the DockerHub. 

- `kubectl exec -i --tty pod-name -- sh` will execute and take you inside the curl terminal if you exit from it.

- Take the cluster ip and type `curl ip-address:port` in the curl terminal to show you the success message.

- `kubectl get services` OR `kubectl get service` OR `kubectl get svc` will give the list of services and the Cluster IP that is basically a virtual ip address.

- `kubectl describe services service-name` will show you the details of the service.

**2. NodePort**

                                              ------------
                  |-------------------------> | Internet |
                  |                           ------------
                  |
                  |                   Cluster IP: ip-address:port-number 
           httpd  |   ---------------------------------------------------------------
                  |   |   --------------------               --------------------   |----> Cluster
                  |   |   |   ------------   |               |   ------------   |---|----> Node    
                  |   |   |   |          |   | ------------> |   |          |---|---|----> Pod    
                  ----|---|   |   Pod1   |   |               |   |   Pod2   |   |   |  
                      |   |   |          |   | <------------ |   |          |   |   |                  
                      |   |   ------------   |               |   ------------   |   |
                      |   --------------------               --------------------   |
                      ---------------------------------------------------------------

- Nodeport access a service from outside the cluster via internet.

- Attach a port number that is assigned to you with public DNS and that port number is attached to the virtual ip address and the VIP will contact the pod inside a node. As a result, the container inside pod will be shown to us via internet.

- First take the deployment.yml file from above and apply it in the kubectl. Then apply the service.yml file below.

**service.yml**

    kind: Service			    --> Defines to create service type object
    apiVersion: v1
    metadata:
      name: demoservice
    spec:
      ports:
        - port: 80			    --> Containers port exposed
          targetPort: 80		--> Pods port
      selector:
        name: deployment		--> Apply this service to any pods which has the specific label
      type: NodePort		    --> Specifies the service type i.e. ClusterIP or NodePort

- Make a deployment file and inside it, write the data that is written above in the deployment.yml file.

- NodePort will make the pod accessible to the internet or outside the cluster.

- After making a pod of this file, type `kubectl get svc`, you'll be provided a port number like this `80:<this-port-number>/TCP`.

- `kubectl describe svc demoservice` will show you the details of the service.

- Browser will access the VIP that is attached to the port number. VIP will will access a pod and an application inside it.

- `minikube ip` will give the ip address that will be used in the browser to work on.

- After getting the minikube ip address and the port number from `kubectl get svc`, write `http://<minikube-ip>:<this-port-number>` in the browser. It will give you the success message.

- If you're using a cloud platform, you can take the DNS link and attach it with port-number to make it work.

## **Volumes**

- Containers are short lived in nature.

- All the data stored inside a container is deleted if the container crashes. However the kubelet will restart it with a clean state, which means that it will not have any of the old data.

- To overcome this problem, volume comes into picture and kubernetes uses it.  A Volume in Kubernetes represents a directory with data that is accessible across multiple containers in a Pod.

- In kubernetes, a volume is attached to a pod and shared among the containers of that pod.

- The volume has the same life span as the pod and it will not be affected if the containers crashed. If new containers are created, then they will take the data from the volume that is already present.

- If the pod is crashed then the volume will also be crashed.

                                                    Pod
                                      --------------------------------
                                      |          ---------           |
                                      |          |  Vol  |           |
                                      |          ---------           |
                                      |          /       \           |
                                      |    ---------    ---------    |
                                      |    |  C00  |    |  C01  |    |
                                      |    ---------    ---------    |
                                      -------------------------------- 

### **Volume Types**

- A volume decides the properties of the directory/pod like size, content etc. Some of the volume types in which you can store the data are.

- None-local such as EmptyDir or host path.

- File sharing type such as NFS.

- Cloud provider such as AWSElasticBlockStore, AzureDisk etc.

- Distributed filesystem types, e.g. glusterfs or cephfs.

- Special purpose types like secret, gitrepo.

- **EmptyDir**

  - When a pod is newly created and assigned to a node then an emptydir volume is also created and exist as long as that pod is running on that node.

  - Use emptydir if we want to share content b/w multiple containers on the same pod and not to the host machine.

  - As the name says, it is initially empty.

  - After the containers are created, they will be mounted/attached with same volume.

  - When a pod from a node is deleted, the data in the emptydir will be deleted forever.

  - A container crashing does not remove a pod from a node. The data in an emptydir volume will be safe if the container crashes.

        kind: Pod
        apiVersion: v1
        metadata:
          name: myvolemptydir
        spec:
          containers:
            - name: c1
              image: centos
              command: ["/bin/bash", "-c", "sleep 15000"]
              volumeMounts:				---> Mount definitions inside the containers
                - name: xchange
                  mountPath: "/tmp/xchange"
            - name: c2
              image: centos
              command: ["/bin/bash", "-c", "sleep 10000"]
              volumeMounts:
                - name: xchange
                  mountPath: "/tmp/data"
          volumes:
            - name: xchange
              emptyDir: {}

  - After creating a pod, type `kubectl exec pod-name -it -c c1 -- /bin/bash`. It will take you inside the pod container 1 terminal.

  - `cd tmp/xchange` will take you inside the xchange directory. Create any kind of file and write something in it.

  - Type `kubectl exec pod-name -it -c c2 -- /bin/bash`. It will take you inside the pod container 2 terminal.

  - `cd tmp/data` will take you inside the data directory. If you type `ls`, it will show you the same file that was created in the first container.

  - If you modified it, it will show you the changes in another container also.

## **Explaining it in a video**

Here you can get an explanation in a video. [26/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=7X4XznzdLb4&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=24)