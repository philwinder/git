# Workshop 4 - Making mistakes

**Answers to the goals are hidden as HTML comments.**

Cheat sheet:

- `git reset`
- `.gitignore`
- `git clean`

Setup:

```
cd ~/training
git clone https://gitlab.com/windtrain/git.git
cd ~/training/git
```

## Resetting

### HEAD

**Goal**: View the location of the pointer `HEAD`

<!--
```
git status -b
```

OR

```
cat .git/HEAD
```
-->

### Remove from staging

```
touch new1 new2 new3
git add *
```

**Goal**: Remove the file `new1` from staging

<!--
```
git reset new1
```
--->

**Goal**: Remove all files from staging

<!--
```
git reset
```
-->

### Remove from staging and delete

```
touch new1 new2 new3
git add *
```

**Goal**: Remove all files from staging and delete.

<!--
```
git reset --hard
```
-->

### Moving the HEAD pointer

**Goal**: Move the HEAD pointer to the commit `c7b1f76`.

<!--
```
git reset c7b1f76
```
-->

## Ignoreing files

Create the test files:

```
mkdir logs
touch rubbish.yml good.xml logs/rubbish.xml
```

### Ignore file types

**Goal**: Ignore all xml files. So that the status looks like:

```
git status -s --untracked-files=all
?? rubbish.yml
```

<!--
```
echo *.xml > .gitignore
```
-->

### Ignore named files

**Goal**: Ignore all files named rubbish. . So that the status looks like:

```
git status -s --untracked-files=all
?? good.xml
```

### Ignore files in a directory

**Goal**: Ignore all files in the directory logs. So that the status looks like:

```
git status -s --untracked-files=all
?? good.xml
?? rubbish.yml
```

<!--
```
echo logs/ > .gitignore
```
-->

## Cleaning the repository

Create the files:

```
mkdir test ; touch fileA test/fileB fileC
```

### Dry run a clean

**Goal**: Run a dry run on a clean.

<!--
```
git clean -n
```
-->

### Perform a clean 1

**Goal**: Perform a clean on files within the current directory.

<!--
```
git clean -f
```
-->

### Perform a clean 2

**Goal**: Perform a clean on all files in the repo.

<!--
```
git clean -fd
```
-->
