On the forty forth day, I learned the following things about Ansible.

There are three ways to push the code from ansible server to the node(s).

1. Ad-hoc commands
2. Modules
3. Playbooks

## 1. Ad-hoc commands

- Ad-hoc means temporary. It will do the things for a short period of time.

- It can run individually to perform quick funtions like creating the files, running or stopping the machines, etc.

- Ad-hoc commands are the linux commands that will be used for temporary purpose.

- The linux commands have no idempotency. It means that it will do one task repeatedly multiple times. It's the drawback of ad-hoc.

- These ad-hoc commands are not used for configuration management and deployment because the commands are of one time usage.

- The ansible ad-hoc commands uses the `/usr/bin/ansible` that contains the commands and this command line tool is used to automate a single task.

### Steps to use ad-hoc commands

- Start the instances first and then go to the directory where the ansible key is present and use it in the machine by writing `ssh -i <file-name.pem> ec2-user@<public-ip-address>` command of all three instances.

- Go to ansible server by typing `su - ansible`.

- `ansible <groupname> -a "ls"` will execute the `ls` command in a particular group. `-a` is an argument that will tell that whatever I am writing in the inverted command should be executed.

- `ansible <groupnme>[0] -a "touch filename"` will create a file in node1 in a particular group.

- `ansible all -a "touch filename"` will create a file in all the nodes and in all the groups.

- `ansible <groupname> -a "ls -al"` will give a long list of hidden files in a particular group.

- `ansible <groupname> -a "sudo yum install httpd -y"` will install the httpd package in all the nodes in a particular group.

- `ansible <groupname> -ba "yum install httpd -y"` will install the httpd package in all the nodes in a particular group. Here the `sudo` is not used. Instead the `b`(become) is used to perform the `sudo` functionality. 

- `ansible <groupname> -ba "yum remove httpd -y"` will remove the httpd package in all the nodes of a particular group.

- To check a package, write `which httpd`. It will show you nothing.

## 2. Ansible Modules

- Module is a single command or single work that will be executed one at a time.

- Ansible ships with a number of modules(called module library) that can be executed on remote hosts or through playbooks.

- It is present by default in the package.

- Your library of modules can reside on any machine and there are no servers, daemons or database required.

- Where the ansible modules are stored?

    - The default location for the inventory file is `/etc/ansible/hosts`.

### Steps to use modules

- `ansible <groupname> -b -m yum -a "pkg=httpd state=present"` will install the httpd package in all the nodes of a particular group. The `m` sign is for module. After that, the `a` is used to insert the argument but this time there is no linux commands. Instead there is a module command. The next step is the `pkg=httpd` that will show the package and the `state=present` will install the package. You can replace `present` with `install` also but the `present` is the standard.

    - To install = present
    - To update = latest
    - To uninstall = absent

- To check a package, write `which httpd` in both the nodes. It will show the `httpd` package.

- `ansible <groupname> -b -m yum -a "pkg=httpd state=latest"` will update the `httpd` package in all the nodes of a particular group. The `state=latest` will update the package.

- `ansible <groupname> -b -m yum -a "pkg=httpd state=absent"` will remove the `httpd` package in all the nodes of a particular group. The `state=absent` will remove the package.

- To check a package, write `which httpd` in both the nodes. It will show you nothing.

- `ansible <groupname> -b -m yum -a "pkg=httpd state=present"` will install the service in all the nodes and then run the service.

- To check a package, write `which httpd` in both the nodes. It will show the `httpd` package.

- To check the status of the service in the nodes, type `sudo service httpd status`. It will show you the inactive message.

- Type `ansible <groupname> -b -m service -a "name=httpd state=started"` in the ansible server and it will start the `httpd` service in all the nodes of a particular group. `state=started` will start the service.

- To check the status of the service in the nodes, type `sudo service httpd status` again. It will show you the active message.

- `ansible <groupname> -b -m user -a "name=<name>"` will create a user in all the nodes of a particular group.

- To check it, type `cat /etc/passwd` in the nodes terminal and they will show you the newly created user at the end.

- First create a file in the ansible server to copy it.

- `ansible <groupname> -b -m copy -a "src=<filename> dest=/tmp"` will copy a file from the ansible server and paste it into **/tmp** directory of all the nodes in a particular group.

- If you want to copy a file into a particular node then type `ansible <groupname>[0] -b -m copy -a "src=<filename> dest=/tmp"`.

- To check the directory, type `ls /tmp/` in a particular node.

- `ansible <groupname> -b -m user -a "name=<name> state=absent"` will remove a user in all the nodes of a particular group.

### How the ansible server will know that a package is already present?

- It is possible with the help of idempotency. It means that the ansible server contains the setup module that will send a request to the nodes and that setup module will check a package whether it is present or not. If it is present then it will not overwrite it. If it is present then it will write it in those nodes.

- The setup command will know whether a package is already present or not.

- Run `ansible <groupname> -m setup` in a server and it will show you all the information of the nodes in a particular group.

- `ansible <groupname> -m setup -a "filter=*ipv4*"` will give you the ip-address of all the nodes in a particular group.

## **Explaining it in a video**

Here you can get an explanation in a video. [44/60 Day of DevOps Challenge]()