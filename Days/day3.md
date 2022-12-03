On the third day, I learned the following things about GitHub.

- Click on the plus button to create a new repository.
- `git remote add origin repo-copy/link.git` will add the local storage or the origin into the remote server.
- `git remote -v` will give the links of all the repositories from where the data was added or is to be added.
- When the repository is first created, `git push origin branchname` will push the data from the branchname and upload it on GitHub.
- Click on the commit link to see the history of commits.
- Click on the fork button to make a copy of someone else's repository in your own account.
- `git clone repository-link.git` will download the repository data into your local storage.

**Origin Repository**

The copy of the repository that is forked from someone else's account and now it is present in your own account will be called origin.

**Upstream Repository**

Upstream is the original repo that you have forked from an original account.

- `git remote rm origin` will delete the origin data form your local repository.
- `git remote add upstream original-repo/link.git` will add the data of the original repository.
- `git push origin branchname` will send a pull request to the upstream account from the origin account so that upstream could merge those changes into itself.
- In the pull request section, *Merge pull request* option will be appeared so that the owner of the repository could merge the requested data into itself.
- `git fetch --all --prune` will fetch all the data from the upstream or the original account and transfer it to the origin account or a person's repository who forked it. *Prune* means that only the relevant data will be fetched.
- `git reset --hard upstream/main` will delete all your local changes to main. 
- `git pull upstream main` will fetch the data from the upstream and delete all the local changes also.
- Merge conflict will arise if there are multiple changes are committed on the same line.

## **Explaining it in a video**

Here you can get an explanation in a video. [3/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=EX31ny6PQgY&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=2)