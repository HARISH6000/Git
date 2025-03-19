# Simulating and Resolving Merge Conflicts

## Objective
- Create a scenario that produces a merge conflict and resolve it.

## Requirements
- Create two branches from the same commit.
- Modify the same line(s) of code in a common file in both branches.
- Attempt to merge the branches, observe the conflict, and resolve it manually.
- Use `git status` and `git diff` to identify and resolve the conflicting changes.

## Steps

### 1. Create Two Branches
```bash
git branch branch1
git branch branch2
```
Both branches now originate from the same commit.

### 2. Make Conflicting Changes
switch to branch1
```bash
git checkout branch1
```
In branch1 add a file called conflict.txt with content
```bash
This is branch1
```
```bash
git add conflict.txt
git commit -m "Branch1 change"
```
```bash
[branch1 9979990] Branch1 change
 1 file changed, 1 insertion(+)
 create mode 100644 conflict.txt
```
Now, switch to branch2 and make a conflicting change:
```bash
git checkout branch2
```
add conflict.txt file again with the following content
```bash
This is branch2
```
```bash
git add conflict.txt
git commit -m "Branch2 change"
```
```bash
[branch2 8581224] Branch2 change
 1 file changed, 1 insertion(+)
 create mode 100644 conflict.txt
```
Now the branches look like this
```bash
git log --graph --oneline --decorate --all

* 8581224 (HEAD -> branch2) Branch2 change
| * 9979990 (branch1) Branch1 change
|/
* e4d1f9e (master) file version 4
* aa5ea1a Revert "made a commit with error in file1.txt"
* 7131951 made a commit with error in file1.txt
* 6639a64 edited file1.txt
* 6fda4c4 Add .gitignore and track necessary files
* 0c5fe1b (feature-branch) updated file1 in feature-branch
* ab5af6d initial commit with basic files
```

### 3. Attempt to Merge and Create a Conflict
```bash
git checkout branch1
git merge branch2
```
You will see a merge conflict message because both branches modified the same line.
```bash
Auto-merging conflict.txt
CONFLICT (add/add): Merge conflict in conflict.txt
Automatic merge failed; fix conflicts and then commit the result.
```

### 4. View and Resolve the Conflict
Check the conflict using:
```bash
git status
```
```bash
On branch branch1
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both added:      conflict.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
```bash
git diff
```
```bash
diff --cc conflict.txt
index a1c79d2,3c2af44..0000000
--- a/conflict.txt
+++ b/conflict.txt
@@@ -1,1 -1,1 +1,5 @@@
- This is branch1
 -This is branch2
++<<<<<<< HEAD
++This is branch1
++=======
++This is branch2
++>>>>>>> branch2
```
Open the conflicted file. You will see markers, Manually edit the file to keep the desired changes.

### 5. Finalize the Merge
```bash
git add conflict.txt
git commit -m "Resolved merge conflict"
```
```bash
[branch1 60fd98a] Resolved merge conflict
```
now we can check the status and graph
```bash
git status
```
```bash
On branch branch1
nothing to commit, working tree clean
```
```bash
git log --graph --oneline --decorate --all
```
```bash
*   60fd98a (HEAD -> branch1) Resolved merge conflict
|\
| * 8581224 (branch2) Branch2 change
* | 9979990 Branch1 change
|/
* e4d1f9e (master) file version 4
* aa5ea1a Revert "made a commit with error in file1.txt"
* 7131951 made a commit with error in file1.txt
* 6639a64 edited file1.txt
* 6fda4c4 Add .gitignore and track necessary files
* 0c5fe1b (feature-branch) updated file1 in feature-branch
* ab5af6d initial commit with basic files
```