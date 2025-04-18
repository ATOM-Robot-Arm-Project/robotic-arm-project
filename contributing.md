# Branching Guide for the Project

This document explains how to manage and use branches in any repository of this project. The branch structure is organized into **long branches** (for main areas of the project) and **short branches** (for specific tasks, such as new features).

## Branch Structure

### Long Branches
1. **`main`**: 
   - This is the main branch containing production-ready code. 
   - **Usage**: The `main` branch should always reflect the stable version of the code.
   - **How to update**: The `main` branch will only be updated through pull requests from `development` or other long-lived branches.

2. **`development`**:
   - The branch where all new features and changes are integrated before being sent to production.
   - **Usage**: All developers should merge their features into `development` first.
   - **How to update**: Use `git pull origin development` to update your local branch with the latest changes.

3. **`documentation`**:
   - A branch dedicated to the project documentation.
   - **Usage**: If you need to update the documentation (e.g., updates to README, guides, etc.), create a branch from `documentation` and merge back into it.
   - **How to update**: Documentation will be maintained separately from the codebase, allowing more frequent and specific updates.

## 🧩 Branch Naming Convention
 ### **`Documentation branches must start with 'docs/'`**:
  - ✅ Correct: `docs/fix-readme`
  - ❌ Incorrect: `documentation`, `docfix`, `readme-update`

- Pull Requests without this convention will be denied.

### Short Branches
These branches are created from the long branches and serve specific features and bug fixes. 

1. **`feature/{name}`**:
   - **Usage**: To develop a new feature. The `feature` branch should be created from the `development` branch.
   - **Example**: `feature/login-system`
   - **How to create**:
     ```bash
     git checkout development
     git checkout -b feature/{feature-name}
     ```

2. **`bugfix/{name}`**:
   - **Usage**: To fix bugs. The `bugfix` branch can be created from either `development` or `main`, depending on the urgency of the fix.
   - **Example**: `bugfix/fix-login-error`
   - **How to create**:
     ```bash
     git checkout development
     git checkout -b bugfix/{bug-name}
     ```

### Workflow

1. **Creating a new feature or bugfix branch**:
   - Always create a new branch for each specific task, using the appropriate naming convention.
   - **Example**:
     ```bash
     git checkout development
     git pull origin development  # Ensure your local branch is up-to-date
     git checkout -b feature/{feature-name}
     ```

2. **Making changes and commits**:
   - Make regular commits with clear messages about what has been changed. Avoid large and unrelated commits.
   - **Example**:
     ```bash
     git add .
     git commit -m "Add login system functionality"
     ```

3. **Merging your feature into `development`**:
   - Once the feature or fix is complete, create a pull request (PR) to merge it into the `development` branch and wait for review.
   - **Example PR**: "Add login system"
   - To ensure a quality PR, make sure to test your changes locally and communicate any dependencies that might impact other features.

4. **Keeping branches updated**:
   - Before starting new work or making a merge, update the branch you're working on with the latest changes from `development`.
   - **Example**:
     ```bash
     git checkout development
     git pull origin development
     git checkout feature/{feature-name}
     git rebase development
     ```

### Merge Conflicts

- **How to handle conflicts**: When merge conflicts occur, Git will notify you and you will need to resolve them manually. After resolving conflicts, commit the changes to complete the merge.
- **Example**:
  ```bash
  git status
  git add {resolved-files}
  git commit -m "Resolve merge conflicts"
