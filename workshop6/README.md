# Workshop 6 - Branches, merges, reverting and submodules

<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>

<a href="#" onclick="$('div').show(); return false;">Click here to show answers</a>

(Reload this page to hide answers)

Cheat sheet:

- `git branch`
- `git branch`

## Branches

### Create a branch

**Goal**: Create a branch. Show that your branch has been created.

<div style="display: none;">

```
$ git branch mybranch
$ git branch
```

</div>

### Viewing a branch split

**Goal**: Create a file on both the master and your new branch. The log should look like:

```
* 95f2b37 (HEAD -> mybranch) mybranch file
| * 39d4b50 (master) master commit
|/
* 6ae0ce5 (origin/master, origin/HEAD) Finished Workshop 5 - Distributed VCS.
```

<div style="display: none;">

```
$ git checkout master ; git branch mybranch
$ touch masterfile ; git add . ; git commit -m "master commit"
$ git checkout mybranch
$ touch branchfile ; git add . ; git commit -m "mybranch file"
$ git log --all --decorate --oneline --graph
```

</div>

## Merging

### Merge the branches just made

**Goal**: Merge your new branch into master. The resultant log should look similar to:

```
*   17f9e39 (HEAD -> master) Merge branch 'mybranch'
|\
| * e663c1e (mybranch) mybranch file
* | c6c3bfb master commit
|/
* 6ae0ce5 (origin/master, origin/HEAD) Finished Workshop 5 - Distributed VCS.
```

<div style="display: none;">

```
$ git checkout master
$ git merge mybranch
$ git log --all --decorate --oneline --graph
```

</div>

### Fixing a merge conflict

**Goal**: Create two branches. Edit the same file. Merge both into master. The result should look similar to:

```
*   6329425 (HEAD -> master) Merge branch 'dave'
|\
| * cc7e912 (dave) new title
* | 6e78399 (bob) new content
|/
* 6ae0ce5 (origin/master, origin/HEAD) Finished Workshop 5 - Distributed VCS.
```

**Tips**

You can always abort a merge to start again! ;-)

A diff might help you see the differences between branches

<div style="display: none;">

For example. Don't worry about using the same method to write the files.

To abort:

```
$ git merge --abort
```

To diff:

```
$ git diff
```

```
$ git branch bob ; git branch dave
$ git checkout dave
$ sed -i "1s/.*/# New Title/" README.md ; git add . ; git commit -m "new title"
$ git checkout bob
$ echo "new content" > README.md; git add . ; git commit -m "new content"
$ git checkout master
$ git merge bob
$ git merge dave
$ ## Fix merge conflicts
$ git add .
$ git commit
$ git log --all --decorate --oneline --graph
```

</div>

## Altering the previous commit

**Goal**: Add a commit, then fix it by altering the last commit.

<div style="display: none;">

```
$ echo "I can has cheezburger" > newfile ; git add . ; git commit -m "cheez"
$ git diff HEAD~
$ git log -2 --oneline
$ echo "Could I have a cheeseburger?" > newfile ; git add .
$ git commit --amend
$ git diff HEAD~
$ git log -2 --oneline
```

</div>

## Rebasing commits

Imagine you're working on a feature branch. Someone has committed their changes into master and you'd rather not have the merge commit showing.

**Goal**: Rebase your branch onto the new HEAD of master. Your last two commits should start similar to:

```
* 92ac790 (HEAD -> mybranch) hi hi
| * 8a7183e (master) newfile on master
|/
* 6ae0ce5 (origin/master, origin/HEAD) Finished Workshop 5 - Distributed VCS.
```

And end up looking like:

```
* 9416fce (HEAD -> mybranch) hi hi
* 8a7183e (master) newfile on master
```

<div style="display: none;">

```
$ git branch mybranch
$ touch newfile ; git add .
$ git commit -m "newfile on master"
$ git checkout mybranch
$ touch another file
$ git add . ; git commit -m "hi hi"
$ git log --all --decorate --oneline --graph
$ git rebase master
$ git log --all --decorate --oneline --graph
```

</div>


## Relative links

**Goal**: Write a command that is able to alter the commit messages of the last two commits.

<div style="display: none;">

```
$ git rebase -i HEAD~~
```

</div>

## Submodules

Imagine you have a shared library that another part of your business has developed. You want to add it to your code, but it isn't packaged anywhere.

**Goal**: Add another project as a submodule. You should be able to show that:

```
$ cat .gitmodules
[submodule "shared_module"]
    path = shared_module
    url = /shared
```

<div style="display: none;">

```
$ mkdir /shared ; cd /shared ; git init ; touch shared_file ;\
    git add . ; git commit -m "Shared file"
$ mkdir /myapp ; cd /myapp ; git init ; echo "My app" > README.md ;\
    git add . ; git commit -m "New app!"
$ git submodule add /shared shared_module  ## More likely to be a url
$ ls shared_module/
$ git commit -m "Added shared module"
$ cat .gitmodules
```

</div>

### Initialising

Imagine that another developer wants to clone your repo.

**Goal**: Clone your repo and pull down the submodules.


<div style="display: none;">

```
$ git clone /myapp /daves-app ; cd /daves-app
$ git submodule update --init --recursive
```

</div>

### Updates from the remote

Imagine that someone has updated the shared library.

**Goal**: Pull all updates from the shared repo and commit the changes.

<div style="display: none;">

```
$ cd /shared ; touch fire ; git add . ; git commit -m "Add fire"
$ cd /my-other-app/shared_module
$ git fetch
$ git checkout master
$ git pull
$ cd .. ; git status -s
$ git commit -a -m "Updated module"
$ git log --decorate --graph --oneline -U0 --submodule | grep -E '^[*| /\\]+([0-9a-f]{7} |Submodule |> |$)'
```

</div>
