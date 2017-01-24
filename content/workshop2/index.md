---
title: Workshop 2 - Creating and cloning repositories
---

**Answers to the goals are hidden as HTML comments.**

Cheat sheet:

- `git init`
- `git clone`
- `diff`

## Create a repository

```
cd ~
mkdir -p training/temp
cd training/temp
```

**Goal**: Initialise a git repository in this directory.

Inspect the created repository with: `ls -la .git`

<pre style="display: none;">
git init
</pre>

## Clone a repository

Cloning makes a full copy of a remote repository. Depending on the access rights of the repository, you may be asked for a username and password. The repo below is public.

It is also possible to setup ssh keys to communicate with a repository.

**Goal**: Clone the repository `https://gitlab.com/windtrain/git.git` into `~/training`.

<pre style="display: none;">
cd ~/training
git clone https://gitlab.com/windtrain/git.git
</pre>

## Clone an existing repository

We can clone any git repository, even one on our own machine!

```
cd ~/training
git clone git my_new_git
```

Let's do a diff to see what is different about the repo:

```
diff -r git my_new_git
```

If you look carefully, you'll notice that the "remote origin" is different. (More on remotes later)

Also, the index has changed to point towards files that are now on different paths.


## Configuring the author

Before making any changes to a repository, you must set the username and email address. This will be stored as meta data along with any changes you make.

```
git config user.name "Phil Winder"
git config user.email "phil@winderresearch.com"
```
