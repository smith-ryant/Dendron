---
id: eun05oyg5vuos70e8so1sv7
title: Notes
desc: ""
updated: 1722875354746
created: 1718830878755
---

## Summary of Commands

See more specifics in other sections below

```bash
# Navigate to your project directory
cd path/to/your/project

# Create a new README file
echo "# Name-of-Project" >> README.md

# Initialize a new Git repository
git init

# Add the README file to the staging area
git add README.md

# Commit the file
git commit -m "first commit"

# Create the main branch
git branch -M main

# Add the remote repository URL
git remote add origin https://github.com/smith-ryant/Name-of-Project.git

# Push the changes to the remote repository
git push -u origin main

# Create and switch to a new branch (e.g., feature-branch)
git checkout -b feature-branch

# Make some changes, then add and commit those changes
echo "Some changes" >> changes.txt
git add changes.txt
git commit -m "Added changes to feature-branch"

# Push the new branch to the remote repository
git push -u origin feature-branch

# Switch back to the main branch
git checkout main

# Merge the feature branch into the main branch
git merge feature-branch

# Push the updated main branch to the remote repository
git push origin main
```

## To create a new reposoitory from the command line:

Navigate to the project directory (the root).
Change `Name-of-Project` to the name of your project.

```bash
echo "# `Name-of-Project`" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/smith-ryant/`Name-of-Project`.git
git push -u origin main
```

## To push to an existing repositroy from the command line

```bash
git remote add origin https://github.com/smith-ryant/`Name-of-Project`.git
git branch -M main
git push -u origin main
```

## To branch off main

To branch from the main of the specified repository and create a new branch named `NameOfComponent.component`, you can follow these steps:

1. Open your terminal or command prompt.
2. Clone the repository if you haven't already:

```bash
git clone https://github.com/Codemosphere/ViteSantasCauseWebsite.git
```

3. Change into the repository directory:

```bash
cd ViteSantasCauseWebsite
```

4. Ensure you're on the `main` branch and pull the latest changes:

```bash
git checkout main
git pull origin main
```

5. Create and switch to the new branch `NameOfComponent.component`:

```bash
git checkout -b NameOfComponent.component
```

Now you have successfully created a new branch from the `main` branch. You can start working on your changes in the `NameOfComponent.component` branch.

## Push Changes and Merge Them Into the main branch

To push your changes and merge them into the main branch while keeping the branch, follow these steps:

Push the changes to the remote repository:

```bash
git push origin section-two
```

Switch to the main branch:

```bash
git checkout main

Merge the section-two branch into the main branch:
```

```bash
git merge section-two
```

Push the updated main branch to the remote repository:

```bash
git push origin main
```

## This will push your changes from the section-two branch to the remote repository, merge those changes into the main branch, and then push the updated main branch back to the remote repository.

`What is a git pull?`  
A `git pull` command in Git is used to update the local version of a repository from a remote repository. It is a combination of two commands: `git fetch` and `git merge`. When you execute `git pull`, it first fetches the changes from the specified remote repository (usually the one you cloned from or the origin) and then merges those changes into your current branch.

Here’s a more detailed breakdown of what happens during a `git pull`:

1. **Fetch**: The command retrieves any updates from the remote repository. This means it downloads new commits, files, and other data from the remote repository.

2. **Merge**: After fetching the updates, `git pull` will merge the updates into your current working branch. If there are any changes that conflict with your local changes, you'll need to resolve those conflicts manually.

The syntax for `git pull` is:

```
git pull [options] [<repository> [<refspec>...]]
```

In most cases, you will use it simply as:

```
git pull
```

This pulls changes from the remote repository and branch that your local branch is tracking.

### Example

To pull the latest changes from the remote repository named `origin` into your current branch:

```
git pull origin
```

If you want to pull changes from a specific branch, you can specify it:

```bash
git pull origin main
```

This command fetches changes from the `main` branch of the remote repository `origin` and merges them into your current branch.

### Potential Issues

- **Conflicts**: If there are conflicting changes between your local branch and the remote branch, Git will prompt you to resolve those conflicts.
- **Rebasing**: Some teams prefer using `git pull --rebase` instead of `git pull` to maintain a cleaner commit history. This command fetches the changes and then replays your local commits on top of the fetched commits.

To use `git pull --rebase`:

```
git pull --rebase
```

This command can be especially useful to avoid unnecessary merge commits in your project's history.

---

## Accidentally Deleted

If you've accidentally deleted a folder and want to restore your local repository to match your current GitHub repository, you can use the following steps in the command line to pull the latest changes from the `main` branch on GitHub:

1. **Open your terminal** and navigate to your local Git repository.

2. **Ensure you're on the `main` branch** (or whichever branch you're working on):

   ```bash
   git checkout main
   ```

3. **Fetch the latest changes from the remote repository** to ensure your local repository is aware of any updates on GitHub:

   ```bash
   git fetch origin
   ```

4. **Reset your local branch to match the remote branch**, discarding any local changes and bringing your local repository in sync with GitHub:

   ```bash
   git reset --hard origin/main
   ```

   This command will reset your local `main` branch to match the remote `main` branch, effectively restoring your code to the latest state from GitHub. Please note that this will discard any local changes that haven't been pushed to GitHub, so make sure this is what you want before proceeding.

5. **Verify the changes** to ensure everything is restored:

   ```bash
   git status
   ```

   This should indicate that your working directory is clean and matches the remote repository.

### Important Note

- **Backup Important Changes:** If you have any important changes that haven't been pushed to GitHub and want to avoid losing them, consider using `git stash` before the reset command. This will temporarily save your changes, allowing you to apply them later if needed:

  ```bash
  git stash
  ```

- **Restore Stashed Changes:** After resetting and verifying your restored code, you can apply the stashed changes if necessary:

  ```bash
  git stash apply
  ```

By following these steps, you should be able to restore your local code to match the current state of your GitHub repository on the `main` branch. If you have any additional questions or need further assistance, feel free to ask!
