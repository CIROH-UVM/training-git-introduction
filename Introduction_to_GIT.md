# Agenda
[The Case for Code Versioning](#the-case-for-code-versioning)

[Introducing GIT](#introducing-git)

[Getting GIT](getting-git)

[Basic GIT Commands](basic-git-commands)

[Getting a Repository](#getting-a-repository)

[Configuring GIT](#configuring-git)

[Making and Saving Changes](#making-and-saving-changes)

[Ignoring Files](#ignoring-files)

[Sharing Changes](#sharing-changes)

[Content History](#content-history)

[Branch Management](#branch-management)

[Resolving Merge Conflicts](#resolving-conflicts)

[Undoing That Thing You Just Did](#undoing-your-work)

## The Case for Code Versioning
* Versioning Saves Snapshots Of Edited Code, With The Ability To Move Forward And Backward Along A History
  * Save Your Brilliant Idea For The Whole Team To Use
  * Undo That Unfortunate Choice
* The Timeline May Include Forks And Mergers Of Experiments Tried And Abandoned Or Propagated 
  * Try Three Things, Test Them In Parallel, And Keep The One You Like Best
  * Change Your Mind And Pick The Other Option That Was Almost As Fast, But Is More Flexible
* A Single Developer May Benefit From Code Versioning, But A Team Of Developers That Are Jointly Modifying A Project Is More Likely To Not Succeed Without Code Versioning 
  * That Elegant Algorithm Your Teammate Wrote Can't Be Used Until You Share Your Updated Data Prep Step
  * The Person Testing The Code You Shared Last Week Needs A Quick Fix, But You Are Halfway Through A New, Major Update

## Introducing GIT
* Global Information Tracker – Aka GIT 
* GIT Is A Utility/App/Program To Facilitate Managing Code Versions
* First Created In 2005 As Part Of Linux Development Environment
* Support Multiple Local Repositories That Can Be Conditionally Synchronized With Each Other
* Each Developer Can Have Their Own Copy Of Everything, And Can Share Updates With All, Or Some Of, The Other Developers As They Are Ready For Use

## Getting GIT
* Popular Toolset With Huge Web Presence
  * https://github.com/git-guides/install-git
  * https://git-scm.com/downloads
  * https://www.uvm.edu/news/story/git-version-control-system-uvm
    * https://gitlab.uvm.edu/

## Basic GIT Commands
* Git clone : To Create A Local Repository Connected To A Remote Copy 
  * Often Points To A Central Copy Referenced As The "Origin"
  * `git clone Git@gitlab.Uvm.Edu:vermont-epscor/Cyberinfrastructure.Git Cyberinf`
* Git status : To Assess The State Of A Local Repository 
  * List Any Untracked Files Or Tracked Files With Uncommitted Changes
* Git add : To Add A New Or Updated File To The List Of Updates To Be Tracked 
  * Adds A File To The List To Be Included In The Next Commit
* Git rm : To Stage The Removal Of Any Files For The Next Commit
* Git commit : To Formally Commit A Set Of Updates To A New Snapshot Of Content 
  * Bundle All Pending Added Changes Into A Retrievable Snapshot
* Git log: Display The History Of Updates Made To The Repository
* Git push : Share An Updated Local Repository To Update The Central Copy
* Git pull : Update A Local Repository With Updates From The Central Copy


## Getting a Repository
* git clone
  * used to create a local copy of a remote repository
  * registers the remote repository as the origin of the copy
  * need to know the URL where the remote content is served from (i.e. our github area)
  * `git clone  git@github.com:scottebemeup/ciroh-ua_website.git`

* git pull
  * used to obtain the updates present at the remote origin
  * will merge new content into your current local working copy
  * `git pull`
  * `git pull origin main`

* git fetch
  * used to get content from a remote repository
  * does not merge content into your local working copy

## Configuring GIT
* $HOME/.gitconfig
  * a user specific file to make settings common across repositories
  * editor selection
  * merge tool specification
  * diff tool specification
* `git config --list`   to list all your configuration settings

> #### List of config contents from a Linux Install
> ```
> [seturnbu@epscor gitdemo]$ git config --list
> user.name=Scott Turnbull
> user.email=seturnbu@uvm.edu
> diff.tool=meld
> merge.tool=meld
> difftool.meld.cmd=meld "$LOCAL" "$REMOTE"
> mergetool.meld.cmd=meld "$LOCAL" "$BASE" "$REMOTE" --output "$MERGED"
> core.repositoryformatversion=0
> core.filemode=true
> core.bare=false
> core.logallrefupdates=true
> remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
> remote.origin.url=git@gitlab.uvm.edu:vermont-epscor/cyberinfrastructure.git
> branch.master.remote=origin
> branch.master.merge=refs/heads/main
> ```


* Updating the config - 2 Options
  * edit the files in a wise and knowing manner
  * use commands to set specific configuration options
      * `git config --global user.name "John Doe"`  to set your user name
      * `git config --global user.email johndoe@uvm.edu`  
      * `git config --global core.editor emacs`   to set the default editor to emacs
      * `git config --global diff.tool meld`  to set the default diff tool to meld
      * `git config --global difftool.meld.cmd 'meld "$LOCAL" "$REMOTE"'`



> #### Contents of a Windows OS .gitconfig has different path syntax
>```
>$ cat $HOME/.gitconfig
>[user]
>	email = seturnbu@uvm.edu
>	name = Scott Turnbull
>[gui]
>[push]
>	default = simple
>[gui]
>	recentrepo = C:/Users/scott.turnbull/Documents/EPSCoR/git/newrnetabm
>	recentrepo = C:/Users/scott.turnbull/Documents/EPSCoR/git/lutabm
>[diff]
>	tool = meld
>[difftool "meld"]
>	cmd = \"C:/Program Files (x86)/Meld/Meld.exe\" \"$LOCAL\" \"$REMOTE\"
>[merge]
>	tool = meld
>[mergetool "meld"]
>	cmd = \"C:/Program Files (x86)/Meld/Meld.exe\" --auto-merge \"$LOCAL\" \"$BASE\" \"$REMOTE\" ---output \"$MERGED\" --label \"MERGE (REMOTE BASE MY)\"
>```


* repository/.git/config
  * repository specific configuration
    * specification of the remote repository
    * branch names
  * is dynamically updated by GIT as you work with your repository
  * can be used to create a repository specific setting that differs from global file

> #### Contents of Repository Specific .git/config
>```
> $ cat config
> [core]
>         repositoryformatversion = 0
>         filemode = false
>         bare = false
>         logallrefupdates = true
>         symlinks = false
>         ignorecase = true
> [remote "origin"]
>         url = git@gitlab.uvm.edu:vermont-epscor/cyberinfrastructure.git
>         fetch = +refs/heads/*:refs/remotes/origin/*
> [branch "master"]
>         remote = origin
>         merge = refs/heads/master
>```



## Making and Saving Changes

* They're "just" files. Change content as you always have

![alt text]( 
https://git-scm.com/book/en/v2/images/areas.png
"Local Directory WorkFlow")


* `git status`  to list the files that have local changes
  * lists changes to be committed (staged)
  * lists changes not staged for commit
  * identifies new files (staged or unstaged)
  * lists tracked files that have been deleted

> #### Status of repository with staged new file and unstaged modification
> ```
> $ git status
> On branch master
> Your branch is up-to-date with 'origin/master'.
> Changes to be committed:
>   (use "git reset HEAD <file>..." to unstage)
> 
>     new file:   README
> 
> Changes not staged for commit:
>   (use "git add <file>..." to update what will be committed)
>   (use "git checkout -- <file>..." to discard changes in working directory)
> 
>     modified:   CONTRIBUTING.md
> ```


![alt text](https://git-scm.com/book/en/v2/images/lifecycle.png "File Workflow")

* git add - the simple use
  * `git add myfile.txt` to stage a single file
  * `git add myfile1.txt myfile2.txt` to stage a list of files
  * `git add myfile*.txt` to stage files using wildcarding
  * `git add .`  stages new and modified in the current directory and below, without deleted
  * `git add -u` stages modified and deleted, without new
  * `git add --all` to stage everything in all dirs that isn't already tracked or staged (CAUTION!)

* git add - much more subtlety and power lurks under many options 
    * `git add [--verbose | -v] [--dry-run | -n] [--force | -f] [--interactive | -i] [--patch | -p]
	  [--edit | -e] [--[no-]all | --[no-]ignore-removal | [--update | -u]]
	  [--intent-to-add | -N] [--refresh] [--ignore-errors] [--ignore-missing]
	  [--chmod=(+|-)x] [--] [<pathspec>…​]`
    * Note that file content is staged at the time of the `git add`
    * A file modified, staged, then re-modified, shows as staged and not staged

> #### Status with a staged modified file that has a 2nd modification
> ```
> $ git status
> On branch master
> Your branch is up-to-date with 'origin/master'.
> Changes to be committed:
>   (use "git reset HEAD <file>..." to unstage)
> 
>     new file:   README
>     modified:   CONTRIBUTING.md
> 
> Changes not staged for commit:
>   (use "git add <file>..." to update what will be committed)
>   (use "git checkout -- <file>..." to discard changes in working directory)
> 
>     modified:   CONTRIBUTING.md
> ```

* `git rm`  to stage the removal of any files for the next commit

* git commit
  * `git commit -m "meaningful message"`   commits all staged content to the local repository
  * `git commit -a -m "helpful description"`  automatically does an add for modified tracked files
  * `git commit --amend`   add staged information to the previous commit

## Ignoring Files
* sometimes there are files in a repository directory that we may not want git to process
  * files derived from source (*.o, *.pyc, *.jar)
  * files autosaved from editors (*.bak)
  * data files
  * output files
* Update contents of the file `.gitignore`
  * specify name patterns of files that git should ignore
      * *.pyc
      * *.[oa]
      * *.bak
  * specify directory names to exclude
      * datadir


## Sharing Changes
* git push 
  * `git push origin master`
  * `git push --dry-run`   will prepare the push, generate any messages, but make no changes
* git pull
  * Updates Your Local Repository Will All The Changes From The Remote Copy
* git rebase
	* Updates Your Local Branch With Updates From Parent Branch
	* Conflicts Merged Locally Prior To Any Push Of Of Your New Content 


## Content History
* git log
	* Scrollable History of All Commits to a Repository
* git tag
  * `git tag`   list of all defined tags
  * `git tag -l "partial*"`  list tags matching a wildcarded name
  * `git tag -a thetag -m "Good description"`  create a new annotated tag
  * `git tag -a goodtagname 9fceb02`   to tag a previous commit identifier
  * `git push origin --tags`   pushes all tags to the origin, alternatively they can be named
* git diff
	* Lists the Changes Between Current Committed Copy and Your Staging Area
* git show
  * `git show thetag`   list information about a tag
* git checkout
  * `git checkout thebranch`  to switch context to a branch
  * `git checkout thetag`   to switch context to a tagged commit (beware the HEADless context!)


## Branch Management
* git branch
  * `git branch`   list the current branches
  * `git branch testing` create a branch
* git checkout
  * `git checkout main`  selects main branch
  * `git checkout testing` selects testing branch
  * `git checkout -b newbranch` create and checkout a new branch
* currently selected branch pointed to by **HEAD**

![alt text](https://git-scm.com/book/en/v2/images/advance-testing.png "Straight Branch Example")

![alt text](https://git-scm.com/book/en/v2/images/advance-master.png "Split Branch Example")

## Resolving Conflicts
*  `git diff`
  * displays differences between two copies of content
*  `git merge`
  * attempts to reconcile differing content copies into a merged result
  * invoked under the covers of a `git pull`
* `git merge <branch_name>` merge updates made to "branch_name" to the current branch
* `git mergetool`  launches a graphical merge tool to guide the resolution of conflicts

## Undoing Your Work
* `git stash`  moves local edits to a side directory to avoid a merge conflict
* `git checkout` undoes unstaged edits
* git reset HEAD 
  * unstages a file
* git revert
  * undoes a commit
* `git merge --abort` undoes a merge conflict by by unspooling commits it made

## Resources

GIT Documentation - https://git-scm.com/docs
* https://git-scm.com/book/en/v2/Getting-Started-Git-Basics
* https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository

https://dev.to/exwhyzed/how-to-git-a-complete-beginners-guide-1h85
https://dev.to/lydiahallie/cs-visualized-useful-git-commands-37p1  
https://dev.to/milu_franz/git-explained-the-basics-igc

Software Carpentry Version Control Lecture and Labs
https://swcarpentry.github.io/git-novice/

* Introduction to Version control
  * https://swcarpentry.github.io/git-novice/01-basics/
* Setting up GIT
  * https://swcarpentry.github.io/git-novice/02-setup/
* Collaboration using GIT
  * https://swcarpentry.github.io/git-novice/08-collab/
* Ignoring Files
  * https://swcarpentry.github.io/git-novice/06-ignore/
* Resolving Conflicts
  * https://swcarpentry.github.io/git-novice/09-conflict/
* History
  * https://swcarpentry.github.io/git-novice/05-history/

