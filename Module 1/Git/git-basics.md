# Git & GitHub Resources

## Cheat Sheet

- [GitHub Cheat Sheet](https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf)

## Git Basic Commands
### Create Repositories

- Creates a new local repository with the specified name.
````
  $ git init [project-name]
````
- Downloads a project and its entire version history.
````
$ git clone [url]
````

### Make Changes
- Lists all new or modified files to be commited.
````
$ git status
````
- Snapshots the file in preparation for versioning (stages a file).
````
$ git add [file]
````
- Unstages the file, but preserve its contents.
````
$ git reset [file]
````
- Records file snapshots permanently in version history.
````
$ git commit -m "[descriptive message]"
````

### Synchronize Changes
- Combines bookmark’s branch into current local branch.
````
$ git merge [bookmark]/[branch]
````
- Uploads all local branch commits to GitHub.
````
$ git push [alias] [branch]
````
- Downloads bookmark history and incorporates changes.
````
$ git pull
````

### Review History
- Lists version history for the current branch.
```
$ git log
```

### Redo Commits
- Undoes all commits afer [commit], preserving changes locally.
````
$ git reset [commit]
````
- Discards all history and changes back to the specified commit.
````
$ git reset --hard [commit]
````

### Group Changes

- Lists all local branches in the current repository.
````
$ git branch
````
- Creates a new branch.
````
$ git branch [branch-name]
````
- Switches to the specified branch and updates the working directory.
```
$ git checkout [branch-name]
```
- Creates a new branch, switches to it and updates the working directory.
```
$ git checkout -b [branch-name]
```
- Combines the specified branch’s history into the current branch.
```
$ git merge [branch]
```
- Deletes the specified branch.
````
$ git branch -d [branch-name]
```
