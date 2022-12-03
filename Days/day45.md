On the forty fifth day, I learned the following things about Ansible.

# Playbook

- More than one command present in a YAML file will be called playbook. The combination of modules is called playbook.

- Playbook in ansible is written in YAML format.

- It is a human readable data serialzation language. It is commonly used for configuration.

- Playbook is like a file where you write code consist of vars, handlers, files, templates, and roles.

- Each playbook is composed of one or more "modules" in a list. Module is a list of configuration files.

- Playbook is divided into many sections.

    - **Target section:** Defines the host against which playbook task has to be executed.

    - **Variable section:** Defines variables. If there are multiple variables then just change a first variable and it will update all the values.

    - **Task section:** List of all modules that need to run in an order.

## YAML

- For ansible, nearly every YAML file starts with a list.

- Each item in a list is a list of key-value pairs commonly called a dictionary.

- All the YAML files will begin with **---** and end with **...**

- All members of a list lines must begin with some indentation level starting with space.

    For example: 
    
      --- # A list of fruits
      Fruits:
      - Mango
      - Strawberry
      - Banana
      - Grapes
      - Apple
      ...

- A dictionary is represented in a simple key-value pair.

    For example: 
    
      --- # Details of customer
      Customer:
        Name: Bilal
        Job: YouTuber
        Skills: DevOps
        Exp: 1 year
      ...

    **Note:** There should be space b/w **:** and the value.

## Target section

### Steps

- Start the instances, connect the ansible server with node by using `ssh -i <file-name.pem> ec2-user@<public-ip-address>`.

- After that, go to ansible server by typing `su - ansible`.

- Create a YAML file by the name of *target.yml* and write the following data in it.

      --- # Target Playbook
      - hosts: groupname
        user: ansible
        become: yes
        connection: ssh
        gather_facts: yes
      ...

- `become: yes` means to give the sudo privilege.

- `gather_facts: yes` will gather the private ip addresses of the nodes.

- Execute the file by writing `ansible-playbook target.yml`

- To check the idempotency, execute the above command, and this will show the `changed=0` because the task is not repeated.

## Task section

### Steps

- Create a YAML file by the name of *task.yml* and write the following data in it.

      --- # Task Playbook
      - hosts: groupname
        user: ansible
        become: yes
        connection: ssh
        gather_facts: yes

        tasks:
          - name: Install httpd on Linux
            action: yum name=httpd state=installed
      ...

- `yum` is the module name.

- You can also write `present` as a state that will install a package.

- Before executing a file, first remove the `httpd` package from all the nodes by typing `sudo yum remove httpd -y`.

- Execute the file by writing `ansible-playbook task.yml` and it will show you `changed=1` because something new is added.

- After executing a file, type `which httpd` in all the nodes to confirm the installation.

## Variables section

- Ansible uses variables which are defined previously to enable more flexibility in playbooks and roles. They can be used to loop through a set of given values, access various information like the host name of a system and replace certain strings in templates with specific values.

- Put variable section above tasks so that we define it first and use it later.

### Steps

- Go to ansible server and switch to ansible user.

- Create a YAML file by the name of *vars.yml* and write the following data in it.

      --- # Variables Playbook
      - hosts: groupname
        user: ansible
        become: yes
        connection: ssh
        gather_facts: yes

        vars:
          - pkgname: httpd    
        tasks:
          - name: Install httpd on Linux
            action: yum name='{{pkgname}}' state=installed
      ...

- Before executing a file, first remove the httpd package from all the nodes by typing `sudo yum remove httpd -y`.

- Execute the file by writing `ansible-playbook vars.yml`

- After executing a file, type `which httpd` in all the nodes to confirm the installation.

## Handlers Section

- A handler is exactly the same as a task but it will run when it is called by another task.

- The first task will be executed and then it will be shifted to another task. Without the first task completion, the second task won't complete.

- The first task must contain the notify directive to indicate and also notify that it changed something.

### **Steps**

- Go to ansible server and switch to ansible user.

- Create a YAML file by the name of *handlers.yml* and write the following data in it.

      --- # Handlers Playbook
      - hosts: groupname
        user: ansible
        become: yes
        connection: ssh  
        tasks:
          - name: Install httpd server
            action: yum name=httpd state=installed
            notify: restart HTTPD
        handlers:
          - name: restart HTTPD
            action: service name=httpd state=restarted
      ...

- `handlers` value must be equal to `notify` value so that the handlers will run only after the task is completed.

- Before executing a file, first remove the httpd package from all the nodes by typing `sudo yum remove httpd -y`.

- **Dry run:** Check whether the playbook is formatted correctly before an execution by typing `ansible-playbook handlers.yml --check`.

- Execute the file by writing `ansible-playbook handlers.yml`.

- After executing a file, type `which httpd` in all the nodes to confirm the installation.

- For checking the status, write `sudo service httpd status` in all the nodes. If it is `active` then it means the `httpd` is running.

## Loops

- Sometimes you want to repeat a task multiple times. In computer programming, this is called loops.

- Common ansible loops include changing ownership on several files and/or directories with the file module, creating multiple users with the user module, and repeating a pulling step until certain results are reached.

### **Steps**

- Go to ansible server and switch to ansible user.

- Create a YAML file by the name of *loops.yml* and write the following data in it.

      --- # Loops Playbook
      - hosts: groupname
        user: ansible
        become: yes
        connection: ssh  
        tasks:
          - name: Add a list of users in the nodes
            user: name='{{item}}' state=present
            with_items:
              - Bilal
              - Ali_ahmed
              - Zeeshan
              - Rahmat
      ...

- It will go inside the node1 of a groupname and create the users one after the other. Then it will go to node2 of a groupname and create the users one after the other.

- The username should be written without a space, otherwise it will us an error.

- Execute the file by writing `ansible-playbook loops.yml`.

- To verify, go inside any node and type `cat /etc/passwd`.

## **Explaining it in a video**

Here you can get an explanation in a video. [45/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=I9aU6a40u7Y&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=43)