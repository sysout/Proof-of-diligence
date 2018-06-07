## GUI
https://www.sourcetreeapp.com/

## git log
```
git log --graph --pretty=oneline
```

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

## [git index and git diff](http://alblue.bandlem.com/2011/10/git-tip-of-week-understanding-index.html)

```bash
# for unstaged changes
git diff filename
# for staged changes
git diff --cached
```

## reset (dangerous)
reset to a previous state and discard all changes
```
git reset --hard
git reset --hard f414f31
```
the commits after f414f31 will no longer be in the history of your master branch

## [git rebase](https://www.youtube.com/watch?v=TymF3DpidJ8)
```
git checkout somebranch
git log --oneline --all --decorate
git rebase master
git checkout master
git merge somebranch
```

## [Squashing multiple commits into a single one](https://www.youtube.com/watch?v=gXCkYkLQ3To)
```
git rebase -i HEAD~4
# Helpful hint: You can always edit your last commit message, before pushing, by using:
git commit --amend
```

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
