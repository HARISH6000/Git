# Undoing Changes and Reverting Commits

## Objective
- Experiment with undoing changes in your working directory and commits.

## Requirements
- Modify a tracked file and use `git checkout -- <file>` (or `git restore`) to undo changes.
- Make a commit, then use `git revert` or `git reset` to see how you can undo a commit safely.
- Explain the differences between these approaches.

## Steps
I am going to use the Repository from last task to perform the given tasks. it has the following commit history
```bash
commit 6639a644ecdf5b691787a6a3e0e6c0a76e26b45e (HEAD -> master)
Author: Harish G <harishgovind6000@gmail.com>
Date:   Wed Mar 19 10:27:12 2025 +0530

    edited file1.txt

commit 6fda4c41333069fc356091eb8a3e4a3b2541e038
Author: Harish G <harishgovind6000@gmail.com>
Date:   Wed Mar 19 07:48:01 2025 +0530

    Add .gitignore and track necessary files

commit 0c5fe1b745650c2b4bc38d3c7048f56fccf6752e (feature-branch)
Author: Harish G <harishgovind6000@gmail.com>
Date:   Wed Mar 19 06:27:17 2025 +0530

    updated file1 in feature-branch

commit ab5af6d3ac029390b7dea9e4429973ac902e5d54
Author: Harish G <harishgovind6000@gmail.com>
Date:   Wed Mar 19 06:18:32 2025 +0530

    initial commit with basic files
```
### 1. Undo Unstaged Changes
If you've made changes to a file but haven't staged it yet, you can discard those changes using:
```bash
git restore <file>
```
This reverts the file back to its last committed state.

### 2. Undo Staged Changes
If you've staged changes using `git add` but haven't committed yet, you can unstage them using:
```bash
git restore --staged <file>
```
then you can discard changes using
```bash
git restore <file>
```

### 3. Reverting a Commit
Lets say i made a commit with an error
```bash
commit 713195186bde2634e441c709db94cd32a0432d77 (HEAD -> master)
Author: Harish G <harishgovind6000@gmail.com>
Date:   Wed Mar 19 10:35:07 2025 +0530

    made a commit with error in file1.txt
```
If you want to undo this commit without losing history, use `git revert`:
```bash
git revert <commit-hash>
```
This creates a new commit that undoes the changes from the specified commit.
```bash
[master aa5ea1a] Revert "made a commit with error in file1.txt"
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### 4. Resetting a Commit
Lets make another two commits,
```bash
git log --pretty=oneline
```
```bash
d3b091442616e0acda9b4d8b5f2bf452454b71d4 (HEAD -> master) file version 5
e4d1f9e5b82a714839e1d9de9d0c890d3230d749 file version 4
aa5ea1a64bf40968a18ed5a224108ab1b68f1fb7 Revert "made a commit with error in file1.txt"
713195186bde2634e441c709db94cd32a0432d77 made a commit with error in file1.txt
6639a644ecdf5b691787a6a3e0e6c0a76e26b45e edited file1.txt
6fda4c41333069fc356091eb8a3e4a3b2541e038 Add .gitignore and track necessary files
0c5fe1b745650c2b4bc38d3c7048f56fccf6752e (feature-branch) updated file1 in feature-branch
ab5af6d3ac029390b7dea9e4429973ac902e5d54 initial commit with basic files
```
If you want to remove a commit and potentially lose changes, use `git reset`. Options include:
- `git reset --soft <commit-hash>` → Moves HEAD to the specified commit, keeping changes staged.
- `git reset --mixed <commit-hash>` → Moves HEAD to the specified commit, unstaging changes.
- `git reset --hard <commit-hash>` → Moves HEAD to the specified commit and deletes all changes.
I did an hard reset
```bash
git reset --hard e4d1f9e5b82a714839e1d9de9d0c890d3230d749
```
```bash
HEAD is now at e4d1f9e file version 4
```
if we check the log,
```bash
e4d1f9e5b82a714839e1d9de9d0c890d3230d749 (HEAD -> master) file version 4
aa5ea1a64bf40968a18ed5a224108ab1b68f1fb7 Revert "made a commit with error in file1.txt"
713195186bde2634e441c709db94cd32a0432d77 made a commit with error in file1.txt
6639a644ecdf5b691787a6a3e0e6c0a76e26b45e edited file1.txt
6fda4c41333069fc356091eb8a3e4a3b2541e038 Add .gitignore and track necessary files
0c5fe1b745650c2b4bc38d3c7048f56fccf6752e (feature-branch) updated file1 in feature-branch
ab5af6d3ac029390b7dea9e4429973ac902e5d54 initial commit with basic files
```
it moved HEAD to the specified commit and deleted all the changes.

### Differences
- **git revert**: It is safe for shared repositories since it creates a new commit to undo changes.
- **git reset**: It is used for fixing mistakes in local repo before pushing, as it modifies commit history.