# Skillura Branching Instructions

## Backend:
1. Fork the main or master branch of the repository (ex. Skillura's backend git repository). 
2. Create and go to your preferred folder (eg. skillura). Open a terminal under that folder and type `git init` then clone your local repository for backend afterwards.
    ```
    git init
    ```
    ```
    git clone https://github.com/your-username/011-skillura-backend.git
    ```
3. Go to the cloned folder (011-skillura-backend) and add local remote repository. In your terminal, type:
    ```
    git remote add origin https://github.com/your-username/011-skillura-backend.git
    ``` 
    Change `your-username` to your github username.
    <br>
    This will be your local remote repository

4. Add skillura remote repository. In your terminal, type:
    ```
    git remote add skillura_be https://github.com/AAA-Software/011-skillura-backend.git
    ```
    This will be the backend remote repository
5. Check if origin and skillura_be is added.
    ```
    git remote -v
    ```
    ![Local and Remote Repository](https://i.imgur.com/jCxznvg.png)

## Frontend:
1. Fork the main or master branch of the repository (ex. Skillura's frontend git repository). 
2. Go to skillura folder that you created then clone your local repository for frontend afterwards.
    ```
    git clone https://github.com/your-username/011-skillura-frontend.git
    ```
3. Go to the cloned folder (011-skillura-frontend) and add local remote repository. In your terminal, type:
    ```
    git remote add origin https://github.com/your-username/011-skillura-frontend.git
    ``` 
    Change `your-username` to your github username.
    <br>
    This will be your local remote repository

4. Add skillura remote repository. In your terminal, type:
    ```
    git remote add skillura_fe https://github.com/AAA-Software/011-skillura-backend.git
    ```
    This will be the frontend remote repository
5. Check if origin and skillura_fe is added.
    ```
    git remote -v
    ```
    ![Local and Remote Repository](https://i.imgur.com/nOJqasX.png)

*If no error, and you have checked that the origin, skillura_be, and skillura_fe is added. Then, you may proceed with:*
<br>

### Using git fetch
- This command downloads changes from the remote repository (e.g., GitHub) but does not merge them into your local branch.
- It updates your local references to the remote branches.
- Useful when you want to check for updates before merging.
    ```
    git fetch skillura_be
    ```
    *(This fetches updates from the skillura_be remote repository but does not apply them to your local branch.)*

### Using git pull
- It fetches updates from the remote repository and immediately merges them into your current local branch.
- If there are conflicts, Git will ask you to resolve them.
- This command is essentially git fetch + git merge.
    ```
    git pull skillura_be
    ```
    *(This fetches and merges changes from the skillura_be remote repository into your current branch.)*

    If you want to pull an specific branch from skillura_be remote repository. You can also use:
    ```
    git pull skillura_be staging
    ```

### Using git merge
- This command merges changes from one branch into another.
    ```
    git merge skillura_be/staging
    ```
    *(This merges changes from the remote staging branch into your current branch.)*


### Copying remote branch to your local branch
- Create first a branch that will be used for requesting a PR.
    1. You should be on staging or production branch. On this tutorial I'll use staging branch.
        ![Staging Branch](https://i.imgur.com/iVjUwje.png)
    2. Then click on the branches selection. Type your specified branch name. Then click the "Create Branch [your-specified branch name]"
        ![Staging Branch](https://i.imgur.com/nDp4Cby.png)
    3. After creating a branch on the skillura remote repository. You may proceed to copying that remote branch to your local branch. Go your your terminal and type:
        - Use `git checkout -b [your-branch-local-repo] [remote-name/remote-branch-repo]`
            ```
            git checkout -b fix/SK-9999-login-issue skillura_be/fix/SK-9999-login-issue
            ```
    4. And you're done! You have created your local branch that is based on the remote branch. You may start fixing the issue. Push it when you're finish and request a PR on the remote branch.

### 📌Note: When working on a new feature or fixing bugs, use the following branch naming convention:

- For new feature: `feature/[jira-ticket-id]-short-description`
- For fixes: `fix/[jira-ticket-id]-short-description`
- For hotfixes: `hotfix/[jira-ticket-id]-short-description`
<br>
<br>
<br>

---
## Proposed Git Workflow for Issue Resolution and Deployment:

### 1. Create a Local Branch
- Copy the remote branch (sk-9999) containing the issue to a local branch (sk-9999-local).

### 2. Sync with Production
- Update the local branch with the latest changes from the remote production branch to ensure the fix is applied to the most recent version.

### 3. Apply Fixes and Push Changes
- Implement the necessary fixes and push the changes to the local branch.
- Create a Pull Request (PR) to merge sk-9999-local into sk-9999.

### 4. Code Review & Approval
- A manager or an authorized reviewer checks the PR and reviews the code changes in sk-9999.

### 5. Merge to Issue Branch (sk-9999)
- After the code review is completed, an authorized person merges the PR into sk-9999.

### 6. Prepare for Staging Deployment
- Once sk-9999 has the updated fix, a PR is created to merge sk-9999 into the staging branch.
- Do not merge immediately—another round of code review is required to check for conflicts or additional issues.

### 7. Merge to Staging
- If no issues are found during the second review, the PR is approved, and sk-9999 is merged into staging.

### 8. Deploy to Staging Server
- The staging site is updated with the latest fixes.

### 9. QA Testing
- The QA team tests the staging site for any new issues.
- If issues are found, a new ticket is created to Jira, and the cycle repeats.

### 10. Schedule Production Release
- The manager schedules the release, typically on a predefined deployment day (e.g., Monday).
- He/she will make a PR from the staging branch to production branch. But before merging it, a final review is performed to check for conflicts.

### 11. Merge to Production
- If no conflicts or issues are found, the staging branch is merged into production.

### 12. Deploy to Production Server
- The production site will now be updated with the latest fixes, new features, and hotfixes.
<br>
<br>

This structured workflow ensures a smooth process from issue resolution to deployment, with multiple review checkpoints to maintain code quality and stability.

