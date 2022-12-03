On the fifty ninth day, I learned the following things about Helm.

# Helm

<p align="center"> 
    <img src="../Images/helm.svg" alt="Helm" width="30%" height="30%">
</p>

- Before discussing helm, let's understand the common functionalities present in linux.

- Suppose you created a linux machine and then did the following things.

    **1. Package management:** It means to install the packages by using the commands like `apt`, `yum` etc.
    
    **2. Automated installation:** It means that it will install the packages automatically without the files moving manually.
    
    **3. Version management:** It means that it will update the packages.

    **4. Dependency management:** It means that it will install the dependencies that are required for a package to be installed.

    **5. Remove:** It means that you can remove the packages and all the dependencies will be removed with it.

## What is Helm?

- Helm is a package manager that deals with package management in kubernetes.

- It means to manage the manifest or YAML files, creating them and managing the packages inside that YAML file.

- Suppose you have 2-tier architecture in kubernetes. One is frontend and another one is backend.

- In the frontend you create a deployment. Inside that deployment, the replicas are present. Inside each pod the container will be present and each container will run an application. You also need configmap that will contain the configuration data inside the file. You also create a service YAML file that will tell in which pod the application will run.

                                                --------------------
                                                |   -------------  |
                                                |   |  Service  |  |
                                                |   -------------  |
                                                |   -------------  |
                                                |   | configmap |  |
                                                |   -------------  |
                                                |  --------------- |
                                                |  |  Deployment | |
                                                |  --------------- |
                                                --------------------


- In the backend, you need a stateful set that runs an application in the database. You also need another YAML file to store the confidential data. You also need a service YAML file that will tell accessibility b/w different pods outside the cluster and inside the cluster etc.

                                                --------------------
                                                |   -------------  |
                                                |   |  Service  |  |
                                                |   -------------  |
                                                |   -------------  |
                                                |   |   Secret  |  |
                                                |   -------------  |
                                                |   -------------  |
                                                |   |  Stateful |  |
                                                |   |    Set    |  |
                                                |   -------------  |
                                                --------------------

- First the backend will be executed and then the result will be shown to you on the frontend.

**Problem**

- If you have one or two files then it is easy to write `kubectl apply` with every file and send it to the kubernetes master.

- But if there are hundreds of files then applying every file is not an easy task.

**Solution**

- To solve this problem, helm comes into picture. It will take all the YAML files of an application and consider it as a package.

- Now there is no need to apply each of the file. Instead a package that contains the file will be executed with one command.

- Helm is a utility tool or the package maanger that will make the processes of kubernetes easy. Now instead of writing `apt` or `yum`, write `helm`.

## Difference b/w Helm and Helm chart

- Helm creates a package in which all the manifest files are present and that package is called Helm chart.

- Helm chart is a collection of manifest files that becomes a package.

- Now you can easily deploy the helm chart(package) into the kubernetes cluster.

## Brief Intro

- Helm is introduced first time in 2015.

- Helm 3 was released in Nov 2019.

- Helm helps you manage k8s applications with helm charts which helps you define, install, upgrade and remove even the most complex kubernetes application.

- `helm` is the equivalent of `yum` and `apt`.

- Helm is now an official k8s project and is a part of CNCF.

- The main building block of helm based deployments are Helm charts that describe a configurable set of dynamically generated k8s resources.

- The chart can either be stored locally or fetched from remote chart repositories.

- Just like github or dockerhub, helm has helmhub that will take and install a package from the helmhub repository.

## Why use Helm?

- Writing and maintaining kubernetes YAML manifest for all the required kubernetes objects can be a time consuming issue and tedious task.

- For the simple deployment, you would need atleast 3 YAML manifest file with duplicated and hardcoded values.

- Helm simplifies the process and create a single package that can be referred to your cluster.

- Helm k8s automatically maintains a database of all versions of your releases so when something goes wrong during the deployment, rolling back to the previous version is just one command away.

## Some keywords to understand Helm

- **Chart:** Helm charts are simply k8s yaml clusters manifests combined into a single package that can be advertised to your k8s cluster.

- **Release:** A chart can often be installed many times and each time it is installed, a new release is created. Those release will help you to go to the next and previous state of the kubernetes if you want to. Consider a MySQL chart, if you can install that chart twice, each one will have its own release which will in turn have its own release name.

- Helm keeps tracks or keep the record of all chart execution like install, upgrade, remove, rollback.

- **Repository:** Location where packaged can be stored and shared. It can local or remote repository.

## How Helm helped us in the CI/CD pipeline?

- Suppose we have Dev, QA, Pre-Production and Production. For each environment you have different number of replicasets, like Dev contains 2 replicaset, QA replicaset and so on.

- Now the question arises that do we need to write the number of replicasets everytime in each manifest file.

- To solve this problem, helm provides you a template which will contain the empty field in which you just need to put the values according to your replicaset.

- There will be another file in which you just need to write the numbers that will be allocated to the replicaset. In this way, you don't need to edit the YAML file everytime to change the number of replicaset.

- Instead you just need to mention the file name in the manifest file that contains the values. The key will be present in the manifest and the value will be present in another file that will be called in the manifest.

- Template engine will create the replicas that you mentioned in a file according to each of the environment.

**Example**

    apiVersion: apps/v1
    kind: Deployment
    metadata:
    name: release-name-springboot
    spec:
        replicas: {{Values.replicaCount}}
    selector:
        matchlabels:
        app kubernetes.io/name:Springboot

## Helm Architecture

- Helm is a single-service or a client architecture. It means that only client is required and the server is not required because kubernetes now contains RBAC(Role-based access control).

- Helm 2 had a client-server architecture but with RBAC in kubernetes, helm 3 has come and it only requires the client architecture.

- Client is responsible for implementing helm. There is no core processing logic distributed among components.

- Implementation of helm 3 is single command line that knows that how to manage the kubernetes cluster.

- Helm and its library both are written in Golang.

- In previous scenario, you had to write `kubectl apply` to install a package that is present in the manifest file.

- That package had to contact the api-server and then the package would be installed in all the nodes like this.

                                                --------------------
                                                |  --------------  |
                                                |  | API-SERVER |  |
                                                |  --------------  |
                                                |        ↓         |
                                                |   ------------   |
                                                |   |  Node 1  |   |
                                                |   ------------   |
                                                |   ------------   |
                                                |   |  Node 2  |   |
                                                |   ------------   |
                                                --------------------

- In the helm case, first you will write `helm install jenkins` and it will go to the helm-client. The helm-client will find that package in the helm registry or repository and give it to the helm-client.

- The helm-client will give that package to the API-Server and then it will be installed on each node like this.

                                                          --------------------
                            ----------------              |  --------------  |
                            |  Helm-client |  ----------> |  | API-SERVER |  |
                            ----------------              |  --------------  |
                                ↓      ↑                  |        ↓         |
                                ↓      ↑                  |   ------------   |
                                ↓      ↑                  |   |  Node 1  |   |
                                ↓      ↑                  |   ------------   |
                            -----------------             |   ------------   |
                            | Helm registry |             |   |  Node 2  |   |
                            -----------------             |   ------------   |
                                                          --------------------

## **Explaining it in a video**

Here you can get an explanation in a video. [59/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=-IkumgCSFuY&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=56)