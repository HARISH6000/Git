# Using Git Hooks for Automated Checks

## Objective
- Set up a Git hook to run scripts (like linters or tests) before commits are finalized.

## Requirements
- Create a `pre-commit` hook in the `.git/hooks` directory.
- Write a simple script (e.g., a shell script or Node script) that runs a linter or a unit test.
- Ensure that if the tests or linting fail, the commit is aborted.
- Document how Git hooks can improve code quality in collaborative projects.

## Prerequisites
- node
- eslint
```bash
npx eslint --init
```

## Steps

### 1. Navigate to the `.git/hooks` Directory
Git provides a `.git/hooks` directory within your repository. It contains sample hook scripts.
```bash
cd .git/hooks
```

### 2. Create a Pre-Commit Hook
Create a new file named `pre-commit`.

I took a basic shell script to run ESLint for JavaScript projects:
```bash
#!/bin/bash

# Run ESLint for linting
if ! npx eslint .; then
  echo "Linting failed. Please fix the errors before committing."
  exit 1
fi

echo "Linting passed. Proceeding with commit."
```
- If ESLint reports any issues, the commit will be aborted.
- Modify this script to run other tests or checks as needed.

### 4. Test the Hook
1. Make changes to your code.
2. Run:
```bash
git add .
git commit -m "Test commit with pre-commit hook"
```
If there are linting issues, the commit will fail.for example,
```
let x = 10
console.log('Hello, World!')
```
```bash
  1:5  error  'x' is assigned a value but never used  no-unused-vars

✖ 1 problem (1 error, 0 warnings)

Linting failed. Please fix the errors before committing.
```
```
let x = 10;
console.log(x);
```
```bash
Linting passed. Proceeding with commit.
[branch3 a423de2] Testing pre-commit
 1 file changed, 2 insertions(+)
 create mode 100644 test.js
```


### 5. Additional Commands
To Skip the Hook (if necessary):
```bash
git commit --no-verify
```

## Benefits of Using Git Hooks
- Ensures consistent code quality by running automated checks before every commit.
- Prevents buggy or unformatted code from entering the repository.
- Encourages team-wide adherence to coding standards.