On the thirty second day, I learned the following things about GitHub Actions.

# GitHub Actions

- GitHub actions will automate the software development workflows right in your repository.

- Let's say you pushed some changes in a branch to GitHub and you want those changes to be merged but the new code that you have added, you do not want to break the existing code with it. In this way, GitHub actions come into picture.

- It will run some checks before the code is pushed or pulled so that after only running those checks, the code will be pushed.

- You can read the documentation related to workflow, events, runner etc in this [page](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions).

## Quickstart

- Visit this [website](https://docs.github.com/en/actions/quickstart) and you will see all the steps in order to automate the workflow.

- First create a directory and inside this directory initialize the git by writing `git init`.

- Once the git is initialized, create the subdirectory by the name of github and command is `mkdir .github`.

- If you want to check, type `ls -a`. It will show you *.git* and *.github* directories.

- Create subdirectory inside the github directory by the name of the workflows by typing the command `mkdir .github/workflows`. Type `ls .github`. It will show you the workflow inside the *.github* directory.

- After creating the *workflows* directory, create a file in it by writing `touch .github/workflows/github-actions-demo.yml`.

- Open this newly created file and copy the data from the [website](https://docs.github.com/en/actions/quickstart) and paste it inside the file.

      name: GitHub Actions Demo
      run-name: ${{ github.actor }} is testing out GitHub Actions 🚀
      on: [push]
      jobs:
        Explore-GitHub-Actions:
          runs-on: ubuntu-latest
          steps:
            - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
            - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
            - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
            - name: Check out repository code
              uses: actions/checkout@v3
            - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
            - run: echo "🖥️ The workflow is now ready to test your code on the runner."
            - name: List files in the repository
              run: |
                ls ${{ github.workspace }}
            - run: echo "🍏 This job's status is ${{ job.status }}."

- This entire data inside this file is called a workflow.

- The jobs that you see above will only run if a particular event is occured.

- The `on` tag shows the event that if the code is pushed then run these jobs.

## Work on the file

- Make *names.txt* file in the workflow directory by writing `touch names.txt`.

- Write `git status` to check the status.

- Add all the data in the git by writing `git add .`

- Commit it in the git by writing `git commit -m <message>`.

- Create a new public repository on GitHub.

- Once the repo is created, write `git remote add origin https://github.com/<username>/<repo-name>.git` to add the repo in the origin.

- After committing the data, write `git push origin master` to push the data in the repository.

- After pushing the data, if you go to the Actions tab in the repository, you will se that the github actions are performed.

- Write something in the *names.txt* and push it again by creating another branch and creating a pull request. If you went back to the Actions tab, you will again see that the github actions are performed.

## Create another file

- Create a file by the name *deployment.yml* and write the following data in it.

      apiVersion: apps/v1
      kind: Deployment
      metadata:
        name: nginx-deployment
        labels:
          app: nginx
      spec:
        replicas: 3
        selector:
          matchLabels:
            app: nginx
        template:
          metadata:
            labels:
              app: nginx
          spec:
            containers:
            - name: nginx
              image: nginx:1.14.2
              ports:
              - containerPort: 80

- Create another file in the workflows directory by the name *kubescape-demo.yml* and write the following data in it.

      name: Kubescape

      on:
        push:
          branches: [ master ]
        pull_request:
          branches: [ master ]

      jobs:
        nsa-security-check:
          runs-on: ubuntu-latest

          steps:
            - name: Checkout
              uses: actions/checkout@v2
            
            - name: Install Kubescape
              run: curl -s https://raw.githubusercontent.com/kubescape/kubescape/master/install.sh | /bin/bash

            - name: Scan YAML files
              run: kubescape scan framework nsa *.yml

## **Explaining it in a video**

Here you can get an explanation in a video. [32/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=jfEkQN1UpUU&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=30)