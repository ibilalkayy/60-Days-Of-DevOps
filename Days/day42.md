On the forty second day, I learned the following things about Ansible.

### **System Administrator**

System administrator is a person who manages all the systems in an organization like which application to install in a particular machine, change the ip address of an OS, or making other users in an OS.

### **Problem**

- The management of the systems would be easy if there are few servers but if there are 1000 or more servers then it would be very difficult for one person to manage all of them in a short period of time.

- If there are many system administrators then as humans they could make mistakes or maybe a company has not enough budget to hire them.

### **Solution**

The solution is automation. The role of system administrator is replaced with DevOps engineers.

- **Configuration:** Each and every detail of your machine(server, storage).

- **Management:** Delete, update, and create the details.

Configuration management tool is a part of operations in DevOps.

Configuration management tool is of two types:

1. Push-based
2. Pull-based

**1. Push-based**: 

- Push-based configuration server pushes configuration to the nodes.

- All the data will be present inside one server and that server will push the data and update their versions to other nodes.

- Push-based configuration is used when you want the full control over other nodes and you don't want to send the data until you want.

- The example of push-based tools are Ansible, and SaltStack.

                                                         -----
                                                         |   |
                                                         -----
                                                          / \
                                                           |  
                                                           |
                                        -----          ----------          -----
                                        |   |  <----   | Server |   ---->  |   |
                                        -----          ----------          -----
                                         / \               |                / \
                                                           |
                                                         -----
                                                         |   |
                                                         -----
                                                          / \

**2. Pull-based**

- The nodes itself check and contact the server periodically(after some time) and fetches the configuration and update the version from it.

- The example of pull-based tools are CHEF, and Puppet.

- Pull-based configuration is used when you add multiple nodes. After that, you don't need to configure them manually. Instead they will do it automatically.

                                                         -----
                                                         |   |
                                                         -----
                                                          / \
                                                           |  
                                                           |
                                        -----          ----------          -----
                                        |   |  ---->   | Server |   <----  |   |
                                        -----          ----------          -----
                                         / \               |                / \
                                                           |
                                                         -----
                                                         |   |
                                                         -----
                                                          / \

## What is Ansible?

- Ansible is a configuration management tool that will automate the processes of the nodes. It will control, and manage the servers automatically so that you don't have to do it manually. 

- It is a push based configuration tool.

- Michael Dehaan developed ansible and the it began in February 2012.

- RedHat acquired it in in 2015.

- Ansible is available for RHEL, Debian, CentOS, Oracle Linux, Windows.

- It can be used in on-promises or in the cloud.

- It turns your code into infrastructure. It means if you want the particular infrastructure, write a code, run it and it will do that for you.

## Structure

                                                   ssh        --------
                                              --------------> | Node |
                        -------------------  /                --------  
                        |                 | /
                        |                 |        ssh        --------
                        |                 | ----------------> | Node |
                        |                 |                   --------
                        |                 | \ 
                        -------------------  \     ssh        --------
                           Ansible Server     --------------> | Node |
                                                              --------

- There is no middleman required in this mechanism.

- Ansible uses YAML to transfer data.

- It communicates with the help of ssh.

- It is an agentless. It means that as in chef, the node was containing the chef-client agent to communicate with chef-server. Here there is no agent required.

- The file in which the recipe or the data is written is called playbook.

## Advantages

- Ansible is free to use for everyone.

- It is very lightweight and is not specific to any OS.

- It is very secure due to its agentless capabilities and SSH security features.

- Ansible does not need any special system administrator skills to install and use it.

- It follows the push based mechanism to push the data. I won't accept the requests that are coming everytime to disturb it. It means that the ansible has a control to push the data the desired time it wants.

## Disadvantages

- Insufficient user-interface. Although ansible-tower is GUI but it is still in the development stage.

- You can't achieve automation by ansible because somehow you have to be involved in it to push the data.

- It is new to the market. Therefore it has limited support and documentation is available.

## Terms used in Ansible

- **Ansible Server:** The machine where ansible is installed and from which all the tasks and playbook will be written.

- **Module:** Basically a module is a command or a set of similar commands meant to be executed on the client side.

- **Task:** A task is a section that consists of a single procedure to be completed.

- **Role:** A way of organizing tasks and related files to be called in a playbook.

- **Fact:** Information fetched from the client system and the global variables with the gather facts operation.

- **Inventory:** File containing the data about the ansible client servers.

- **Play:** Execution of a playbook.

- **Handler:** Task which is called only if a notifier is present.

- **Notifier:** Section attributed to a task which calls a handler if the output is changed.

- **Playbooks:** It consists of a code in YAML format, which describes tasks to be executed.

- **Host:** These are the nodes which are automated by ansible.

## **Explaining it in a video**

Here you can get an explanation in a video. [42/60 Day of DevOps Challenge]()