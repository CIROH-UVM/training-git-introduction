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