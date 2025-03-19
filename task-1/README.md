# Initialize, Commit, and Branch Basics

## Objective
- Initialize a new Git repository.
- Create a few files and commit them.
- Create a new branch, make changes, and merge it back to the main branch.

## Prerequisites
- Git installed on your system.

## Steps

### 1. Initialize a New Repository
```bash
cd path/to/your/folder
git init
```
This creates a new Git repository in your directory.
```bash
Initialized empty Git repository in C:/Presidio/PreInternshipTraining/Testing/.git/
```

### 2. Create and Commit Files
I have created two Text files (file1.txt and file2.txt) both consisting of "<filename> version 1" as their content.
```bash
git add .
git commit -m "Initial commit with basic files"
```
This stages the changes in the file and git commit captures a snapshot of the staged changes and saves them to your Git repository's history. It acts like a checkpoint.
```bash
[master (root-commit) ab5af6d] initial commit with basic files
 2 files changed, 2 insertions(+)
 create mode 100644 file1.txt
 create mode 100644 file2.txt
```

### 3. Create a New Branch
```bash
git branch feature-branch
git checkout feature-branch
```
git branch creates a new branch and git checkout helps switch to that branch
```bash
Switched to branch 'feature-branch'
```
Make your changes in the new branch( changed the content of file1 to "file1 version 2"):
```bash
git add .
git commit -m "updated file1 in feature-branch"
```
```bash
[feature-branch 0c5fe1b] updated file1 in feature-branch
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### 4. Merge Changes into Main Branch
```bash
git checkout master
git merge feature-branch
```
Using git checkout master, we switch back to master branch and git merge combines changes from one branch into another.
```bash
Switched to branch 'master'

Updating ab5af6d..0c5fe1b
Fast-forward
 file1.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

