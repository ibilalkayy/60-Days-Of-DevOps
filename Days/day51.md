On the fifty first day, I learned the following things about CI/CD Pipeline.

## Build after other project are build (jenkins upstream and downstream)

- Now let's take a look that how to link two jobs so that the previous one won't be executed unless the first one is executed.

- If the first job(upstream) is executed then the second job(downstream) will start.

- First create a job by the name of upstream and then go to the configure to write `echo "Hello World"` in the execute shell.

- Then create the second job by the name of downstream and go to the configuration. Scroll down and in the *build triggers* option check the option that is *build after other projects are build*

- It will give you an option to link the previous project(upstream) with downstream project.

- Write the `echo "Hello World"` and `sleep 5` commands in the execute shell.

- Apply and then save the configuration.

- Build the upstream job and wait for 5 seconds when the sleep time is over then the second job(downstream) will automatically be executed.

- You can design a CI/CD pipeline using upstreaming and downstreaming.

## Build after other project are build (failed, unstable job)

- Open the newly created job(downstream job) configuration and scroll down to go to the *build trigger* option and check another option that is *Trigger even the build fails*.

- Apply and save the configuration.

- After applying if you made changes in the previous job(upstream job) and write an unexisted in it, the next job will still be executed even if the first one fails.

- Now let's apply the unstable functionality in the upstream job.

- First open the newly created job(downstream job) configuration and scroll down to go to the *build trigger* option and check another option that is *Trigger even the build is unstable*.

- Apply and save the configuration.

- Once you apply the changes, go to the previous job(upstream job), scroll down and write `exit 10` in the *Execute shell*.

- Go to the advanced option of the *Execute shell* and then write `10` in the *Exit code to set build unstable* option.

- It will show that after 10 seconds, the upstream job will become unstable and downstream job will start executing.

## Build Periodically

- If you want to execute a job and create build after every 2 minutes or any time that you want then you can do it.

- To do this, first create a job and then go to the configuration. Scroll down and write `date` in the *Execute shell*.

- After writing the data in the execute shell, scroll up and go to the *build triggers* option and check the *Build periodically* option.

- Once it is checked then you can schedule the task by writing the cron job in it. You can get an example by clicking on the question mark.

- Write `H/2 * * * *` to execute the job and build it after every two minutes.

## Poll SCM(Source code management)

- If you want to monitor the changes in your github repository then you can also do this.

- First create a job and then go to the configuration. Scroll down and go to the *build triggers* option and check the *Poll SCM* option.

- Once it is checked then you can schedule the task by writing the cron job in it. You can get an example by clicking on the question mark.

- Write `H/2 * * * *` to execute the job to monitor the changes after every 2 minutes.

- The next is to create a github repository and take a link of that repository by clicking on the code button and getting the HTTPS link.

- Once the link is copied, go to the jenkins dashboard and go to the source code management in the configuration.

- Select the Git option, paste the link there and change the branch from master to main.

- Go to the execute shell and write the following data into it.

      ls
      cat README.md
      cat index.html

- After making changes, apply and save the configuration.

- Wait for the first build and if you wait for 2 minutes, the build will not happen because no changes are made in the github.

- Now make some changes in the github and wait for 2 minutes. After 2 minutes, you will see that the build is created.

- If you open the console output, you will see that changes are now present.

## **Explaining it in a video**

Here you can get an explanation in a video. [51/60 Day of DevOps Challenge]()