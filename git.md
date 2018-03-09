## GUI
https://www.sourcetreeapp.com/

## checkout file/folders from remote branch
```
git checkout upstream/master -- folder/file
```

## discard unstaged changes in Git
Do a [Dry run first](https://stackoverflow.com/questions/15840009/undo-a-git-clean-command/15840063#15840063)!!!
```
git clean -n
git clean -df
git checkout -- .
```
git clean removes all untracked files (warning: while it won't delete ignored files mentioned directly in .gitignore, it may delete ignored files residing in folders) and git checkout clears all unstaged changes.

## remove files from git staging area
```
git reset HEAD -- .
```

## revert to a previous commit
```
git reset --soft HEAD@{1}
```

## reset (dangerous)
reset to a previous state and discard all changes
```
git reset --hard
git reset --hard f414f31
```
the commits after f414f31 will no longer be in the history of your master branch

## Checkout github pull requests locally
https://gist.github.com/piscisaureus/3342247


## The meaning of refs and refspecs
https://git.seveas.net/the-meaning-of-refs-and-refspecs.html

### show refs
```
git show-ref
```

### revert a git pull
```
git reflog
git reset --hard <hash found above>
```

### Git Checkout Remote Branch
```
git fetch origin
git checkout -b workingbranch origin/branchxyz
```
Or you can use:
```
git branch workingbranch origin/branchxyz
```
