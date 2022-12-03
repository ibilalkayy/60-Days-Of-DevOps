On the fifteeth day, I learned the following things about CI/CD Pipeline.

## Jenkins Role Base Access Control (RBAC)

- In the previous video, I have shown you how you can create a user but the problem was that the newly created user was also able to configure the jobs of the first user.

- In this video, I am going to prevent this from happening.

- This can possible with the help of role base access control.

- Go to this [website](https://plugins.jenkins.io/) and write role base. You will see that a *Role-based authorization strategy* plugin is shown to you.

- Once the plugin is found, go to the manage plugins option and open the available plugin tab. Search the *Role-based authorization strategy*. You will find it there.

- Check the plugin and click on the install without restart button.

- Once the plugin is installed, restart the dashboard and go to *Configure global security*.

- Here you will see under the *Authorization* that the logged in-users can do anything. Change it to *Role-based strategy*.

- Once you apply and save this, you will see under the security section that manage and assign roles is appeared.

- Click on it and you can manage and assign roles in it.

- Click on the manage roles option to add a new role that is developer.

- After saving it, if you logout and login to the second user, you will see the access denied message because this second user does not have any permission.

- Again login to the first user, and inside the manage role, give the developer the overall read permission and save it.

- Go to the assign role and type the user name that is **ali** and click on add button to add it and then assign the developer role to the user **ali**.

- Apply and save the changes.

- If you login to the second user again, you will see the empty dashboard with no job present in it.

- Now go to the manage roles of the first user and give read and build permission. Apply and save it.

- Login to the second user and you will see that the jobs are appeared but if you open any of the job, it won't give an option to configure.

## Use of git plugin and clean workspace

- First create a job and write `echo "Hello World"` in the execute shell.

- After creating the job, build it and show console output.

- Create a github repository with README file in it and add another file also by clicking on the *add file* option.

- Make it an HTML file and give it a name like *index.html* and write the following data in it.

      <html>
          <body>
              <h1> This is Bilal Khan </h1>
          </body>
      </html>

- Go to the jenkins configuration of the newly created job and write the following data in it.

      ls
      git clone <repository-link>
      cd repo-name
      ls
      cat README.md
      cat index.html

- After writing the data, apply and save it and then build it to get the console output.

- If you build this job again, it will give you an error because the repository is already cloned.

- To tackle this problem, go to the configuration of the job and scroll down to the *build environment* and check the box *Delete workspace before build starts* and then apply and save it.

- If you build it again, it will delete the repository and then again clone it.

- You can also write clone commands somewhere else and just write the `cat` in the execute shell.

- Create a new and then go to the configuration of it. Scroll down and in the *source code management*, check the *Git* option. Enter the repository url and change the branch name from master to main.

- Open the execute shell and write the following commands in it.

      # clone
      # cd jenkins
      ls
      cat README.md
      cat index.html

- The clonning and the changing directory option is already done. Now only the list and cat option will be executed.

- If you made some changes in the github file, and build the jenkins job again, you will see the updated output.

## Trigger Build Remotely

- If you want to execute the jenkins job using the terminal then you can do this by remotely building the trigger.

- Go to the configuration option of the job and scroll down to click on the *Build triggers* option. Give any authentication token name.

- Once you gave token name, there will an example URL that you need to copy and after some modification of writing job name and the token, run it in the browser and it will create a build for you in the jenkins.

- If you want to do the same functionality in the terminal then copy the link and past it with the curl command like this `curl <link>` and execute it. You will see that the new build is created.

- If it is giving you the message to authenticate the user first then you need a install a plugin for that.

- Go to the manage plugins and on the available plugins section, write *build authorization token root* and install it. After installation, restart the jenkins dashboard.

- Once the plugin is installed, take the link from the plugin example [here](https://plugins.jenkins.io/build-token-root/). The link is like this: `http://jenkins.local:8080/buildByToken/build?job=<job-name>&token=<token>`.

- Take this link and paste it in the browser and it will create another build for you.

- Let's create a build in the terminal by typing the command `curl http://jenkins.local:8080/buildByToken/build?job=<job-name>\&token=<token>`. You need to add `\` before `&` sign to run it successfully.

## **Explaining it in a video**

Here you can get an explanation in a video. [50/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=Y96rdfNQMxg&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=48)