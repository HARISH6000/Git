# Interactive Rebasing for Clean Commit History

## Objective
- Use interactive rebase to tidy up your commit history.

## Requirements
- Create a series of commits (some with minor changes or typos in commit messages).
- Run `git rebase -i HEAD~n` (with `n` representing the number of commits) to squash, reorder, and edit commit messages.
- Explain how squashing helps in cleaning up commit history before merging into a main branch.

## Steps

### 1. Create Sample Commits
Make multiple commits to simulate a scenario for interactive rebasing.
```bash
git add file1.txt
git commit -m "file1 version 5"

git add file1.txt
git commit -m "file1 version 5 - mino changes"


git add file1.txt
git commit -m "file1 version 5 - minor changes"
```
```bash
* 0b78d30 (HEAD -> master) file1 version 5 - minor changes
* 941d754 file1 version 5 - mino changes
* f33942b file1 version 5
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

### 2. Start Interactive Rebase
Run the following command to start an interactive rebase for the last 3 commits:
```bash
git rebase -i HEAD~3
```

### 3. Choose Actions During Rebase
You'll see a list of commits like this in your editor:
```
pick f33942b file1 version 5
pick c327a5a file1 version 5 - mino changes
pick 80c51e0 file1 version 5 - minor changes
```
- **pick** - Keep the commit as is.
- **reword** - Edit the commit message.
- **squash** - Combine this commit with the previous one.
- **edit** - Modify the commit contents.

For example, To edit the commit message:
```
pick f33942b file1 version 5
reword c327a5a file1 version 5 - mino changes
pick 80c51e0 file1 version 5 - minor changes
```
save this, it will open a new editor where you have to give the commit message and save it.
```bash
[detached HEAD c327a5a] file1 version 5 - mino changes
 Date: Wed Mar 19 12:52:39 2025 +0530
 1 file changed, 1 insertion(+), 1 deletion(-)
Successfully rebased and updated refs/heads/master.
```
```bash
commit c327a5a099f9282c2fddcb3475cdbb2e4a94ccce
Author: Harish G <harishgovind6000@gmail.com>
Date:   Wed Mar 19 12:52:39 2025 +0530

    file1 version 5 - mino changes

    file version 5 - editted commit message
```
To squash the last two commits into the first one:
```
pick f33942b file1 version 5
squash c327a5a file1 version 5 - mino changes
squash 80c51e0 file1 version 5 - minor changes
```

After squashing, Git will ask you to edit the combined commit message. Adjust it as needed and save.
```bash
[detached HEAD ba47018] file1 version 5
 Date: Wed Mar 19 12:51:48 2025 +0530
 1 file changed, 1 insertion(+), 1 deletion(-)
Successfully rebased and updated refs/heads/master.
```
```
* ba47018 (HEAD -> master) file1 version 5
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
## Why Squashing Helps
- **Clean Commit History:** It removes unnecessary commits, making it easier to read.
- **Easier Code Review:** Reviewers can follow a streamlined set of meaningful commits.
- **Efficient Merging:** Fewer commits reduce merge complexity.