# Comprehensive Workflow with Forced Pushes and Recovery

## Objective
- Simulate an advanced Git scenario that includes forced pushes, recovering lost commits, and a multi-branch workflow using the existing repository.

## Requirements
- Create additional branches representing features, bug fixes, or releases.
- Simulate a scenario where a forced push (`git push --force`) is required (e.g., after rewriting history with an interactive rebase).
- Use `git reflog` to locate and recover lost commits after a mistaken force push.
- Document each step, explaining how and why forced pushes should be handled with care, and how `git reflog` can be a lifesaver.
- Discuss best practices for collaborating with teams when rewriting history and using force pushes.

## Steps

### 1. Create New Branches
- Create additional branches to simulate the scenario:
```bash
git checkout -b new-feature-branch
git checkout -b new-bugfix-branch
```

### 2. Make Changes and Commit
- On `new-feature-branch`, add a new feature:
```bash
git add feature.txt
git commit -m "Add new feature"
```
```bash
Linting passed. Proceeding with commit.
[new-feature-branch 451f39f] Add new feature
 1 file changed, 1 insertion(+)
 create mode 100644 feature.txt
```
- On `new-bugfix-branch`, simulate a bug fix:
```bash
git add bugfix.txt
git commit -m "Apply bug fix"
```
```bash
Linting passed. Proceeding with commit.
[new-bugfix-branch 6f0a4b9] Apply bug fix
 1 file changed, 1 insertion(+)
 create mode 100644 bugfix.txt
```

### 3. Perform an Interactive Rebase
- Rebase the last two commits interactively to edit or combine them:
```bash
git checkout new-feature-branch
git rebase -i HEAD~2
```
```bash
[detached HEAD 1ce0c4e] added test.js
 Date: Thu Mar 20 13:07:26 2025 +0530
 2 files changed, 3 insertions(+), 2 deletions(-)
 create mode 100644 feature.txt
Successfully rebased and updated refs/heads/new-feature-branch.
```
```bash
git push origin new-feature-branch
```
To simulate a force push, make another new commit in `new-feature-branch` and do a rebase to squah the last commit with previous one. 

### 4. Force Push After Rewriting History
- Since the history has been rewritten, a forced push is required:
```bash
git push origin new-feature-branch --force
```
```bash
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 20 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (4/4), 382 bytes | 382.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/HARISH6000/Testing.git
 + 1ce0c4e...6e6de69 new-feature-branch -> new-feature-branch (forced update)
```

### 5. Recover Lost Commits Using `git reflog`
- If commits are lost after a force push, use `git reflog` to view the commit history:
```bash
git reflog
```
```bash
6e6de69 (HEAD -> new-feature-branch, origin/new-feature-branch) HEAD@{0}: rebase (finish): returning to refs/heads/new-feature-branch
6e6de69 (HEAD -> new-feature-branch, origin/new-feature-branch) HEAD@{1}: rebase (squash): added test.js
1ce0c4e HEAD@{2}: rebase (start): checkout HEAD~2
cf46e84 HEAD@{3}: commit: Altered feature
1ce0c4e HEAD@{4}: rebase (finish): returning to refs/heads/new-feature-branch
1ce0c4e HEAD@{5}: rebase (squash): added test.js
9850409 (fix) HEAD@{6}: rebase (start): checkout HEAD~2
ce484b0 HEAD@{7}: rebase (finish): returning to refs/heads/new-feature-branch
ce484b0 HEAD@{8}: rebase (pick): Add new feature
```
- Identify the commit hash and create a new branch to recover the lost commit:
```bash
git checkout -b recovery-branch ce484b0
```
```bash
git log --graph --oneline --decorate --all

* 6e6de69 (origin/new-feature-branch, new-feature-branch) added test.js
| * ce484b0 (HEAD -> recovery-branch) Add new feature
| | * 6f0a4b9 (new-bugfix-branch) Apply bug fix
| | * 7ad00f3 (origin/master, master) Merge branch 'master' of https://github.com/HARISH6000/Testing
| |/|
| | *   1497989 Merge pull request #1 from HARISH6000/fix
| | |\
| |_|/
|/| |
| * | 9850409 (fix) added test.js
|/ /
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
```
