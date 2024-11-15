# Git Tutorial for Beginners

This tutorial will guide you through the basic Git commands, from creating a repository to committing changes and connecting to a remote repository.

---

## Table of Contents

1. [Creating a Repository](#creating-a-repository)
2. [Staging and Committing Changes](#staging-and-committing-changes)
3. [Working with Branches (Brief Intro)](#working-with-branches)
4. [Connecting to a Remote Repository](#connecting-to-a-remote-repository)

---

## 1. Creating a Repository

A Git repository is where Git tracks the history of your code.

### Steps:

1. **Navigate to your project directory**:
   ```bash
   cd path/to/your/project
   ```

2. **Initialize Git**:
   ```bash
   git init
   ```
   This will create a `.git` directory that holds all the version history for the project.

3. **Check the repository status**:
   ```bash
   git status
   ```
   This command will show which files are staged for commit and if there are any untracked files.

---

## 2. Staging and Committing Changes

Git works in two stages: staging and committing.

### Steps:

1. **Add files to the staging area**:
   ```bash
   git add <file_name>
   ```
   To add all files:
   ```bash
   git add .
   ```
   This command stages changes for commit, telling Git which files you want to include in your next snapshot.

2. **Commit changes**:
   ```bash
   git commit -m "Describe your changes here"
   ```
   A commit is a snapshot of your changes. The message (`-m`) should be a brief description of what you've done.

---

## 3. Working with Branches

Branches in Git allow you to work on different versions of your code at the same time.

### Key commands:

1. **Create a new branch**:
   ```bash
   git branch <branch_name>
   ```

2. **Switch to a branch**:
   ```bash
   git checkout <branch_name>
   ```

3. **Create and switch to a new branch in one step**:
   ```bash
   git checkout -b <branch_name>
   ```

4. **View all branches**:
   ```bash
   git branch
   ```

5. **Merge a branch into the main branch**:
   First, switch to the main branch (usually called `main` or `master`):
   ```bash
   git checkout main
   ```
   Then merge the branch:
   ```bash
   git merge <branch_name>
   ```

---

## 4. Connecting to a Remote Repository

Remote repositories (like GitHub, GitLab, etc.) allow you to collaborate with others and store your code online.

### Steps:

1. **Add a remote repository**:
   ```bash
   git remote add origin <remote_repo_url>
   ```
   The `origin` is a shorthand name for the remote repository URL.

2. **Push changes to the remote**:
   ```bash
   git push -u origin main
   ```
   This pushes the code to the `main` branch of the remote repository.

3. **Pull changes from the remote**:
   ```bash
   git pull origin main
   ```

---

## Conclusion

In this tutorial you have learned the most important Git commands. To have a little help for your next Git Repos, create a list with the commands you learned. Include the syntax and _what_ those commands are used for.


## Additional Task

Create a git Repo for your API(s) from the first two parts and upload it to GitLab.
