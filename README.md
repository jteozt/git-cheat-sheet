#### Check for changes on remote origin
```shell
fetch from remote, reports how many commits behind my local is. (if Any)
git remote update
git status

bring my local up to date
git pull origin master
```

#### Detached Head 
```shell
To recover from your situation, you should create a branch that points to the commit currently pointed to by your detached HEAD:

git branch temp
git checkout temp
(these two commands can be abbreviated as git checkout -b temp)

This will reattach your HEAD to the new temp branch.

Next, you should compare the current commit (and its history) with the normal branch on which you expected to be working:

git log --graph --decorate --pretty=oneline --abbrev-commit master origin/master temp
git diff master temp
git diff origin/master temp
(You will probably want to experiment with the log options: add -p, leave off --pretty=… to see the whole log message, etc.)

If your new temp branch looks good, you may want to update (e.g.) master to point to it:

git branch -f master temp
git checkout master
(these two commands can be abbreviated as git checkout -B master temp)

You can then delete the temporary branch:

git branch -D temp

https://stackoverflow.com/questions/5772192/how-can-i-reconcile-detached-head-with-master-origin
```

#### Go one step back in history
```shell
git checkout @~1
```

#### Tag a commit
```shell
git tag <name> <commit id> 
```

#### Show commit changes
```shell
git show <commit-sha>
git show <tag name> 
```

#### Push master branch to origin
```shell
git push origin master
```

#### List all branches
```shell
git branch -a
git branch -av
```

#### List remote branches
```shell
git branch -r
```

#### Sync list of remote branches
```shell
git remote update
```

#### Checkout remote branch into local repository
```shell
git checkout -t -b <local-name> <remote-name>
```

#### Create a branch
```shell
git checkout -b <name>
```

#### Push local branch to remote
```shell
git push origin <remote-name>
```

#### Merge two commits
```shell
git rebase --interactive HEAD~2

pick   b76d157 b <older>
squash a931ac7 c <latest>
```

#### Merge two branches
```shell
git checkout <target>
git merge <source>
```

#### Merge two branches (no fast forward)
```shell
git merge --no-ff <source>
```

#### Merge two branches with squash
```shell
git checkout <target>
git merge --squash <source>
```

#### See what branches are merged into master
```shell
git branch -r --merged master
```

#### Ignore files globally
https://help.github.com/articles/ignoring-files

#### pull changes from the server + rebase (equivalent of git stash save && git pull && git stash pop && git push) + push
```shell
git pull --rebase origin master && git push
```

#### Set up git inet server
```shell
git daemon --base-path /home/git --verbose
```

#### Add remote origin
```shell
git remote add origin <url>
```

#### Tracking information between local branch and origin:
```shell
git branch --set-upstream-to=origin/master <local target branch>
```

#### Fix 'branch not tracking anything'
```shell
git config --add branch.master.remote origin
git config --add branch.master.merge refs/heads/master
```

#### Extract patch from a given file
```shell
git diff --patch-with-raw rev1 rev2 patched_file > diff_file
```

#### Diff with paging
```shell
GIT_PAGER='less -r' git dc
```

#### Apply a patch
```shell
git apply diff_file
```

#### Publish branch
```shell
git push origin <name>
```

#### Delete last commit 
```shell
git reset HEAD~ 
git reset --hard HEAD^
````

#### Delete remote branch
```shell
git push origin :<name>
```

#### Uncommit Commit
```shell
git reset HEAD^
```

#### Discard Uncommitted changes
```shell
git reset --hard
```

#### Discard Untracked files
```shell
git clean -n (to show what will be deleted)

git clean -fdx
-f - force
-d - directories too
-x - remove ignored files too ( don't use this if you don't want to remove ignored files)

```

#### Stash changes
```shell
git stash save 'name'
git stash save -u 'name'       // to stash untracked files without staging them.
```

#### Stash List
```shell
git stash list
```

#### Stash Pop
```shell
git stash pop <stash id>
```

#### Cherry-pick a commit
```shell
git cherry-pick -n <sha>
```

#### Revert commit
```shell
git revert -n <sha>
```

#### Reset HEAD to n commits back
```shell
git reset --hard HEAD~<n>
```

#### Squash N last commits
```shell
git rebase --interactive --autosquash HEAD~N
```

#### search git log commits
```shell
git log -S “free text”
```

#### remove file from history (can use 'git rm -rf…' to remove files recursively)
```shell
git filter-branch --index-filter 'git rm --cached --ignore-unmatch <path to file>' --prune-empty --tag-name-filter cat -- --all
git push origin master --force
rm -rf .git/refs/original/
git reflog expire --expire=now --all
git gc --prune=now
git gc --aggressive --prune=now
```

#### Prune history
```shell
git gc
git gc --aggressive
git prune
```

#### Checkout GitHub PR
```shell
git fetch origin pull/1234/head:local-branch-name
```

#### Convert long sha to short one
```shell
git rev-parse --short <sha>
```

#### My aliases
```shell
git config --global alias.aa "add --all"
git config --global alias.ai "add --interactive"
git config --global alias.b "branch"
git config --global alias.ba "branch -a"
git config --global alias.c "commit"
git config --global alias.ca "commit --amend"
git config --global alias.cf '!sh -c "git commit --fixup $@"'
git config --global alias.co "checkout"
git config --global alias.col '!sh -c "git checkout -b $@"'
git config --global alias.cor '!sh -c "git checkout --track -b $@ origin/$@"'
git config --global alias.cp "cherry-pick"
git config --global alias.cpa "cherry-pick --abort"
git config --global alias.cpc "cherry-pick --continue"
git config --global alias.cs '!sh -c "git commit --squash $@"'
git config --global alias.d "diff"
git config --global alias.dc "diff --cached"
git config --global alias.ds "diff --stat"
git config --global alias.dsc "diff --stat --cached"
git config --global alias.fpr '!sh -c "git fetch origin pull/$@/head:$@-pr"'
git config --global alias.l "log"
git config --global alias.lp "log --pretty=oneline"
git config --global alias.lf "log --follow"
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %Cblue<%an>%Creset' --abbrev-commit --date=relative --all"
git config --global alias.m "merge"
git config --global alias.mb "merge-base master HEAD"
git config --global alias.ms "merge --squash"
git config --global alias.pl "pull"
git config --global alias.ps "push"
git config --global alias.psc '!sh -c "git push --set-upstream origin \$(git rev-parse --abbrev-ref HEAD)"'
git config --global alias.psd '!sh -c "git push origin :\$(git rev-parse --abbrev-ref HEAD)"'
git config --global alias.psf "push --force-with-lease"
git config --global alias.r "reset HEAD"
git config --global alias.rb "rebase"
git config --global alias.rba "rebase --abort"
git config --global alias.rbc "rebase --continue"
git config --global alias.rbi "rebase --interactive --autosquash"
git config --global alias.rbm "rebase --interactive --autosquash origin/master"
git config --global alias.rh "reset --hard"
git config --global alias.rs "reset --soft"
git config --global alias.s "status"
git config --global alias.sh "show"
git config --global alias.shs "show --stat"
git config --global alias.st "stash"
```

#### Global git ignore
```shell
git config --global core.excludesfile ~/.gitignore
```

#### Global username & email
```shell
git config --global user.name "Jakub Pawlowicz"
git config --global user.email '<email>'
```

#### Local username & email
```shell
git config user.name "Jakub Pawlowicz"
git config user.email '<email>'
```

####
```shell
git config --global color.diff auto
git config --global color.status auto
git config --global color.branch auto
```

#### Branch name and merge status in bash prompt (should go to local or global bash profile)
```shell
function parse_git_dirty {
  [[ $(git status 2> /dev/null | tail -n1) != "nothing to commit, working directory clean" ]] && echo "*"
}
function parse_git_branch {
  git branch --no-color 2> /dev/null | sed -e '/^[^*]/d' -e "s/* \(.*\)/[\1$(parse_git_dirty)]/"
}
export PS1='\u@\h \[\033[0;36m\]\w \[\033[0;32m\]$(parse_git_branch)\[\033[0m\]$ '
```
