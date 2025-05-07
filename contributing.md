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

## 🧩 Branch Naming Convention 
### Use the following format for all branch names:

<type>(ATOM-RepositoryAcronym): description-in-kebab-case

**Allowed types:**

| Type       | Meaning                            |
|------------|------------------------------------|
| `feat`     | New feature                        |
| `fix`      | Bug fix                            |
| `refactor` | Code refactoring                   |
| `docs`     | Documentation changes              |
| `test`     | Adding or updating tests           |
| `ci`       | CI/CD or pipeline changes          |
| `chore`    | Other tasks (build, infra, etc.)   |

**Examples:**
- `feat(ATOM-SOFT): add-bluetooth-module-support`
- `fix(ATOM-HARD): fix-login-endpoint-response`
- `docs(ATOM-DOCS): update-deployment-guide`

### Commits must follow the same structure as branches:
<type>(ATOM-REPOSITORYNAME): short and clear description in imperative form
**Examples:**
- `feat(ATOM-FIRMWARE): implement ultrasonic sensor`
- `fix(ATOM-API): fix token validation`
- `chore(ATOM-WEB): remove outdated dependencies`

---

## 🔁 Pull Requests (PRs)

When opening a PR, use this format for the title:
<type>(ATOM-REPOSITORYNAME) - Clear and concise description

### Convention per Repository

| Repository     | Branch / Commit / PR Prefix Example                | Description Example                        |
|----------------|----------------------------------------------------|--------------------------------------------|
| `hardware`     | `feat(ATOM-HW-): integrate-ultrasonic-sensor`| For all firmware, electronics or embedded  |
| `software`     | `fix(ATOM-SW-): fix-face-detection-algorithm`| Backend/frontend, computer vision, etc.    |
| `atom-project` | `chore(ATOM-PJT-): restructure-project-folders`| General coordination / umbrella repo       |
| `docs`         | `docs(ATOM-DOCS-): update-installation-guide`      | Documentation, diagrams, manuals           |
| `utils`        | `feat(ATOM-UTILS-): add-serial-parser-script`      | Scripts, helpers, automation tools         |


**Examples:**
- `feat(ATOM-SW-) - Add OLED display support`
- `fix(ATOM-DOCS-) - Fix OAuth authentication`
- `docs(ATOM-UTILS-) - Improve contribution guide`

Include in the PR body:
- Reference to the related issue (e.g., `Closes #42`)
- A checklist of what's been done
- Screenshots or videos if applicable

---

## 📋 PR Checklist

Before submitting your pull request, make sure:

- [ ] The branch follows the correct naming pattern
- [ ] Your code was tested locally
- [ ] There are no conflicts with `main`
- [ ] The PR description is clear and informative
- [ ] The CI pipeline passed successfully (if any)

---

## 🤖 Contribution Tips

- Always pull the latest changes from `main` before starting (`git pull origin main`)
- Use **Squash Merge** to keep a clean commit history
- Make atomic and meaningful commits
- Keep branches small and focused

---

## 💬 Contact the Team

If you have any questions, suggestions, or issues, feel free to open an issue or contact the project maintainers.

Thanks for being part of the ATOM project! 🚀
---

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

## Workflow

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
