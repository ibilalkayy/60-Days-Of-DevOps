On the forty sixth day, I learned the following things about Ansible.

# Ansible Conditions

- Whenever we have different scenarios, we put conditions according to different scenarios.

## When Statement

- If there are multiple servers of different operating systems then in order to run let's say the last server, it will skip the first few servers of particular nodes to reach the selected one and run it.

- Start the instances, connect the ansible server with node by using `ssh -i <file-name.pem> ec2-user@<public-ip-address>`.

- After that, go to ansible server by typing `su - ansible`.

- Create a YAML file by the name of *condition.yml* and write the following data in it.

      --- # Condition Playbook
      - hosts: groupname
        user: ansible
        become: yes
        connection: ssh
        tasks:
            - name: install apache on debian
              command: apt-get -y install apache2
              when: ansible_os_family == "Debian"
            - name: install apache on redhat
              command: yum -y install httpd
              when: ansible_os_family == "RedHat"
      ...

- For Amazon Linux and redhat, the `httpd` will install the `apache` but only the name is different.

- Before executing a file, first remove the `httpd` package from all the nodes by typing `sudo yum remove httpd -y`.

- Execute the file by writing `ansible-playbook condition.yml` and it will show you `changed=1` and `skipped=1` because new thing is added and one package is skipped.

- After executing a file, type `which httpd` in all the nodes to confirm the installation.

# Vault

- Ansible allows keeping sensitive data such as passwords or keys in encrypted form rather than a plaintext in your playbooks.

- To create a new encrypted playbook, write `ansible-vault create vault.yml`.

- Edit the encrypted playbook by writing `ansible-vault edit vault.yml`.

- To change the password, write `ansible-vault rekey vault.yml`.

- To encrypt an existing playbook, write `ansible-vault encrypt file.yml`.

- To decrypt an encrypted playbook, write `ansible-vault decrypt file.yml`.

- The latest **AES256** technique is used in the encryption.

# Roles

- We can use two techniques for running a set of tasks. One is includes and another is roles.

- Roles are good for organizing tasks, handlers, vars etc and encapsulating(putting data in a box) the data needed to accomplish those tasks, handlers, vars etc.

- If any task, handler etc is required, the roles will only contact that box. In this way, the traffic will be distributed.

- Some of the things that the roles contain are.

                                                    Ansible Roles
                                                          |
                                                          |
                                ----------------------------------------------------
                                |        |        |        |       |        |      |
                                |        |        |        |       |        |      |
                              Default  Files   Handlers  Meta  Templates  Tasks  Vars

- We can organize playbooks into a directory structure called roles.

- Adding more and more functionality to the playbook will make it difficult to maintain in a single file.

                                                    Playbook
                            -----------------------------------------------------------
                            |         master.yml                      Roles           |
                            |  ------------------------     ------------------------  | 
                            |  |                      |     |        myrole        |  |
                            |  |                      |     |  ------------------  |  |
                            |  |       Target         |     |  | -------------- |  |  |
                            |  |                      |     |  | |    Tasks   | |  |  |
                            |  |                      |     |  | |   main.yml | |  |  |
                            |  |                      |     |  | -------------- |  |  |
                            |  |       Roles          |     |  | -------------- |  |  |
                            |  |                      |     |  | |    Vars    | |  |  |
                            |  |       myrole         |     |  | |   main.yml | |  |  |
                            |  |                      |     |  | -------------- |  |  |
                            |  |                      |     |  | -------------- |  |  |
                            |  |                      |     |  | |  Handlers  | |  |  |
                            |  |                      |     |  | |  main.yml  | |  |  |
                            |  |                      |     |  | -------------- |  |  |
                            |  |                      |     |  ------------------  |  |
                            |  ------------------------     ------------------------  |
                            -----------------------------------------------------------

- Every task will be defined in the myrole directory. If I want to go to a specific task, I will simply open that one instead of searching the whole playbook.

- *master.yml* file will run myrole playbook and it will contact the directories that has a specific role assigned to it.

  - Target contains the ansible server and the nodes that will run the task.
  - myrole contains the tasks, vars, handlers etc that will be executed if required. 
  
  - You can only the change myrole directory name. Others are not allowed.

## Different kind of roles

- **Default:** It stores the data about the role/application. Default variables example is: If you want to run port 80 or 8080 then variables needs to be defined in this path.

- **Files:** It contains files that need to be transferred to the remote VM(static files).

- **Handlers:** They are triggers or or a next task that will run after the first task is completed.

- **Meta:** It contain the files that establish roles dependencies e.g -> author name, supported platform, dependencies if any.

- **Tasks:** It contains all the tasks that are normally in the playbook e.g -> installing packages and copies files etc.

- **Vars:** Variables for the role can be specified in this directory and used in your configuration files. Both vars and default store the variables.

## Steps

- Make some directories by typing `mkdir -p playbook/roles/webserver/tasks`. `-p` is for the parent directory.

- Move to the playbook directory by typing `cd playbook`.

- Make a file inside the **tasks** directory by typing `touch roles/webserver/tasks/main.yml`.

- Make a file inside the **playbook** directory by typing `touch master.yml`

- Open the *main.yml* file and write the following things.

      - name: install apache
        yum: pkg=httpd state=latest

- Open the *master.yml* file and write the target and the roles(mention the webserver that is the present inside the roles directory).

      - hosts: groupname
        user: ansible
        become: yes
        connection: ssh
        roles:
          - webserver

- Before executing a file, first remove the `httpd` package from all the nodes by typing `sudo yum remove httpd -y`.

- `ansible-playbook master.yml` will call the *master.yml* file. *master.yml* file will call the roles. Roles will call the webserver because it is mentioned in the *master.yml* file. After that, the *main.yml* file inside the **tasks** directory will be executed. If something is defined in **handlers** and **vars** directory, that will also be executed.

- After executing a file, type `which httpd` in all the nodes to confirm the installation.

## **Explaining it in a video**

Here you can get an explanation in a video. [46/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=j-U-wmr_abM&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=44)