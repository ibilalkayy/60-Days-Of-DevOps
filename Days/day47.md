On the forty seventh day, I learned the following things about CI/CD Pipeline.

# CI/CD Pipeline

- A continuous integration and continuous deployment (CI/CD) pipeline is a series of steps that must be performed in order to deliver a new version of software.

- CI/CD is a methodology. It's not a tool.

- The code won't be deployed all at once because it will create a problem for a developer to review it again after some days or months. Instead the code will be divided in different parts and those parts will be deployed continuously by giving us a feedback that whether it is succeeded or failed.

- The process is automated so that if the bugs are found in between, it will automatically be detected and we can solve it from there.

## Before continuous integration

                    Developer
                        ()          ----------              ----------              ----------
                        /\ -------> |        |              |        |              |        |
                                    |        | ---------->  |        | ---------->  |        |
                        () -------> |        | <------      |        |              |        |
                        /\          ----------       |      ----------              ----------
                                    Repository       |  Integration/Build            Testing
                                                     |                                  |
                                                     |                                  |
                                                     --<--------------<---------------<--

- Before continuous integration, the process was very tense.

- The developers push the files(containing thousand lines of code) to github.

- The next step is to build the code at one place.

- The third step is to test the code from start to the end to find the errors.

## Problem

- This process has a problem that if a file has some minor issues then it will go back to the developers.

- The developers will shift their focus from another project to this problem again.

- They will have to find a minor bug inside a huge file.

## After continuous integration
                            
                    Developer                                ------------------------------------
                        ()          ----------               | ---------- ---------- ---------- |
                        /\ -------> |        |               | |        | |        | |        | |
                                    |        | ----------->  | | Build  | |  Test  | | Deploy | |
                        () -------> |        |               | |        | |        | |        | |
                        /\          ----------               | ---------- ---------- ---------- |
                                    Repository               ------------------------------------
                                        ↑                                  CI Server
                                        ↑                                     ↓
                                        <-------------------<-----------------<
                                            Notification: Success/Failure

- The developer push the files(containing few lines of code) to github.

- The whole application won't be given to the repository and the CI server. Instead the code that is written in one or two days will be given to the CI server to check and then another day some more lines of code will be pushed to check and this process will go on.

- In this way, continuous integration = continuous build + continuous testing.

## CI/CD Pipeline

                                                                            Check the quality and assurance
                     -------------------------------------------------------------------------↑-----
                    /       \           \           \           \           \           \     ↑     \
        ------------|       |  Version  |           |           |           |   Prod.   |  Measure  |
        |  -------> |  Dev. |  Control  |   Build   | Unit Test | Auto Test |    env.   |    and    |
        | ↑  -------|       |           |           |           |           |  Deploy   |  Validate |
        | ↑  |      \       /           /           /           /           /           /           /
        |    |       ------------ ------------ ----------- ---------- ----------- --------- --------
        |    |                  |↓|          |↓|         |↓|        |↓|         |↓|       |↓|
        | ↑  |                  |↓|          |↓|         |↓|        |↓|         |↓|       |↓|
        | ↑  -------------------- ------------ ----------- ---------- ----------- --------- | 
        | ↑    <--------------     <---------   <--------   <-------   <--------   <------  |
        -------------------------------------------------------------------------------------
                            Production feedback and testing at every stage

- The developer will send the code to version control and then it will go through all the stages one by one.

- On each stage, the code will be tested and it will give the feedback.

- If some bug found in any stage then the code will stop there and the feedback will be given to the developer to make it correct.

- In this way, it will be easy to check the code before deployment.


## Jenkins

- DevOps has different phases like the following.

                        --------                                            
                        | Plan | <--   
                        --------   |
                                   |   <---------------                     ----------
                                   |                  ↑                 --> | Deploy | 
                        --------   |                  ↑                 |   ----------   
                        | Code | <--            ---------------    ---> |                 
                        --------                | Integration |   /     |                 
                                                |    Tool     |  /      |   -----------   
                                                |   Jenkins   |         --> | Operate | 
                        ---------               ---------------             -----------
                        | Build |                  ↓  ↓  ↓
                        ---------  <----------------  ↓  ↓
                                                      ↓  ↓                  -----------   
                                                      ↓  -----------------> | Monitor |
                        --------                      ↓                     -----------
                        | Test | <--------------------- 
                        --------

- You will first plan and write the code and then push it to GitHub.

- After that, build the code with many tools like Maven, gradie etc.

- For testing, use the Selenium, Junit tool, etc.

- For deployment and operation, use the Chef, puppet, etc.

- For monitoring, use the nagios tool.

- Jenkins will automate this process of transitioning from one phase to another. It means that after completing the work on the first phase, you don't need to go to the next phase and so on. Instead the Jenkins will automatically go to each of the phase one by one.

- Jenkins is an open-source tool written in Java that runs on Windows, MacOS and Linux. It is free, community supported tool for CI.

- Jenkins automate the entire software development life cycle as I have shown you above.

- Jenkins was originally developed by Sun Microsystem in 2004 under the name Hudson.

- The project was later named Jenkins when Oracle bought Microsystem.

- Jenkins was kept free but the paid enterprise version was released that is called Hudson.

- It can run on any major platform without any compatibility issues.

- There are other alternatives of Jenkins like Bamboo, Travis CI, Buildbot, etc.

- Whenever developers write code, we integrate all that code of all developers at that point of time and we build, test and deliver/deploy to the client. This process is called CI/CD.

- Because of CI, now the bugs will be reported fast so that the entire development process works fast.

## Workflow of Jenkins

            Developer                                                            -----------
                ()              ----------             -----------  ---------->  |  Build  |
                /\ ---------->  | GitHub | ----------> | Jenkins |  <----------  | (Maven) |
                                ----------             -----------               -----------
                                                        ↓ ↓↑ ↑ ↓                      
                                                        ↓ ↓↑ ↑ ↓                      
                                                <-------- ↓↑ ↑ ↓               -------------
                                                ↓         ↓↑ ↑ ------------->  |  Testing  |
                                                ↓         ↓↑ <---------------  | (Selenium)|
                                                ↓         ↓↑                   -------------
                                                ↓         ↓↑
                                                ↓     --------------------
                                                ↓     |  QA(Checkstyle)  |
                                                ↓     --------------------                   CI
                --------------------------------↓-----------------------------------------------
                                                ↓                                            CD
                                            <---- ↓
                                            ↓     ↓    ----------
                                            ↓     ---> | Deploy |
                                            ↓          ----------
                                            ↓     
                                            ↓          -----------
                                            ↓ -------> | Deliver |
                                                       -----------     

- Plugins are available for Jenkins that will help it to communicate with other tools. 

- Developer will write a code. It will be given to the GitHub.

- Jenkins will pull the code from the GitHub and give it to build(maven).

- Jenkins will pull the code from the maven and give it to the testing(selenium).

- Jenkins will pull the code from the selenium and give it to the artifactory(for archiving purpose, it will store the final code that is able to be used). It will also give it to the QA(checkstyle).

- Jenkins will pull the code from the checkstyle and deploy and deliver it.

- After delivery, our work is finished but if the end user or customer does not know how to deploy it, then our technical team go for the support to deploy and deliver the software.

- **Build:** Build will first compile the code,. Then it will review it. Next is to perform unit testing on it. After that, integration testing will be done. At the end, it will package it using WAR or JAR etc.

## Advantages of Jenkins

- It has a lot of plugins available that will help Jenkins to connect with other tools like GitHub, maven, etc.

- You can write your own plugin.

- You can use community plugin that are already present.

- Jenkins is not a tool. It's a framework. You can do whatever you want. All you need are plugins.

- All the things are automated but if you want to manually do some things like building, testing then you can do it manually.

- Jenkins has a master and slaves architecture. Inside Jenkins there is one master and multiple slaves that you can connect who will perform the jobs.

- We can attach multiple slaves(node) to one master(jenkins) that will do the work for us. Master instructs the slaves. If the slaves are not available. Jenkins itself will do the job.

- It can schedule the tasks that after sometime that task will be started.

- It can create the labels for the slaves so that the task will be done by slave1, or slave2.

## **Explaining it in a video**

Here you can get an explanation in a video. [47/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=iCyNVCf5dUA&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=45)