# Cherry-Picking Commits Between Branches

## Objective
- Selectively apply a commit from one branch to another using cherry-pick.

## Requirements
- Create two branches with distinct commits.
- Identify a commit on one branch that you want to apply to the other.
- Use `git cherry-pick <commit-hash>` to apply the commit and handle any conflicts if they arise.
- Verify the commit history to ensure the cherry-picked commit is present.

## Steps

### 1. Create Two Branches
Create two branches with separate commits.
```bash
git checkout -b branch3
git add file1.txt
git commit -m "Commit on branch3"
```
```bash
[branch3 80db78a] Commit on branch3
 1 file changed, 1 insertion(+), 1 deletion(-)
```
```bash
git checkout -b branch4
git add file2.txt
git commit -m "Commit on branch4"
```
```bash
[branch4 cf0ebc4] Commit on branch4
 1 file changed, 2 insertions(+), 1 deletion(-)
```

### 2. Identify the Commit to Cherry-Pick
List commits using:
```bash
git log --graph --oneline --decorate --all
```
```
* cf0ebc4 (HEAD -> branch4) Commit on branch4
* 80db78a (branch3) Commit on branch3
* ba47018 (master) file1 version 5
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
* ab5af6d initial commit with basic files
```

Copy the commit hash of the desired commit from `branch4`.

### 3. Switch to the Target Branch
```bash
git checkout branch3
```

### 4. Perform Cherry-Pick
Apply the commit from `branch4` using its hash:
```bash
git cherry-pick <commit-hash>
```
```bash
[branch3 df65fda] Commit on branch4
 Date: Wed Mar 19 15:26:25 2025 +0530
 1 file changed, 2 insertions(+), 1 deletion(-)
```

### 5. Handle Conflicts (If Any)
- If conflicts occur, Git will pause the cherry-pick.
- Use `git status` to check the conflicting files.
- Resolve conflicts by manually editing files.
- Mark conflicts as resolved using:
```bash
git add <file>
git cherry-pick --continue
```

### 6. Verify the Cherry-Pick
Ensure the commit is applied by checking the log:
```bash
git log --oneline
```
```bash
df65fda (HEAD -> branch3) Commit on branch4
80db78a Commit on branch3
ba47018 (master) file1 version 5
60fd98a (branch1) Resolved merge conflict
8581224 (branch2) Branch2 change
9979990 Branch1 change
e4d1f9e file version 4
aa5ea1a Revert "made a commit with error in file1.txt"
7131951 made a commit with error in file1.txt
6639a64 edited file1.txt
6fda4c4 Add .gitignore and track necessary files
0c5fe1b (feature-branch) updated file1 in feature-branch
ab5af6d initial commit with basic files
```

Cherry-picking is useful when you want to apply specific changes without merging entire branches.
