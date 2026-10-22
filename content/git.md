---
title: Git
tags:
  - tools/version-control
  - explanation/first-principles
  - explanation/analogy
---

Git is a free, open-source **distributed version control system**. It records the history of a project as a series of snapshots, so you can see what changed, when, and why, and return to any earlier state.

Git runs entirely on your own machine. There is no central server required; a remote copy (such as one on [[GitHub]]) is just another place the same repository can live.

## Core ideas

- **Repository (repo)** — the project plus its full history, stored in the hidden `.git` folder.
- **Commit** — a saved snapshot with a message, author, timestamp, and a pointer to its parent commit. History is a chain of commits.
- **Working tree** — the files you currently see and edit.
- **Staging area (index)** — the set of changes you have marked for the next commit.
- **Branch** — a movable label pointing at a commit. The default is usually `main`.
- **Remote** — a named URL to another copy of the repo, typically `origin`.

The everyday cycle is:

```
work on files  ->  git add  ->  git commit  ->  git push
```

## The three states

A file moves between three places:

1. **Modified** in the working tree.
2. **Staged** after `git add`, ready to be committed.
3. **Committed** once `git commit` writes the snapshot into history.

`git status` shows which state each change is in.

## Common commands

```bash
# Set up identity (once per machine)
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# Start or copy a repository
git init                      # create a new repo in the current folder
git clone <url>               # copy an existing repo

# Inspect
git status                    # what changed, what is staged
git log --oneline --graph     # compact history
git diff                      # unstaged changes
git diff --staged             # staged changes

# Record changes
git add <file>                # stage a file (git add . for everything)
git commit -m "Message"       # commit the staged snapshot

# Branches
git branch                    # list branches
git switch -c feature         # create and switch to a branch
git switch main               # switch back
git merge feature             # merge a branch into the current one

# Remotes
git remote add origin <url>
git pull                      # fetch + merge changes from the remote
git push -u origin main       # upload a branch and track it
```

## Why it matters

- **Safety** — every commit is a restore point; mistakes can be undone.
- **Collaboration** — many people can work in parallel on branches and merge results.
- **Attribution and context** — the log explains why code looks the way it does.
- **Branches are cheap** — experimenting costs almost nothing.

## Mental model

Think of Git as a graph of commits. A branch is just a pointer into that graph, and `HEAD` is the pointer to your current branch. Merging joins two lines of history. This is why almost every Git operation can be understood as "move a pointer" or "add a node to the graph".

Next: [[GitHub]], the most common place to host Git repositories.
