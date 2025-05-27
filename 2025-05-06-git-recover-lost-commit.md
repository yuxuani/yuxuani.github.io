---
layout: post
title: How to Recover a Lost Commit and Merge a Branch in Git
description: Don't panic when you lose a commit accidentally.
date: 2025-05-06
tags: [git, github, git reflog, git reset, commit]
categories:
- Version Control
---
We all make mistakes sometimes. If you've accidentally lost a commit (for example, by using `git reset --hard HEAD~1`), don't panic! You can recover it by checking it out to a new branch. Here’s how to recover it and merge your changes back into the main branch.

## Recover a Lost Commit
- If you know the commit hash: 

    You can easily check out the commit and create a new branch:

    ```bash
    git checkout <commit-hash>
    git switch -c <new-branch-name>
    ```

    Replace `<commit-hash> ` with the actual commit hash (e.g., `def5678`) and `<new-branch-name>` with the name you want for the new branch. This will check out the commit and create a new branch from it.

- If you don’t know the commit hash:   
    Use `git reflog` to find the commit hash:

    ```bash
    git reflog
    ```

    The output will show a list of recent actions in your repository, including commits and resets. You’ll see something like this:

    ```bash
    abc1234 HEAD@{0}: reset: moving to HEAD~1
    def5678 HEAD@{1}: commit: Your last commit message
    ```

    Look for the commit you want to recover, then do the same as above.

## Create and Merge a New Branch
Once your commit is back, create and work on a new branch:

- Switch to the main branch:

    ```bash
    git checkout main
    ```

- Merge the new branch into main:

    ```bash
    git merge <new-branch-name>
    ```

- If there are conflicts, resolve them, then commit the changes:

    ```bash
    git add <conflicted-file>
    git commit
    ```

- Push the changes (if using a remote):

    ```bash
    git push origin main
    ```

## Conclusion
Git makes it easy to recover lost commits and manage branches. With a few commands, you can get back on track and continue your work .

If you found this guide helpful or have any questions, feel free to leave a comment below. :)