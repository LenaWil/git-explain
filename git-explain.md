# Git: an abstract overview

## Intro

Ok, first of all, apologies for the little bit abstract explanation. It’s a relatively complicated program, and I want you to know how it actually works, not just the magic commands that fix everything, because they don’t always work. And besides, we are university students, we can do this.
I also recommend _(and assume you use something like)_ [SourceTree](https://www.sourcetreeapp.com/) as a GUI to git, which normally only has a CLI. [GitKraken](https://www.gitkraken.com/) also works.

I don't go that much in depth in the actual commands, since I am assuming you use SourceTree. Also this is the first time I actually try to explain git to someone else, and I have no idea how much experience you guys have. If this goes too quickly, there is a way longer tutorial listed below. I think I already spent too much time on this. But please ~~leave a like and subscribe~~ let me know how it goes.  

![git xkcd 1](https://imgs.xkcd.com/comics/git.png)  
_Quote from the XKCD: If that doesn't fix it, git.txt contains the phone number of a friend of mine who understands git. Just wait through a few minutes of 'It's really pretty simple, just think of branches as...' and eventually you'll learn the commands that will fix everything._

## Summary

Ok, git is a distributed version control system. This means it’s an app that keeps records of versions of your data (in most cases: source code) Distributed means, among some other things, that it works offline.  

### Branches, commits and clones

A git repo(sitory) consists of branches, the default being called ```master```. (insert bad BDSM joke here)  
Branches consist of a pointer to the last `commit`.  
Commits are small versions or snapshots of your version of the source code, consisting of a snapshot of the version of the code, a pointer to the previous commit (a ```NIL``` pointer if it is the first one) and if it is a merge commit, (a commit that merges two branches), a second (and sometimes even a third in a 🐙merge) pointer to the commit it merges. Commits also contain metadata about the date they were created and the author. (For those who follow 2IL50, the commit history is btw a DAG.)

Commits are immutable, and the pointer is a cryptographic hash.  
Selecting files to commit is called staging.

![git history](https://i.stack.imgur.com/DOXN0.png)  
_A picture of a sample git commit history tree_

![bad history](https://imgs.xkcd.com/comics/git_commit.png)  
_A much less informative history, listed in ascending order instead of descending_

#### Checking out a branch (`git checkout`)

If you clone a repo, the `master` branch is checked-out by default. This means that the version that's currently in the directory is the commit your `master` branch points to. You can use SourceTree or the `git branch` command to create or switch to a different one. There is a special branch, called `HEAD` that points to the currently checkout version of the code. (Most of the time, SourceTree doesn't display the the head branch, but just displays the current branch in **bold**).

Git works mostly offline. If you clone (aka download) a git repo, you also download the entire commit history. If you then add a commit, the branches on your computer are updated, but the branches on the server are not.  

### `Push` and `Pull`

For that, there are two operations, Push: sending your commits to the server; and Pull: downloading the new commits from the server. (Insert another bad sex joke here)  
`Push` fails if the commits on the server contain newer ones, `pull` doesn't, unless there are merge-conflicts, which SourceTree will ask you to solve. Therefore, push before you pull.
We could just all use the master branch, but it’s also possible to use a new temporally branch, then asking someone else to review the code, (AKA sending a pull request) and then asking the reviewer to merge that code. (AKA merging a pull request) There are git repos where only the _‘dictator’_ (aka scrum master; aka probably Willem) has push permission on the master branch on the main repo and repos where everyone has. I don’t know which permission model is the best for this project, my suggestion is though to put some safeguards in place so someone doesn’t mess up the entire repo.  

_(As of 1 April, there are restrictions in place to not directly push to master-branch for everyone except @TijmenW and Willem. If you want to experiment, please use a fork. If you think you can bear the responsibility, please message them.)_

There are some advanced options for the `pull` command, that make for a cleaner commit history, ~~but they are complicated and outside the scope of this short tutorial.~~ in the chapter below.

![xkcd github for lesbians](https://imgs.xkcd.com/comics/branding.png)

### `git rebase`, `git commit --amend`, `git reflog` and `git reset`

If you made mistake, for example, you committed all your passwords, and you want them removed from Git history, it's possible to use these commands to change/rewrite history. However, they are very dangerous, and it takes a long time to explain them. Because I don't know how well the rest of the tutorial will go, I haven't (yet) explained them (all) here in detail. In the meanwhile, please use the [book](https://git-scm.com/book/en/v2) if you want to know more about them.

`git commit --amend` is a commit that creates a new commit, but makes the parent be the parent of the current commit, and deletes the current commit if that was the only reference.  

`git reset` resets the commit-pointer of the branch to a given commit.

`git rebase` travels through time and changes history. It's way to complicated to explain here.

`git reflog` lists recent commits. Very handy if you want to undo any of the above commands.

### forks

There are also things called forks, which is a fancy name for a copy of a git repo in your own namespace from which you can send merge requests.

Most of the time, both the fork and the original repo should be added as a remote.

**Important note**: If you fork the project, please add the 2IOA0 group as a reporter in _Project Settings_ (left down) → _Members_.

### `git fetch`

I forgot about one of the commands: ```git fetch```. Git has a possibility to bookmark repo-URLs. Bookmarks are called `remote`s. For those repos the branches are mirrored to the local git repo on the PC; ```origin/master``` for example is the Git branch on the main repo if you called that main repo ```origin```. ```Git fetch``` refreshes those repos.

## Practical things

Start by cloning the repo. I recommend to use the https url listed at the repo page on Windows, it really doesn’t like SSH keys. (And SSH-keys are complicated to set up). Also, use SourceTree to do so.
It’s possible to use GitKraken.  

### GitLab specific stuff

* Has, like almost all git hosters, built-in pull requests.  
* Has an autobuild (CI/CD) function that runs tests and publishes it as a website that we could potentially use. (It’s basically Momotor+website hosting, only you can write the tests now, and not the TU/e staff, and you don’t get a bad grade if your tests fail.)  
* The master branch is restricted by default. It e.g. doesn’t allow you to use a force push. (A push that rewrites history.)  
* ~~If you sent a pull request, and there is a option to allow write access to other people, you should always enable that.~~
* * Actually, please add the group as reporter by the group members. GitLab doesn't do that automatically for some reason.
* Use your username and password of GitLab when asked in SourceTree. I think there is a password reminder function somewhere but forgot where. 🤷‍♂️
* * The command `git config credential.helper` should return `manager`. 
* * If that doesn't work, I think it was the [Microsoft Git Credential Manager for Windows](https://github.com/Microsoft/Git-Credential-Manager-for-Windows). Not sure though.

### Project structure

* The repo url is <https://gitlab.com/2IOA0-y2019-g28/2IOA0>, the git one <https://gitlab.com/2IOA0-y2019-g28/2IOA0.git>, in theory it’s possible to make a second project under the url <https://gitlab.com/2IOA0-y2019-g28/second-project>.  
* If you want a better, but longer, tutorial, that isn't written by me: <https://git-scm.com/book/en/v2>.  Also available in [Dutch](https://git-scm.com/book/nl/v2) and mostly available in [Polish](https://git-scm.com/book/pl/v2).
* You can also look up the syntax of the CLI: <https://git-scm.com/docs/git-commit>.  
* * Again, SourceTree is often easier.

Feel free to ask questions.

Tijmen Wildervanck
