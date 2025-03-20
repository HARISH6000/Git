# Stashing Changes for Context Switching

## Objective
- Learn how to use Git stash to save uncommitted work temporarily.

## Requirements
- Make changes in your working directory without committing.
- Use `git stash` to save these changes.
- Switch branches, perform some work, then return and reapply your stashed changes with `git stash pop`.
- Optionally, demonstrate how to view and manage multiple stashes using `git stash list` and `git stash drop`.

## Steps

### 1. Make Some Changes
Create or modify files without committing them.

### 2. Stash the Changes
Save your uncommitted changes using:
```bash
git stash
```
```
Saved working directory and index state WIP on master: ba47018 file1 version 5
```
This will store your changes and revert your working directory to the last commit.

### 3. Switch to Another Branch
```bash
git checkout branch1
```
Make any necessary changes on the new branch.

### 4. Return and Apply Stashed Changes
Once you're ready to return to your original work, switch back and apply the stash:
```bash
git checkout master
git stash pop
```
```bash
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   file1.txt

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (7ef8f1ca45f6400dc73b6b3a30cc7afe473367ae)
```
- `git stash pop` applies the stashed changes and removes the stash.
- If you want to keep the stash for later, use `git stash apply` instead.

### 5. Manage Stashes
Lets create few staches with messages
```bash
git stash save <stash message>
```
- View all stashes:
```bash
git stash list
```
```bash
stash@{0}: On master: WIP: stash 3
stash@{1}: On master: WIP: stash 2
stash@{2}: On master: WIP: stash 1
```
- Apply a specific stash using its identifier:
```bash
git stash apply stash@{1}
```
```bash
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   file1.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
- Delete a specific stash:
```bash
git stash drop stash@{1}
```
```bash
Dropped stash@{1} (80a6b86c28de068859ad6d387407fdd761f0b5ed)
```
```bash
git stash list

stash@{0}: On master: WIP: stash 3
stash@{1}: On master: WIP: stash 1
```
- Clear all stashes:
```bash
git stash clear
```
