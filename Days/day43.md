On the forty third day, I learned the following things about Ansible.

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

- Ansible server contains the ansible packages and the updates will be given to the nodes.

## Steps

- Create an AWS account. Go to the services on the upper left side. Click on the compute and then click on EC2.

- Click on the Instances(Running) and then click on the Launch instance on the upper right corner.

- First give a tag name, then change the number of instances to 3.

- Click on the Applications and OS images to Amazon.

- Scroll down and create a new key pair.

- Further scroll down in the network settings and click on create a new security group. Check the SSH and HTTP boxes. Leave the IP as it is.

- Go to advanced settings and write the following data in the user data by scrolling down.

      #!/bin/bash
      sudo su
      apt update -y

- Click on the launch install button and then click on the view instances.

- After the launching the instances, change the names of them. One would be ansible server and other two would be nodes.

- Now open the ec2 instances one by one in the local machine by using SSH.

- Click on the server option in AWS and copy the public IP address. Once the IP is copied, open the terminal ans write `ssh ec2-user@<public-ip-address>`. It will give us an option to write YES or NO. Type yes and it will give you permission denied message.

- Go to the directory where the ansible key is present and use it in the machine by writing `ssh -i <file-name.pem> ec2-user@<public-ip-address>`.

- It will give another error like this **Permissions 0664 for 'ansiblekey.pem' are too open.**

- To counter this error, change the permission by writing `chmod 0400 ansiblekey.pem` and then again write `ssh -i <file-name.pem> ec2-user@<public-ip-address>`.

- You can exit it by writing **exit** and again run it by writing `ssh -i <file-name.pem> ec2-user@<public-ip-address>`.

- Do the same thing with the nodes also and then go to the ansible server terminal and make it a root user by writing `sudo su`.

- Then download the ansible package by writing `wget http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm`

- Type `ls` command and then install the file that is downloaded by writing `yum install file-name`

- `yum update -y` will update the machine.

- Now install the packages one by one by typing `yum install git python python-pip openssl ansible -y`.

- After downloading the packages, type `ansible --version` to check the version of ansible.

- Now go to the hosts file inside ansible server `/etc/ansible/hosts` and paste the private ip-address of node1 and node2 inside a group. In this way, the record of each node will be inside the ansible server.

      [group-name]
      <private-ip>
      <private-ip>

- The hosts file will only work if the `/etc/ansible/ansible.cfg` file is updated by uncommenting some of the following data. By uncommenting, the hosts file data will be activated and run.

      inventory = etc/ansible/hosts
      sudo_user = root

## Create a user

- First run all three instances and run them as root user by typing `sudo su`.

- Now create a user in all three instances by typing `adduser <username>`.

- Now set the password for this user by typing `passwd ansible` and it will give you an option to enter the password.

- Now switch to the ansible user by typing `su - ansible` in all three instances.

- If you want install a package like `sudo yum install httpd -y`, it will ask you for the password but still not downlaod the package because you don't have the root privileges.

- Exit from the ansible user by typing `exit`, then in the root user type `visudo` in all three instances.

- Now go inside this file and change the following things.

      Allow root to run any commands anywhere 
      root    ALL=(ALL)        ALL
      ansible ALL=(ALL) NOPASSWD: ALL

- Become an ansible user again by typing `su - ansible`.

- Now go to the ansible server and try to install httpd package as an ansible user.

    `sudo yum install httpd  -y`

- Now establish a connection b/w the server and the node. Change all the instances into ansible users. Go to the ansible server by typing `ssh <private-ip-address>`.

- It will give you the `permission denied` message.

- Now we have to do some changes in sshd_config file in all the three instances. Go to the root server and open the `/etc/ssh/sshd_config` file and uncomment and comment the following data.

      PermitRootLogin yes
      PasswordAuthentication yes
      #PasswordAuthentication no

- Do this work in node1 and node2 also and restart all the instances by typing `service sshd restart`.

- Now become an ansible user by typing `su - ansible` in all the instances and type `ssh <private-ip-address>` to get the node access from an ansible user.

- It will ask you for your password and after that you will be inside a particular node.

- Create a file and it will be present in another node.

## Solve a password problem that gets asked everytime

                                                   ssh        ------------------------
                                              --------------> | Public Key in a node |
                        -------------------  /                ------------------------  
                        |                 | /
                        |   Public Key    |        ssh        ------------------------
                        |                 | ----------------> | Public Key in a node |
                        |   Private Key   |                   ------------------------
                        |                 | \ 
                        -------------------  \     ssh        ------------------------
                           Ansible Server     --------------> | Public Key in a node |
                                                              ------------------------

- The public key will be given to all the nodes that will authenticate it and there will be no need to ask for password everytime.

- This is a trust-relationship. It means that root only will make a relationship with the root and a user will only make a relationship with user and that's why you have to be the ansible user on all the nodes to access other nodes by typing `su - ansible`.

- Create keys and run commands as an ansible user by typing `ssh-keygen`.

- Now find the hidden files by typing `ls -a` and you will get the .ssh directory.

- `cd .ssh` will get you into ssh directory.

- `ls` will give you id_rsa, id_rsa.pub, known_hosts files that contains the private, public, and the hosts.

- Now copy the public key file in both the nodes by typing `ssh-copy-id <node-username>@<node-private-ip>`

- Now verify and go to the ansible by going backward from ssh directory by typing `cd ..` and then type `ssh <private-ip>`.

- You will get into the node without the password being asked.

## What if I want to make changes in few nodes or a group of few nodes?

- Switch to ansible server by typing `su - ansible`.

- `ansible all --list-hosts` will give you the list of all the nodes that are connected to the ansible server.

- `ansible groupname --list-hosts` will give you a specific group name that contains the nodes.

- The node ascending order representation starts from 0 to so on and the descending order representation starts from -1 to so on.

- `ansible <groupname>[0] --list-hosts` will give the first node of a particular group.

- `ansible <groupname>[1:4] --list-hosts` will give the details from node 2 to node 5 of a particular group.

- The details of multiple groups can be shown by using colon in between like `<groupname1>[1:3]:<groupname2>[4:3]`.

## **Explaining it in a video**

Here you can get an explanation in a video. [43/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=5O4qvZ5M3pE&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=41)