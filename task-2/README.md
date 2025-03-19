# Using .gitignore and Tracking Files

## Objective
- Set up a `.gitignore` file to exclude certain files or directories.
- Verify that ignored files are not tracked by Git.

## Requirements
- Create a `.gitignore` file with patterns (e.g., ignoring log files or temporary files).
- Add files that match and do not match the ignore patterns.
- Use `git status` to confirm which files are being tracked.

## Prerequisites
- Git installed on your system.
- A repository with git initailized and tracked.

## Steps
I have a folder named Testing with Git initialized. It contains a cache folder, a .env file, an error.log file, file1.txt, and file2.txt. I want to exclude the cache folder, log files, and the .env file from being tracked by Git.
### 1. Check Git Status
```bash
git status
```
git status shows the current state of your working directory and staging area.
```bash
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .env
        cache/
        error.log

nothing added to commit but untracked files present (use "git add" to track)
```
### 2. Create a `.gitignore` file with the following content
```bash
.env
*.log
/cache
```
This will ignore all `.log` files, `.env` file and `cache` folder.

### 3. Check Git Status
```bash
git status
```
```bash
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore

nothing added to commit but untracked files present (use "git add" to track)
```
We can see that the .env file, log files, and the cache folder are ignored, with only the .gitignore file appearing as untracked.

4. **Commit Changes**
```bash
git add .
git commit -m "Add .gitignore and track necessary files"
```
```bash
[master 6fda4c4] Add .gitignore and track necessary files
 1 file changed, 3 insertions(+)
 create mode 100644 .gitignore
```

### 5. Check Git Status again
```bash
git status
```
```bash
On branch master
nothing to commit, working tree clean
```
Now there are no untracked files.


