Git Commands
============

### Getting & Creating Projects

| Command | Description |
| ------- | ----------- |
| `git init` | Initialize a local Git repository |
| `git clone ssh://git@github.com/[username]/[repository-name].git` | Create a local copy of a remote repository |

### Basic Snapshotting

| Command | Description |
| ------- | ----------- |
| `git status` | Check status |
| `git add [file-name.txt]` | Add a file to the staging area |
| `git add -A` | Add all new and changed files to the staging area |
| `git commit -m "[commit message]"` | Commit changes |
| `git rm -r [file-name.txt]` | Remove a file (or folder) |
| `git reset head --hard` | Resets local repo to last commit/head - will lose all the changes |
| `git reset --soft HEAD~` | Resets local repo's current (n) commit to n-1 commit - without losing the nth committed changes |
| `git stash` | To store current changes without commiting |
| `git pop` | To bring back the stashed changes |
| `git clean -df` | To delete unwanted untracked files |
| `git checkout -` | To move to previous branch after checking out new branch |

### Branching & Merging

| Command | Description |
| ------- | ----------- |
| `git branch` | List branches (the asterisk denotes the current branch) |
| `git clone --branch 11.5 --shallow-since=3m https://github.com/MariaDB/server.git mariadb-serverh` | This will make a clone that only tracks branch 11.5 and no other branches. Additionally this uses the shallow clone feature to fetch commit history only for the past 3 months instead of the entire history (which in this example otherwise would be 20+ years). |
| `git branch -a` | List all branches (local and remote) |
| `git branch [branch name]` | Create a new branch |
| `git branch -d [branch name]` | Delete a branch |
| `git push origin --delete [branch name]` | Delete a remote branch |
| `git checkout -b [branch name]` | Create a new branch and switch to it |
| `git checkout -b [branch name] origin/[branch name]` | Clone a remote branch and switch to it |
| `git branch -m [old branch name] [new branch name]` | Rename a local branch |
| `git checkout [branch name]` | Switch to a branch |
| `git checkout -` | Switch to the branch last checked out |
| `git checkout -- [file-name.txt]` | Discard changes to a file |
| `git merge [branch name]` | Merge a branch into the active branch |
| `git merge [source branch] [target branch]` | Merge a branch into a target branch |
| `git stash` | Stash changes in a dirty working directory |
| `git stash clear` | Remove all stashed entries |
| `git reset --hard origin/master` | To override local git with that of the remote. This will reset everything to match the remote |

### Sharing & Updating Projects

| Command | Description |
| ------- | ----------- |
| `git config --local fetch.prune true` | Removes and cleans up repo, deletes branchs which are also removed/deleted from the remote repos |
| `git push origin [branch name]` | Push a branch to your remote repository |
| `git push -u origin [branch name]` | Push changes to remote repository (and remember the branch) |
| `git push` | Push changes to remote repository (remembered branch) |
| `git push origin --delete [branch name]` | Delete a remote branch |
| `git pull` | Update local repository to the newest commit |
| `git pull origin [branch name]` | Pull changes from remote repository |
| `git remote add origin ssh://git@github.com/[username]/[repository-name].git` | Add a remote repository |
| `git remote set-url origin ssh://git@github.com/[username]/[repository-name].git` | Set a repository's origin branch to SSH |
| `git remote update` | will fetch all remotes and make sure you have all the latest git commits made since the last time you worked with the repository |

### Inspection & Comparison

| Command | Description |
| ------- | ----------- |
| `git log` | View changes |
| `git log --summary` | View changes (detailed) |
| `git log --oneline` | View changes (briefly) |
| `git diff [source branch] [target branch]` | Preview changes before merging |
| `git log --graph --oneline --decorate` | To log commits in a graph like form |

### Remove Git

| Command | Description |
| ------- | ----------- |
| `rm -rf .git` | Removes GIT from current working repo |

### Git Shortcuts

| Command | Description |
| ------- | ----------- |
| `git commit -am"Your commit message"` | Instead of git add . & git commit -m"Your commit message" |
| `git config --global alias.<<Your shortcut here>> "<<git command here>>"` | Adds a custom command. For Example: `git config --global alias.ac "commit -am"`, sets "git ac" as git commit -am. | 
| `git commit --amend -m"<<Your commit message>>"` | Will updated the last commit message |
| `git push origin YOURBranch --force` | Will override the remote repo with local repo |
| `git revert --no-commit 0d1d7fc3..HEAD -> git commit` | Revert to a previous published commit |

### Replace Git History with new Author

| Command | Description |
| ------- | ----------- |
| `git filter-branch -f --env-filter " GIT_AUTHOR_NAME='WorkWithAfridi' GIT_AUTHOR_EMAIL='afridi.khondakar@gmail.com' GIT_COMMITTER_NAME='WorkWithAfridi' GIT_COMMITTER_EMAIL='afridi.khondakar@gmail.com' " HEAD` | Run the script to replace past commit's author history with new author |

 ```
git filter-branch -f --commit-filter '
    if [ "$GIT_AUTHOR_NAME" = "old_username" ] && [ "$GIT_AUTHOR_EMAIL" = "old_email" ]; then
        GIT_AUTHOR_NAME="WorkWithAfridi"
        GIT_AUTHOR_EMAIL="afridi.khondakar@gmail.com"
        GIT_COMMITTER_NAME="WorkWithAfridi"
        GIT_COMMITTER_EMAIL="afridi.khondakar@gmail.com"
    fi
    git commit-tree "$@"
' HEAD 
```
- Run the script to replace certain users commit's author history with new author, remember to change the old_username & old_email properties |
 
