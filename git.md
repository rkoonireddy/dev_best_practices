# **Git Workflow: Using Merge and Rebase**

## Key Principles

* **Do not rebase commits that exist outside your repository and that others may have based work on.** Rebasing rewrites history, which can cause conflicts for others working on the same branch.
* **Use rebase to keep your feature branch updated.** When working on a feature branch, use rebase to incorporate the latest changes from `main` without introducing extra merge commits.
* **Use merge to integrate changes into shared branches.** When your feature is complete, merge it back into `main` to preserve history and ensure a smooth integration.

## Recommended Process

### Keeping Your Feature Branch Up to Date (Rebase)

While working on a feature branch, `main` may receive updates from other developers. To ensure your branch remains current:

1.  **Switch to your feature branch:**

    ```bash
    git checkout feature-branch
    ```

2.  **Fetch the latest changes:**

    ```bash
    git fetch origin
    ```

3.  **Rebase your branch on top of the latest `main`:**

    ```bash
    git rebase origin/main
    ```

4.  **If conflicts occur, resolve them and continue:**

    ```bash
    git rebase --continue
    ```

### Merging the Feature Branch Back into `main`

Once your feature is complete and tested, merge it into `main` to preserve commit history:

1.  **Switch to `main`:**

    ```bash
    git checkout main
    ```

2.  **Ensure `main` is up to date:**

    ```bash
    git pull origin main
    ```

3.  **Merge your feature branch:**

    ```bash
    git merge feature-branch
    ```

4.  **Push the merged changes:**

    ```bash
    git push origin main
    ```

## Example Workflow

**Scenario:** You are working on `feature-branch`, and `main` has received new commits (X and Y):

```
A --- B --- C --- X --- Y (main)
     \
      D --- E (feature-branch)
```

### Step 1: Rebase Feature Branch

Applying rebase moves your changes on top of `main`:

```bash
# Switch to feature branch
git checkout feature-branch

# Rebase onto the latest main
git rebase origin/main
```

New history:

```
A --- B --- C --- X --- Y --- D' --- E' (feature-branch)
```

### Step 2: Merge Back into `main`

Once the feature is complete:

```bash
# Switch to main
git checkout main

# Merge feature-branch
git merge feature-branch
```

Final history:

```
A --- B --- C --- X --- Y --- D' --- E' (main)
```

## Summary

* Use `rebase` to keep feature branches up to date with `main`.
* Use `merge` when integrating feature branches into `main` to preserve history.
* Never rebase commits that others may have based work on to avoid rewriting shared history.

By following this workflow, you ensure a clean Git history while minimizing conflicts in a team environment.

## Git Commands in a Nutshell

### Git Commands and Their Purpose

#### Basic Setup & Configuration

| Command | Description |
| :------------------------------------- | :------------------------------------------------ |
| `git init` | Initialize a new Git repository |
| `git clone <repo-url>` | Clone an existing repository |
| `git config --global user.name "Your Name"` | Set your Git username |
| `git config --global user.email "you@example.com"` | Set your Git email |

#### Working with Files

| Command | Description |
| :-------------------------- | :----------------------------------------------------- |
| `git status` | Show the status of the working directory and staging area |
| `git add <file>` | Stage a specific file for commit |
| `git add .` | Stage all modified and new files |
| `git commit -m "Commit message"` | Commit changes with a message |
| `git commit --amend -m "New commit message"` | Modify the last commit message |

#### Working with Branches

| Command | Description |
| :---------------------------- | :----------------------------------------- |
| `git branch` | List all branches |
| `git branch <branch-name>` | Create a new branch |
| `git checkout <branch-name>` | Switch to a different branch |
| `git checkout -b <branch-name>` | Create and switch to a new branch |
| `git branch -d <branch-name>` | Delete a local branch |
| `git push origin --delete <branch-name>` | Delete a remote branch |

#### Synchronizing with Remote

| Command | Description |
| :---------------------- | :--------------------------------------------- |
| `git remote -v` | List remote repositories |
| `git fetch origin` | Fetch changes from remote without merging |
| `git pull origin main` | Fetch and merge changes from remote `main` |
| `git push origin <branch-name>` | Push local changes to remote repository |

#### Merging and Rebasing

| Command | Description |
| :---------------------- | :---------------------------------------------- |
| `git merge <branch-name>` | Merge a branch into the current branch |
| `git rebase <branch-name>` | Reapply commits on top of another branch |
| `git rebase --continue` | Continue rebasing after resolving conflicts |

#### Undoing Changes

| Command | Description |
| :---------------------------- | :--------------------------------------------- |
| `git reset --soft HEAD~1` | Undo the last commit but keep changes staged |
| `git reset --hard HEAD~1` | Undo the last commit and discard changes |
| `git checkout -- <file>` | Discard changes to a file |
| `git revert <commit-hash>` | Create a new commit that undoes a previous commit |

#### Viewing History & Logs

| Command | Description |
| :------------------------------------- | :------------------------------------------------ |
| `git log` | Show commit history |
| `git log --oneline --graph --all` | Show a compact, graphical history |
| `git diff` | Show differences between working directory and last commit |
| `git blame <file>` | Show who modified each line of a file |

#### Stashing Changes

When you need to switch branches or temporarily save your work, use `git stash`:

| Command | Description |
| :------------------ | :------------------------------------------------------------ |
| `git stash` | Save your uncommitted changes and clean your working directory |
| `git stash list` | List all stashes |
| `git stash pop` | Apply the most recent stash and remove it from the stash list |
| `git stash apply` | Apply a stash without removing it from the stash list |
| `git stash drop` | Remove a stash from the list |
| `git stash clear` | Remove all stashes |

## Example Workflow Using These Commands

**Scenario:** Working on a Feature and Merging It into `main`

### Step 1: Clone the Repository

```bash
git clone [https://github.com/user/repo.git](https://github.com/user/repo.git)
cd repo
```

### Step 2: Create a New Branch

```bash
git checkout -b feature-branch
```

### Step 3: Make Changes and Commit

```bash
echo "New feature" > feature.txt
git add feature.txt
git commit -m "Add new feature"
```

### Step 4: Stash Changes (if needed)

If you're switching branches and want to temporarily save changes:

```bash
git stash
```

### Step 5: Update Feature Branch with Latest `main`

```bash
git fetch origin
git rebase origin/main # Apply feature-branch on top of latest main
```

### Step 6: Resolve Conflicts (If Any)

If there are conflicts, resolve them manually and run:

```bash
git rebase --continue
```

### Step 7: Merge Feature into `main`

```bash
git checkout main
git merge feature-branch # Merge with preserved history
git push origin main
```

### Step 8: Delete the Feature Branch

```bash
git branch -d feature-branch
git push origin --delete feature-branch
```

### Step 9: Restore Stashed Changes (If Needed)

If you stashed changes earlier:

```bash
git stash pop
```

Just copy that and save it to a file with a `.md` extension.
