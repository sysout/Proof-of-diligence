## discard unstaged changes in Git
```
git clean -df
git checkout -- .
```
git clean removes all untracked files (warning: while it won't delete ignored files mentioned directly in .gitignore, it may delete ignored files residing in folders) and git checkout clears all unstaged changes.
