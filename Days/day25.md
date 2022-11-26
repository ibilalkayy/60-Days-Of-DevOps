On the twenty-fifth day, I learned the following things about Kubernetes.

## **Deployment and Rollback**

                                                    --------------
                                                    | Deployment |
                                                    --------------
                                                           |
                                                           |
                                      -------------------------------------------
                                      |                    |                    |
                                      | <<<<<<<<<<<<<<<<<< | <<<<<<<<<<<<<<<<<< |
                                  ----------           ---------- <<<<<<<<< ----------
                                  |   RS   |           |   RS   |           |   RS   |
                                  |   V1   |           |   V2   |           |   V3   |
                                  ----------           ----------           ----------
                                      /\                   /\                   /|\
                                     /  \                 /  \                 / | \
                                    /    \               /    \               /  |  \
                             --------  --------    --------  --------   -------- | --------
                             | Pod1 |  | Pod2 |    | Pod1 |  | Pod2 |   | Pod1 | | | Pod2 |
                             --------  --------    --------  --------   -------- | --------
                                                                                 |
                                                                              --------
                                                                              | Pod3 |
                                                                              --------

- Replication control and replica set is not able to do updates and rollback apps in the cluster.

- A deployment works as a supervisor for pods, giving you control over how and when a new pod is updated or rolled back to the previous state.

- When using deployment object, we first define the state of an app then K8s cluster schedules an app onto specific individual nodes.

- K8s monitors if the node goes down or pod is deleted then the deployment controller replaces it.

- A deployment provides declaration updates for pods and replicaset. Deployment will send a request to the replicaset and replicaset will implement the functionality on pod.

- **Note:** If the deployment rolled back from the version 3 replicaset to the version 2 replicaset, then the version 3 replicaset pods will be present in the version 2 replicaset. Although the code is of version 2 but the pods are of version 3.

## **Use cases of Deployment**

- Deployment rollsout the replicaset. The replicaset creates pods in the background and check the status of the rollout to see if it is succeeded or not.

- If a new version of the replicaset is created then the previous version replicaset will stop working and the pods of that previous version will be deleted. If the previous version replicaset activated again then the pods will be newly created.

- Scale up and scale down the deployment to facilitates more load.

- Pause the deployment if you want to remove some errors and then resume back to start a new rollout.

- Clean up older replicaset that you don't need anymore.

- If there are problems in the deployment, kubernetes will automatically go to the previous version, however you can also explicitly rollback to a specific version.

      kind: Deployment
      apiVersion: apps/v1
      metadata:
        name: mydeployment
      spec:
        replicas: 2
        selector:		# tell the controller which pods to watch/belongs to
          matchLabels:
            name: deployment
        template:
          metadata:
            name: testpod
            labels:
              name: deployment
          spec:
            containers:
              - name: c00
                image: ubuntu
                command: ["bin/bash", "-c", "while true; do echo Bilal Khan; sleep 5; done"]

- **Note:** The format of the replicaset is always formatted as [deployment-name]-[random-string].

- `kubectl get deploy` will show you the list of deployments and their status, whether they're created or not.

- `kubectl describe deploy deployment-name` will check that how deployment creates RS and pods.

- `kubectl get rs` will give the replicaset.

- `kubectl scale --replicas=1 deploy deployment-name` will scale up or scale down the deployment.

- `kubectl logs -f podname` will check what is running inside the containers.

- Change the image in a file to centos and apply again to get the new replicas created.

- After changing the image in a file, to check which OS image, you can write `kubectl exec deployment-pod-name -- cat /etc/os-release`.

- `kubectl rollout status deployment deployment-name` will give you the current status of the roll out.

- `kubectl rollout history deployment deployment-name` will give you the history of deployment.

- `kubectl rollout undo deploy/deployment-name` will help you to rollback to only one previous version. 

- `kubectl rollout undo deploy/deployment-name --to-version` will help you to rollback to a specific version by specifying it with `--to-version`.

**Deployment failure**

Your deployment may get stuck trying to deploy its newest replicaset without ever completing. This can occcur due to some following factors.

- Insufficient Quota(Insufficient space in node)

- Readiness probe failures(pods were not ready to be readed)

- Image pull errors(Image is not addressed in manifest file)

- Insufficient permission(No permission to fetch)

- Limit ranges(Limits are exceeded)

- Application runtime configuration(App didn't run)

## **Explaining it in a video**

Here you can get an explanation in a video. [25/60 Day of DevOps Challenge]()