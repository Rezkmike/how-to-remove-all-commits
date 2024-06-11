To remove all commit history from your GitHub repository, including any sensitive information like credentials, you'll need to rewrite the history using Git. Here are the steps to completely remove the history, which will effectively make your repository appear as if it was just created, without any previous commits:

### Warning:
This process will irreversibly change your repository's history. Any collaborators will need to clone the repository again. Any forks may retain the old history unless they too are reset in this manner.

### Steps:

1. **Backup Your Current Repository**
   Before proceeding, make sure to backup your current repository in case you need to restore or refer to anything later.

2. **Clone the Repository Locally**
   If you haven't already cloned the repository locally, do so:
   ```bash
   git clone https://github.com/your-username/your-repository.git
   cd your-repository
   ```

3. **Check Out to a Temporary Branch**
   Create a temporary branch and check it out:
   ```bash
   git checkout --orphan temp_branch
   ```

4. **Add All the Files**
   Add all the files to this temporary branch:
   ```bash
   git add -A
   ```

5. **Commit the Changes**
   Make a new initial commit:
   ```bash
   git commit -am "Initial commit"
   ```

6. **Delete the Old Branch**
   Delete the main branch (replace `main` with your default branch name if it's different):
   ```bash
   git branch -D main
   ```

7. **Rename the Temporary Branch**
   Rename the temporary branch to the default branch name:
   ```bash
   git branch -m main
   ```

8. **Force Push to GitHub**
   Force push the changes to overwrite the history on GitHub:
   ```bash
   git push -f origin main
   ```

9. **Check Your Repository**
   Your repository should now only contain the one commit you just made, and all previous history, including any commits containing credentials, should be gone.

### Clean Up Sensitive Data from GitHub

Since you had credentials in your commit history, consider these additional steps:

- **Rotate the Credentials**: Change any credentials that were exposed in the commit history as they might still be accessible in some forks or clones made by others before you cleaned up your repository.

- **Consider Using Git Secrets**: For future safety, you can use tools like `git-secrets` to prevent committing sensitive information.

This approach ensures that the sensitive information is no longer visible in your repository's history on GitHub.
