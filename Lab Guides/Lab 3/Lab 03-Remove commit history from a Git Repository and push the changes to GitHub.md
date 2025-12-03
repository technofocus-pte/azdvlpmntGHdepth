# Lab 03: Remove Commit History from a Git Repository

**Objective:**

Imagine you are part of a development team working on a project where
sensitive information, such as API keys or database credentials, was
accidentally committed to your Git repository. Accidental commits can be
tricky to remove with Git.

In this lab, you will:

- Clone the repository with accidentally committed sensitive data.

- Remove/delete the file containing sensitive data from the cloned
  repository and commit the removal.

- Push Changes to GitHub: Upload the updated repository to GitHub to
  reflect the changes.

## Exercise 1: Create the repository with the accidental commit history (sensitive data)

1.  Sign in to your GitHub account.

2.  Browse to the following link: +++https://github.com/technofocus-pte/change-commit-history+++

    In this lab, you will create the repository using a public template
    “**skills-change-commit-history**”.

    ![](./media/image1.png)

3.  Select **Create a new repository** under **Use this template** menu.

    ![A screenshot of a computer Description automatically
    generated](./media/image2.png)

4.  Enter the following details and select **Create Repository**.

- Repository name: +++skills-change-commit-history+++

- Repository type: **Public**

    ![](./media/image3.png)

### Exercise \# 2: Remove/delete the file (.env in the project root directory) containing sensitive data

1.  On the landing page of the cloned repository, navigate to
    **Code>Local>HTTPS** and copy the URL.

    ![](./media/image4.png)

2.  Open **Windows PowerShell** and enter the following command.

    +++git clone \<your-repository-url\>+++

    **Note**: Replace with the URL you copied in step 1.

    ![](./media/image5.png)

3.  Switch to your repository directory, and enter the following command.

    +++cd “C:\Users\Admin\skills-change-commit-history”+++

    **Note**: Replace with the repository name

    ![](./media/image6.png)

4.  Execute the following command to delete .env from the root
    directory,

    +++git rm .env+++

    ![A screenshot of a computer screen Description automatically
    generated](./media/image7.png)

5.  Set your account's default identity by executing:

    +++git config --global user.email "**write your GitHub email account here**"+++

6.  After setting the account's identity, commit the removal of the .env file

    +++git commit -m "remove .env file”+++

    ![A screen shot of a computer Description automatically
    generated](./media/image8.png)

    **Tip**: How to completely remove the .env file from Git history and
    Rewrite total history with new commit hashes?

    Use the following commands to:

- Completely remove the .env file from Git history and rewrite the total history

    **git filter-branch --force --index-filter 'git rm --cached
    --ignore-unmatch.env' --prune-empty --tag-name-filter cat -- --all**

- Push the removal to GitHub

    +++git push origin --force –all+++

6.  Push the removal to GitHub:

    +++git push+++

    ![A screenshot of a computer program Description automatically
    generated](./media/image9.png)

7.  Once you run the ‘git push’ command, you may be asked to connect to
    GitHub by **signing in with your browser.**

    ![A screenshot of a computer screen Description automatically
    generated](./media/image10.png)

8.  If prompted, on the Authorise Git Credential Manager window, click on the
    **Authorise git-ecosystem** to complete the git push command.
    Note: This is possible that the authentication can automatically succeed. Then, you can simply jump to the next step.

    ![A screenshot of a computer Description automatically
    generated](./media/image11.png)

10.  Then, navigate to the PowerShell again, and you’ll see that the push command is successful.

    ![A screenshot of a computer program Description automatically
    generated](./media/image12.png)

**Summary**:

Now you have completed cleaning up your Git repository, ensuring that
sensitive content is not exposed in the repository’s history.

