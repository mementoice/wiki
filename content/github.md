---
title: GitHub
tags:
  - tools/collaboration
  - explanation/contrast
  - explanation/analogy
---

GitHub is a web platform for hosting Git repositories and collaborating on software. It is built on top of [[Git]], not a replacement for it: Git stores the history, GitHub adds a shared home, a web interface, and collaboration tools.

## Git vs GitHub

|                          | Git                                               | GitHub                             |
| ------------------------ | ------------------------------------------------- | ---------------------------------- |
| What it is               | Version control system                            | Hosting and collaboration platform |
| Where it runs            | Locally on your machine                           | On the web (github.com)            |
| Made by                  | Open source community (originally Linus Torvalds) | GitHub, Inc. (owned by Microsoft)  |
| Needed to use the other? | No                                                | Yes — GitHub hosts Git repos       |

A useful analogy: Git is the engine and the notebook; GitHub is the shared library where copies are kept and discussed.

## What GitHub adds

- **Remote hosting** — a reliable copy of your repo at a URL such as `github.com/user/repo`.
- **Pull requests (PRs)** — propose a branch, review the diff, discuss, and merge through the web UI.
- **Issues** — track bugs, tasks, and feature ideas.
- **Actions** — CI/CD workflows defined in `.github/workflows`, run on pushes and PRs.
- **Pages** — free static site hosting straight from a repo.
- **Releases, wikis, projects, code review, permissions** — team workflow features.

## Typical workflow

```bash
# 1. Get the code
git clone https://github.com/user/repo.git
cd repo

# 2. Create a branch for your work
git switch -c fix/typo

# 3. Make changes and commit
git add .
git commit -m "Fix typo in README"

# 4. Push the branch to GitHub
git push -u origin fix/typo
```

Then open a **pull request** on GitHub from `fix/typo` into `main`. Reviewers comment, checks may run, and once approved the branch is merged.

## Collaboration model

1. **Fork** (for repos you cannot push to) or **branch** (for repos you can).
2. Commit changes on your branch.
3. Open a PR, describe the change, and link related issues (`Closes #12`).
4. CI runs; reviewers request changes or approve.
5. Merge, then delete the branch.

## Authentication

GitHub no longer accepts account passwords over HTTPS for Git operations. Use one of:

- **SSH keys** — generate with `ssh-keygen`, add the public key under Settings → SSH keys, then clone with `git@github.com:user/repo.git`.
- **Personal access token (PAT)** — fine-grained token used as the password for HTTPS.
- **GitHub CLI (`gh auth login`)** — configures credentials for you.

## Hosted alternatives

GitHub is not the only option; GitLab, Bitbucket, Codeberg, and self-hosted Forgejo/Gitea offer similar features. Because they all speak Git, you can move a repository between them without losing history.
