---
title: Workshop 5 - Distributed version control
---

**Answers to the goals are hidden as HTML comments.**

Cheat sheet:

- `git remote`
- `git fetch`
- `git pull`

Setup:

For this workshop, we need a remote repository to play around with.

Below are instructions for Gitlab (my favorite host), but feel free to use another host.

1. Go to http://gitlab.com and create an account if you don't already have one.
2. Log into your account.
3. Next, browse to: https://gitlab.com/windtrain/git
4. Click on the "Fork" button, next to the "star" button. This will fork the repository into your own namespace. Confirm by clicking your namespace.
5. The project should now be hosted within your namespace.
6. Clone your project withe the link shown in the middle. `git clone https://gitlab.com/<username>/git.git`

## Remotes

### Viewing and adding a remote

**Goal**: View your remotes

<pre style="display: none;">git remote -v
</pre>

**Goal**: Add a remote pointing to https://gitlab.com/windtrain/git

<pre style="display: none;">git remote add training https://gitlab.com/windtrain/git
git remote -v
</pre>

### Deleting a remote

**Goal**: Delete a remote

<pre style="display: none;">
git remote rm training
</pre>

## Fetching

Make sure you have cloned your repo. Next we will make an edit via the gitlab UI, so that your local copy is out of date.

Browse to: `https://gitlab.com/<username>/git/blob/master/README.md`

Next click the "edit" button on the right hand side. Add some text.

Scroll down, make sure you are committing to master, then press commit changes. You should see an updated version of the file.

### Fetch

First do a `git status` to see your current state. Note how it says "up-to-date". This is because you haven't told git to fetch any new commits yet.

**Goal**: Fetch the new commits from the remote origin. Your `git status` should report "Your branch is behind 'origin/master' by 1 commit"

<pre style="display: none;">
git fetch
```
or more verbosely
```
git fetch origin master
</pre>

## Copying commits into your local repository

We haven't yet copied the commits into our repository. We could merge the fetch in, but we will be investigating the `merge` command later.

**Goal**: Copy the new commits into your local repository. The status of your repository should show that it is now up to date with origin/master.

<pre style="display: none;">
git pull
```
or more verbosely
```
git pull origin master
</pre>

## Copying commits to the remote repository

Make a change to the `README.md` file again: `echo "more text" >> README.md`

Commit that change.

**Goal**: Copy the commit to the origin (you may need to enter your new user/pass at this point)

<pre style="display: none;">
git push
```
or more verbosely
```
git push origin master
</pre>

## Tagging commits

**Goal**: Tag your new commit as "v0.0.1" with an annotation of "my first tag". Copy that tag to the remote.

Then browse to `https://gitlab.com/<username>/git/tags`. Your tag should be visible.

<pre style="display: none;">
git tag v0.0.1 -m "My first tag"
git push --tags
</pre>
