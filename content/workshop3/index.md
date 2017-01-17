---
title: Workshop 3 - Working with the repository
---

**Answers to the goals are hidden as HTML comments.**

Cheat sheet:

- `git status`
- `git add`
- `git mv`
- `git rm`
- `git log`

Setup:

```
cd ~/training
git clone https://gitlab.com/windtrain/git.git
cd ~/training/git
```

Note: To restore the repository back to its original state, you can delete the directory and re-clone, or you can use the reset command (discussed later) `git reset --hard origin/master`.

## Repository state

Files are either untracked, unstaged, staged or tracked.

**Goal**: Show the state of your repository.

<!--
```
git status
```
-->

### Add a file

Create a new file:

```
touch newfile
```

**Goal**: Add a new file to the repository

<!--
```
git add newfile
git status
```
-->

**Goal**: Simplify the output with the `-s` or `--short` parameter.

<!--
```
git status -s
```
-->

### Modifying a file and add all changes

Add a line to the readme, then stage the changes.

```
echo "hello git" > README.md
```

**Goal**: Add all files to staging.

<!--
```
git add *
git status -s
```
-->

### Only add specific files

```
touch fileA.md
touch fileB.md
touch another.md
touch fileC.txt
```

**Goal**: Only add the markdown (.md) files named "file..." so that your repo looks like:

```
$ git status -s
A  fileA.md
A  fileB.md
?? another.md
?? fileC.txt
...
```

<!--
```
git add file*.md
```
-->

### Removing a file

**Goal**: Remove the `README.md` file

<!--
```
rm README.md
git add .
```

or

```
git rm README.md
```
-->

### Move a file

**Goal**: Move the `README.md` (or another file) file to `NEW.md`

<!--
```
mv README.md NEW.md
git add .
```

or

```
git mv README.md NEW.md
```
-->

## Commits

Make a change to the repository:

```
touch newfile
echo "new text" > README.md
```

### Add a commit

**Goal**: Stage and commit these files to the repository. The status should look like

`Your branch is ahead of 'origin/master' by 1 commits.`

<!--
```
git add .
git commit -m "New files"
```
-->

### Inspect the commit log

**Goal**: Inspect the log to see who made the last commit (clue: it was you :-) )

<!--
```
git log
```
-->

### Pretty log

**Goal**: Show a pretty graph based log

Remember that acronym, A DOG?

<!--
```
git log --all --decorate --oneline --graph
```
-->

### Search for a commit

**Goal**: Search for all commits that have happened today.

<!--
Simplest to just type yesterday's date, but this is automated.

Alpine:
```
git log --after=$(date -d "@$(($(date +%s) - 86400))" +"%Y-%m-%d")
```

OSX:
```
git log --after=$(date -v -1d '+%m-%d-%y')
```
-->
