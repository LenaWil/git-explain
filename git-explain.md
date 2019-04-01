# Git: an abstract overview

## Intro

Ok, first of all apologies for the little bit abstract explanation. It’s a relatively complicated program, and I want you to know how it actually works, not just the magic commands that fix everything, because they don’t always work. And besides, we are university students, we can do this.
I also recommend [SourceTree](https://www.sourcetreeapp.com/) as GUI to git. [GitKracken](https://www.gitkraken.com/) also works.

## Summary

Ok, git is a distributed version control system. This means it’s an app that keeps records of versions of your data (in most cases: source code) Distributed means, among some other things, that it works offline.  

### Branches, commits and clones

A git repo(sitory) consist of branches, the default being called ```master```. (insert bad BDSM joke here)  
Branches consist of a pointer to the last commit.  
Commits are small versions or snapshots of your version of the source code, consisting of a snapshot of the version of the code, a pointer to the previous commit (a ```NIL``` pointer if it is the first one) and if it is a merge commit, (a commit that merges two branches), a second (and sometimes even a third in a 🐙merge) pointer to the commit it merges. Commits also contain metadata about the date they were created and the author. (For those who follow 2IL50, the commit history is btw a DAG)

Git works mostly offline. If you clone (aka download) a git repo, you also download the entire commit history. If you then add a commit, the branches on your computer are updated, but the branches on the server are not.  

### Push and Pull

For that, there are two operations, Push: sending your commits to the server; and Pull: downloading the new commits from the server. (Insert another bad sex joke here)  
We could just all use the master branch, but it’s also possible to use a new temporally branch, then asking someone else to review the code, (AKA sending a pull request) and then asking the reviewer to merge that code. (AKA merging a pull request) There are git repos where only the _‘dictator’_ (aka scrum master; aka probably Willem) has push permission on the master branch on the main repo and repos where everyone has. I don’t know which permission model is the best for this project, my suggestion is though to put some safeguards in place so someone doesn’t mess up the entire repo.  

_(As of 1 April, there are restrictions in place to not directly push to master-branch for everyone except Tijmen and Willem. If you want to experiment, please use a fork. If you think you can bear the responsibility, please message them.)_

### forks

There are also things called forks, which is a fancy name for a copy of a git repo in your own namespace from which you can send merge requests.

### git fetch

I forgot about one of the commands: ```git fetch```. Git has a possibility to bookmark repo-urls. For those repo’s the branches are mirrored to the local git repo on the PC; ```origin/master``` for example is the Git branch on the main repo if you called that main repo ```origin```. ```Git fetch``` refreshes those repos.

## Practical things

Start by cloning the repo. I recommend to use the https url listed at the repo page on Windows, it really doesn’t like SSH keys. (And SSH-keys are complicated to set up). Also use SourceTree to do so.
It’s possible to use GitKracken.

## GitLab specific stuff

* Has, like almost all git hosters, built-in pull requests.  
* Has a autobuild (CI/CD) function that runs tests and publishes it as a website that we could potentially use. (It’s basically Momotor+website hosting, only you can write the tests now, and not the TU/e staff, and you don’t get a bad grade if your tests fail.)  
* The master branch is restricted by default. It e.g. doesn’t allow you use a force push. (A push that rewrites history.)  
* If you sent a pull request, and there is a option to allow write access to other people, you should always enable that.
* Use your username and password of GitLab when asked in SourceTree. I think there is a password reminder function somewhere but forgot where. 🤷‍♂️

### Project structure

* The repo url is <https://gitlab.com/2IOA0-y2019-g28/2IOA0>, the git one <https://gitlab.com/2IOA0-y2019-g28/2IOA0.git>, in theory it’s possible to make a second project under the url <https://gitlab.com/2IOA0-y2019-g28/second-project>.  
* If you want a better tutorial: <https://git-scm.com/book/en/v2>.  
* You can also look up the syntax of the CLI: <https://git-scm.com/docs/git-commit>.  
* * Again, SourceTree is often easier.

Feel free to ask questions.

Tijmen Wildervanck
