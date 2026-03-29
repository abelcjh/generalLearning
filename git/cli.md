# how to merge commits from remote
## always start with
```bash
git status
```
check if any commit differences

then
## if no merge conflict
```bash
git pull origin main
```
nano opens, just type a merge commit message, Ctrl + O, Enter, Ctrl + X
then same thing git add git commit git push


## when there are merge conflicts
```bash
git fetch # update pc new commits in remote
git restore -p --source=origin/main  -- <file-name> # merge code by patch, through prompts
```
then same thing, git add git commit git push

pull and restore same function, just that restore go patch by patch