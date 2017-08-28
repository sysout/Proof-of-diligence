## discard unstaged changes in Git
```
git clean -df
git checkout -- .
```
git clean removes all untracked files (warning: while it won't delete ignored files mentioned directly in .gitignore, it may delete ignored files residing in folders) and git checkout clears all unstaged changes.

## reset
reset to a previous state
```git reset --hard
```
Use the git-reflog command to find the SHA-1 of the previous state and then reset to it.

## Checkout github pull requests locally
https://gist.github.com/piscisaureus/3342247


## The meaning of refs and refspecs
https://git.seveas.net/the-meaning-of-refs-and-refspecs.html

### show refs
```
git show-ref
```
