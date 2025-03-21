# Working with Remote Repositories and Collaboration

## Objective
- Simulate a collaborative workflow with remote repositories.

## Requirements
- Create a local repository and push it to a remote service (e.g., GitHub or GitLab).
- Create a feature branch, make commits, and push the branch to the remote.
- Open a Pull Request (or Merge Request) and perform a code review process.
- Merge the feature branch into the main branch on the remote and then pull the changes locally.

## Steps

### 1. Create a Local Repository
```bash
git init <project name>
git add .
git commit -m "Initial commit"
```

### 2. Connect to a Remote Repository
- Create a repository on GitHub.
- Link your local repository to the remote:
I am going to push the repsoitry i am using so far to remote.
```bash
git remote add origin https://github.com/HARISH6000/Testing.git
```
- Push your code to the remote:
```bash
git push -u origin master
```
```bash
Enumerating objects: 32, done.
Counting objects: 100% (32/32), done.
Delta compression using up to 20 threads
Compressing objects: 100% (21/21), done.
Writing objects: 100% (32/32), 2.80 KiB | 1.40 MiB/s, done.
Total 32 (delta 6), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (6/6), done.
To https://github.com/HARISH6000/Testing.git
 * [new branch]      master -> master
branch 'master' set up to track 'origin/master'.
```

### 3. Create and Push a Fix Branch
- Create a new branch for your fix:
```bash
git checkout -b fix
```
- Make changes, add them, and commit:
```bash
git add .
git commit -m "added test.js"
```
- Push the branch to the remote:
```bash
git push -u origin fix
```

### 4. Open a Pull Request
- Go to your GitHub repository.
- Go to `fix` branch and click on `Compare & pull request`.
- Add a title, description, and assign reviewers.

### 5. Perform Code Review and Merge
- Review the code for issues or improvements.
- After approval, merge the pull request into the master branch.

### 6. Pull the Latest Changes Locally
- Switch to the master branch and pull the latest updates:
```bash
git checkout master
git pull origin master
```
```bash
git log --graph --oneline --decorate --all
```
```bash
*   7ad00f3 (HEAD -> master, origin/master) Merge branch 'master' of https://github.com/HARISH6000/Testing
|\  
| *   1497989 Merge pull request #1 from HARISH6000/fix
| |\  
* | | 9850409 (fix) added test.js
| |/  
|/|   
* | 8372d8c (origin/fix) added test.js
* | a423de2 (branch3) Testing pre-commit
* | df65fda Commit on branch4
| | * cf0ebc4 (branch4) Commit on branch4
| |/  
|/|   
* | 80db78a Commit on branch3
|/  
* ba47018 file1 version 5
*   60fd98a (branch1) Resolved merge conflict
|\  
| * 8581224 (branch2) Branch2 change
* | 9979990 Branch1 change
|/  
* e4d1f9e file version 4
* aa5ea1a Revert "made a commit with error in file1.txt"
* 7131951 made a commit with error in file1.txt
* 6639a64 edited file1.txt
* 6fda4c4 Add .gitignore and track necessary files
* 0c5fe1b (feature-branch) updated file1 in feature-branch
```
