# git-cheat-sheet
This is my personal git cheat sheet. This is not a deep dive into how git works, just some of the simple stuff.

# Contribute

Feel free to add to the repo or fix any mistakes you see.  Get started by

- Forking the repo.
- Clone your forked repo into your local machine.
- Create a new branch `git checkout -b your-contribution`.
- After making your changes, `git commit -am 'small message about what you did'`.
- Then push up into the remote repo with `git push origin HEAD`.
- Go to GitHub, go to your forked repo and you should see a yellow bar mentioning your branch.
- After hitting that button and reviewing your changes, hit the `Make Pull Request` button near the bottom.
- I will get an email, notifying me of your Pull Request (PR) and if it's good, I will merge it.

To keep your fork up to date

- add a remote upstream repository with 

  `$ git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git` (the original HTTPS clone Url)

- see all your remotes with `git remote -v`
  ```
  origin  https://github.com/black-shadows/rails.git (fetch)
  origin  https://github.com/black-shadows/rails.git (push)
  upstream  https://github.com/rails/rails.git (fetch)
  upstream  https://github.com/rails/rails.git (push) 
  ```
  - now you have a remote called **upstream** which is the original repo

- Then run `git pull upstream master`, to see your merged contribution on your local machine

# Overview

1. [Starting](#starting)
1. [Git Structure](#git-structure)
1. [Git Logs](#git-logs)
1. [Undo](#undo)
1. [Branches](#branches)
1. [Merging](#merging)
1. [Example Workflow](#example-workflow)
1. [Tricks](#tricks)
  - [Stripspace](#stripspace)
  - [Previous Branch](#previous-branch)
  - [Clean Status](#clean-status)
  - [Auto Correct](#auto-correct)
  - [Alias](#alias)
1. [Remotes](#remotes)
1. [GitHub](#github)
1. [Creating a Git Repo](#creating-a-git-repo)
1. [Git Clone](#git-clone)
1. [Reset](#reset)
1. [Update and Delete](#update-and-delete)
1. [Stash](#stash)
1. [Gitignore](#gitignore)
1. [Compare](#compare)
1. [Version Tags](#version-tags)
1. [Collaborate](#collaborate)
1. [Archive](#archive)
1. [Troubleshooting](#troubleshooting)
1. [Security](#security)
1. [Large File Storage](#large-file-storage)

## Starting

Starting is the easy part.  Make sure you have git installed by opening up your terminal and running,
```
git --version
```
If you're running osx or some form of linux, chances are you already have git installed.  If you're running windows, and/or just don't have git installed (it'll be obvious since entering the above command will spit out an unknown command error), head over to the [official site](https://git-scm.com/downloads) to download and install git for your computer

Now that you are sure you have a working version of git, it's time to create your working repository.

Go inside your project directory (in the terminal) and run `git init`, this will let git know you want it to start keeping track of your changes for this folder.
```
$ cd my_project
$ git init 
```
To verify, run `ls -al` and you should see the `.git` file, that is how you know you have git for this directory. If you no longer want to use git for this directory then simply delete the `.git` file.

**[⬆ back to top](#overview)**

## Git Structure

Git breaks things up into three 'trees' which are all maintained by git.

**Working Directory** : This is your current **local** tree. This just holds what's in your repository. 

**Staging** : (Or sometimes known as _index_) is - as the name implies - a staging tree. This will hold all the recent changes you have selected to go into the next commit (more on that later).

**HEAD** : Basically, a reference that usually points to the latest _commit_ for the repository.

Moving from one tree to another is simple.
```
# You must first move files that you have changed to the staging area.
# To specify a single file,
$ git add <filename>

# Alternatively, you can add all files that you have updated, added, or remove by entering,
$ git add -A

# This will put all the changes you've staged into a new commit. HEAD will now point to this newest commit.
$ git commit -m "commit message"

# You can do this all in online with.
$ git commit -am "commit message"
```

There is a caveat to using `git commit -am "commit message"`, it will not pick up on brand new files or files that have been deleted since the last commit.
We personally recommend going through this workflow:

```
git add -A # add all changes to the repo.
git commit -m "commit message"` # creates a new commit with all the changes you made.
```

**[⬆ back to top](#overview)**

## Git logs

The `git log` command is a way to see all previous commits made to the repository (whether by you or someone else)

```
$ git log

commit cd62a7d33d8c20255ef4ba59da61ff21acbf903b
Author: black-shadows <abhisheksharma.0517@gmail.com>
Date:   Fri Apr 3 03:14:41 2015 -0400

    one more method

commit 7b1db82140dc678eb869c742f0479ccf86168da5
Author: rperryng <ryanperrynguyen@gmail.com>
Date:   Fri Apr 3 03:14:08 2015 -0400

    succesfull merges ?

commit bdc7ede1047a698955bd5b419de1ad9cada68b2c
Merge: 8bc63cf cb6ae5f
Author: black-shadows <abhisheksharma.0517@gmail.com>
Date:   Fri Apr 3 03:12:54 2015 -0400

    Merge branch 'master' into random-branch
```

The large assortment of numbers and letters right next to the word commit is the sha_key, it's a specific hexadecimal value that references that particular commit.

- The author line is simple, it's the user that made the commit

- The date line is self-explanatory

- and finally the commit message. The commit message helps you understand what work you did within that commit so make sure to make them as verbose as you can, especially if you are working with a team. 

There is one more thing that I should point out here. If the git log is large enough, git will open it in `vim`, an editor for the terminal. To exit the git log, simply press `esc`, then `:`, then `q` and hit enter.

But if you want cleaner more readable information, definitely try the following:
```
$ git log --oneline -5

70693a1 Merge branch 'master' into random-branch
9f4b039 conflict feature 2 on master
aa87d8a branch conflict feature
1bde9e5 added a conflict feature
6f1c4d9 fourth feature was added
```
where `-5` is an option that lets you specify the number of most recent commits you want to see.  (You can use these options together with the other ones listed below).

To see all the commits made by one author,
```
$ git log --author=black-shadows
```
To see all your merges (we will talk about what a merge is later),
```
$ git log --merges
```
To see the repo history in a visual branching format,
```
$ git log --graph
```
To see all the other ways of viewing git logs, you can check out the [documentation](http://git-scm.com/docs/git-log).

**[⬆ back to top](#overview)**

## Undo

One of the most compelling reasons to use Git is that you can roll back to a previous snapshot (commit) of the repository, in case you've made a mistake.
However, reverting back to a specific commit can be really confusing if you've never done it before. Git gives you several ways to do it, and depending on the situation, one way is easier than another.

First, you'll want to identify which commit you want to roll back to.  enter `git log --oneline` and select the first 5-6 digits of the sha_key for the commit you want to return to.
I will be using the sha_key of 184353d9 (you usually only need the first 6-7 digits of your commit).  as the commit key that we want to return to.

##### Go back and checkout
1. There are no changes that have not been committed.
2. You just want to go back to an older commit, but you don't want to delete all your newer commits.

```
$ git checkout 184353d9

# Or 

$ git checkout -b new_branch_name 184353d9
```

##### Delete everything and just start restart from chosen commit
1. There are no changes that have not been committed.
2. You made a mistake and just need to go back to that commit, erasing everything you have done since then.

```
$ git reset --hard  184353d9
```
##### Start over from head or master
1. You just made some changes to files for testing ( you do not want to commit ).
2. You have not committed your changes yet.

```
$ git reset --hard HEAD
```
Remember that HEAD is (almost always) a pointer to the latest commit on that branch.

##### Ctrl + Z

1. You have no idea what you did, no idea where you are and you just want to go back

- The reflog command is the ultimate safety net. It keeps track of everything you just did, from checking out new branches, to rebases, the reflog is essentially a way to move back through time.


```
$ git reflog

# after finding the place you want to go back to 

$ git reset --hard <sha_key>
```

##### Correcting small mistakes
1. You've already made your commit and you've noticed something small that *should* have been in that commit (usually grammar, stale debug statements or comments).

This will allow you to *add* the changes to that most recent commit, as if it was there all along!
```
$ git commit --amend --no-edit
```

It's important to note that if you've already pushed the commit before fixing your mistake, you won't be able to push the corrected commit. This is because the remote repo and the local repo have conflicting versions of the same commit.  If you've been working on a branch that *only* you have been working on, you can force the remote repository to accept the corrected commit.  **you should only do this if you know no one else has pulled the *non* corrected commit already**.  This will almost always be the case if you have been working on your own branch!
```
$ git push -f
```

**[⬆ back to top](#overview)**

## Branches

The Master branch is the branch that you start in and it's the branch that you should never work directly on. Anytime you want to make changes to the project, you should checkout a different branch. Once you have finished implementing said feature you can then merge your branch into master. This is great because it allows you to organize your features and keep a controlled working version of the app to compare with.

Branches are a great way to start implementing new features. When you start making a new feature, you first run `git pull` on the master branch to make sure you have all the latest code.

- You should never be getting a merge error when doing a `git pull`. If you find yourself in this situation that means that you made a few commits on the master branch by accident. Stop the merge and make sure you're on a clean tree, then do this:

  ```
  $ git checkout -b temp-changes
  $ git reset --hard origin/master
  ```
- All your changes that should not have been on master have been moved to a separate branch (temp-changes). The second line then looks at the remote directory and just sets your local version of the master branch to the same one that is on origin (origin is the name of the remote branch, usually hosted on GitHub).

To create a new branch:
```
$ git checkout -b new_branch_name
```
Branch names should be descriptive to what you are trying to do. Their names cannot contain any spaces and its most common to use either `-` or `_` to separate the words

```
$ git checkout -b getting-live-messages-from-websocket
```
To see which branch you are currently in:

```
$ git status

# Or 

$ git branch
```
To merge a branch once you are done. We will be merging the `getting-live-messages-from-websocket` branch _into_ master

```
$ git checkout master
$ git merge getting-live-messages-from-websocket
```
**[⬆ back to top](#overview)**

## Merging 

##### Merge 
```
$ git merge branch_name
```

The `git merge` command by itself just puts all the commits into master, as if the branch you made never existed.  We personally recommend using the `--no-ff` (no fast forward) flag.  This will create a commit just for the act of merging your commits.  It will also preserve the fact that those commits were made on a branch.  If you are going to use the `--no-ff` flag, I also recommend using the `--no-edit` flag with it as well.  This will automatically create the commit message for you (something like `Merge branch <branch_name>`)
```
$ git merge add-tests-for-app-version --no-ff --no-edit
```

* When merging, you are usually on the master branch and merge with your own branch

##### Rebase

* When rebasing, you are usually on the branch you are working on.
* Rebase right before you decide merge with master

```
$ git rebase master
```
_Why Rebase?_, It's a great to make a clean looking tree, it appears as if you never created a branch to begin with. Remember a rebase is simply shifting the commit that your branch branched off of, to be the HEAD of master.

**[⬆ back to top](#overview)**

## Tricks

### Stripspace

- Removes trailing whitespace
- Collapse New lines
- Adds new lines to end of file

  - Simply pass in the file that you want to strip

  ```bash
  $ git stripspace < text_file.txt
  ```

### Previous Branch

- Quickly go back to your last branch

  ```bash
  $ git checkout - 
  ```

### Clean Status

- Add `-sb` to get a cleaner `git status`

  ```bash
  $ git status -sb
  ```

### Auto Correct

- Set auto correct to true for Git commands

  ```bash
  $ git config --global help.autocorrect 1
  ```

- Results in:

  ```bash
  $ git comit -m "commit message"
  # WARNING: You called a Git command named 'comit', which does not exist.
  # Continuing under the assumption that you meant 'commit'
  # in 0.1 seconds automatically...
  ```

### Alias

- Add shortcuts to reduce your typing

  ```bash
  $ git config --global alias.alias_command git_command
  ```

Examples:

- Set `git stat` to `git status -sb`

  ```bash
  $ git config --global alias.stat 'status -sb'
  ```

- Combine functions with `&&`

  ```bash
  $ git config --global alias.ac '!git add -A  && git commit'
  ```
  - The commit messages needs to be entered in from the editor if using the above alias 

## Merge Conflicts

If you try and perform a merge, there is a chance that you will end up with a merge conflict. Before we go over how to solve these problems, an important thing to learn is how to back out of the current predicament

```
$ git merge --abort
# or 
$ git rebase --abort
```
To see which files contain merge conflicts (assuming you haven't backed out yet). Just run:

```
$ git status
```
The important thing to remember here is that you have final say as to how the merge conflict is handled. If a co-worker spent hours and days on a feature that conflicted with yours, You can simply overwrite all their hard work. ( But let's try our best not to be so selfish ;) ).

##### Edit Conflicts
* Happens when two users edit the same lines of a file.

After opening up the file with the conflict you should see

```
<<<<<<< HEAD
def function_one
=======
def function_two
>>>>>>> your_branch
```
`your_branch` is the name of the branch that you are merging, `HEAD` is the latest commit on the branch that you are merging with. Going back to our example, `HEAD` would be, and usually is, the _HEAD_ of the master branch

After correcting the conflict,
```
$ git add .
$ git commit -am "fixing merge conflicts"
```

* If you want to simply take the changes that are in `HEAD`

```
$ git checkout --theirs <file_name_that_has_merge_conflict>
```

* If you want to keep your own changes

```
$ git checkout --yours <file_name_that_has_merge_conflict>
```

##### Removed files conflict 
* One person modified the file, while another deleted the file

you actually have two choices here, delete the file, or keep the changes

1. Keeping the file with new changes

    Simply add the file back and commit. (let's say the README.md file was modified)

    ```
    $ git add README.md 
    $ git commit 
    ```

2. deleting the file and disregarding the changes

Simply remove the file and commit:

```
$ git rm REAMDE.md 
$ git commit
```

If you had a conflict in the middle of a rebase, after fixing your conflicts run:

```
$ git add .
$ git rebase --continue
```
**[⬆ back to top](#overview)**

## Example Workflow

Now that you've seen all the bits and pieces, it would probably be helpful to see what the workflow with all these different commands looks like.

This is the typical situation.  You're working on a project which is being tracked by git.  You want to begin adding a feature or fixing a bug.
Begin by checking out a new branch with a descriptive branch name.  For demo purposes, the branch name will be `fix-readme-grammar`.
```
$ git checkout -b fix-readme-grammar
```

after making your changes, review your changes by running
```
$ git status
```
and usually
```
$ git diff
```
This will allow you to do a last minute review of your changes before deciding to make a new commit

Once you're satisfied, add the files to the staging area
```
$ git add -A
```

Now, create your new commit
```
$ git commit -m "Restructured commit section.  Fix spelling mistakes for introductory paragraph."
```
Of course, you can always combine these by entering `git add -A && git commit -m "commit message"`

Now you'll want to push your changes to the remote repo.  Since it's a new branch, you'll have to tell the remote repo that you want it to start tracking this new branch as well.  You can set up remote tracking and push at the same time by entering
```
$ git push -u origin fix-readme-grammar
```
After your first push, you can simply use `git push` for future commits on this branch.

Once you've made enough changes, commits, and pushes that you're happy enough to merge it back into master, you'll want to head over to github (or whatever service you're using for your remote repo) to submit a pull request.  Once you've got the OK to merge it back in to master,
```
$ git checkout master
$ git pull
$ git merge fix-readme-grammar --no-ff --no-edit
```

Lastly, you'll want to delete the branches, first on your remote...
```
$ git push origin --delete fix-readme-grammar
```

...and then on your local machine
```
$ git branch -d fix-readme-grammar
```

**[⬆ back to top](#overview)**

## Remotes

We are nearing the GitHub section so it's time to introduce **Remotes**

- When you use `git init` you just started git version control on that local directory (and child directory). But everything is maintained in your local machine. The concept of a remote is to start keeping a central version of the repository online, usually on a service like Github.

- First you have to actually create the remote repository, which is very simple to do. Just go on github.com and click the `New Repository` icon the nav bar

- Github will give you all the needed instructions as to how we move our project into the remote repo 

- By default the name of your repo and all remote repos are set to **origin**. Note that you never have to change this if you don't want to (most people don't) 

##### Push

- To push a new branch onto the remote repo

  ```
  $ git push -u <remote\_repo_name> <branch_name>
  ```

- Or to make things a little nicer 

  ```
  $ git push -u origin HEAD
  ```
- After that, you can usually just use `git push` to push to the matching branch on remote (though you may to have tell git you want `git push` to only push to the matching branch on the remote `git config --global push.default simple`, more on this [here](http://stackoverflow.com/a/948397/3194316))

  ```
  $ git push 
  ```
- This will push the current branch that you are working on 

The `-u` is short for `--set-upstream`, which just means that if you ever want to `pull` the remote branch, you simply have to type 
`git pull` while you are currently checked out in the local branch.

**[⬆ back to top](#overview)**

## GitHub

Github is a website that anyone can access and a great way to work on projects with other people. You can also use Github to contribute to open source, a great way to help everyone!

## Creating a Git Repo

- Go to the top right of the page and click on the create new button. Then pick `New repository`. 

- pick the name of the repo, the name should be the name for the project that you are working on. For example the name of this repo is
**git-cheat-sheet**

- You'll want to initialize with a README.md file. The README.md is a file that you want other people to read before looking at your project
For example, what you are reading right now is a README.md file. If you want to learn about Markdown, which is how you can make things look cool, read here: https://help.github.com/articles/github-flavored-markdown/

- And that's all! You have just created your remote repository. If you have an existing projects, you can import that project to this repo. If this is just the beginning, you can clone the remote repo to your local machine. 

## Git Clone

- If you look at the right side of a git repo's main page, you will see its _git clone_ URL. Copy that link to your clipboard, either with just `cmd + c` or by clicking on the clipboard icon. Then go to the local directory you want to clone the project to and run:

```
$ git clone <clone_link>

# example

$ git clone https://github.com/black-shadows/git-cheat-sheet.git
```

## Reset

Go back to commit:
`git revert 073791e7dd71b90daa853b2c5acc2c925f02dbc6`

Soft reset (move HEAD only; neither staging nor working dir is changed):
`git reset --soft 073791e7dd71b90daa853b2c5acc2c925f02dbc6`

Undo latest commit: `git reset --soft HEAD~ `

Mixed reset (move HEAD and change staging to match repo; does not affect working dir):
`git reset --mixed 073791e7dd71b90daa853b2c5acc2c925f02dbc6`

Hard reset (move HEAD and change staging dir and working dir to match repo):
`git reset --hard 073791e7dd71b90daa853b2c5acc2c925f02dbc6`


## Update and Delete

Test-Delete untracked files:
`git clean -n`

Delete untracked files (not staging):
`git clean -f`

Unstage (undo adds):
`git reset HEAD index.html`

Update most recent commit (also update the commit message):
`git commit --amend -m "New Message"`


## Stash

Put in stash:
`git stash save "Message"`

Show stash:
`git stash list`

Show stash stats:
`git stash show stash@{0}`

Show stash changes:
`git stash show -p stash@{0}`

Use custom stash item and drop it:
`git stash pop stash@{0}`

Use custom stash item and do not drop it:
`git stash apply stash@{0}`

Delete custom stash item:
`git stash drop stash@{0}`

Delete complete stash:
`git stash clear`


## Gitignore

About: https://help.github.com/articles/ignoring-files

Useful templates: https://github.com/github/gitignore

Add or edit gitignore: 
`nano .gitignore`

Track empty dir: 
`touch dir/.gitkeep`


## Compare

Compare modified files:
`git diff`

Compare modified files and highlight changes only:
`git diff --color-words index.html`

Compare modified files within the staging area:
`git diff --staged`

Compare branches:
`git diff master..branchname`

Compare branches like above:
`git diff --color-words master..branchname^`

Compare commits:
`git diff 6eb715d`
`git diff 6eb715d..HEAD`
`git diff 6eb715d..537a09f`

Compare commits of file:
`git diff 6eb715d index.html`
`git diff 6eb715d..537a09f index.html`

Compare without caring about spaces:
`git diff -b 6eb715d..HEAD` or:
`git diff --ignore-space-change 6eb715d..HEAD`

Compare without caring about all spaces:
`git diff -w 6eb715d..HEAD` or:
`git diff --ignore-all-space 6eb715d..HEAD`

Useful comparings:
`git diff --stat --summary 6eb715d..HEAD`

Blame:
`git blame -L10,+1 index.html`


## Version Tags

Show all released versions:
`git tag`

Show all released versions with comments:
`git tag -l -n1`

Create release version:
`git tag v1.0.0`

Create release version with comment:
`git tag -a v1.0.0 -m 'Message'`

Checkout a specific release version:
`git checkout v1.0.0`


## Collaborate

Show remote:
`git remote`

Show remote details:
`git remote -v`

Add remote upstream from GitHub project:
`git remote add upstream https://github.com/user/project.git`

Add remote upstream from existing empty project on server:
`git remote add upstream ssh://root@123.123.123.123/path/to/repository/.git`

Fetch:
`git fetch upstream`

Fetch a custom branch:
`git fetch upstream branchname:local_branchname`

Merge fetched commits:
`git merge upstream/master`

Remove origin:
`git remote rm origin`

Show remote branches:
`git branch -r`

Show all branches:
`git branch -a`

Create and checkout branch from a remote branch:
`git checkout -b local_branchname upstream/remote_branchname`

Compare:
`git diff origin/master..master`

Push (set default with `-u`):
`git push -u origin master`

Push:
`git push origin master`

Force-Push:
`git push origin master --force

Pull:
`git pull`

Pull specific branch:
`git pull origin branchname`

Fetch a pull request on GitHub by its ID and create a new branch:
`git fetch upstream pull/ID/head:new-pr-branch`

Clone to localhost:
`git clone https://github.com/user/project.git` or:
`git clone ssh://user@domain.com/~/dir/.git`

Clone to localhost folder:
`git clone https://github.com/user/project.git ~/dir/folder`

Clone specific branch to localhost:
`git clone -b branchname https://github.com/user/project.git`

Delete remote branch (push nothing):
`git push origin :branchname` or:
`git push origin --delete branchname`


## Archive

Create a zip-archive: `git archive --format zip --output filename.zip master`

Export/write custom log to a file: `git log --author=sven --all > log.txt`


## Troubleshooting

Ignore files that have already been committed to a Git repository: http://stackoverflow.com/a/1139797/1815847


## Security

Hide Git on the web via `.htaccess`: `RedirectMatch 404 /\.git` 
(more info here: http://stackoverflow.com/a/17916515/1815847)


## Large File Storage

Website: https://git-lfs.github.com/

Install: `brew install git-lfs`

Track `*.psd` files: `git lfs track "*.psd"` (init, add, commit and push as written above)