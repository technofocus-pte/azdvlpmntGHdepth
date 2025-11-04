# Lab 04: Enable secret scanning in a GitHub repository and commit a token

Imagine you're a software developer working on a team project with a
shared GitHub repository. To ensure your code remains secure and free of
accidental leaks, you decide to implement secret scanning—a feature that
helps identify sensitive information like API tokens or passwords that
might be inadvertently committed to the repository.

Objective:

In this hands-on lab, you will:

1.  Enable Secret Scanning: Configure secret scanning on your GitHub
    repository to automatically detect and flag sensitive information.

2.  Commit a Token: Intentionally add a token or other sensitive
    information to the repository to test the effectiveness of the
    secret scanning feature.

## Exercise 1: Create a GitHub repository and enable secret scanning

### Task 1: Create a repository using a template

1.  Sign in to your GitHub account.

2.  Browse to the following link:
    <https://github.com/skills/introduction-to-secret-scanning>

    In this lab you will create the repository using a public template
    “**skills-introduction-to-secret-scanning**”.

    ![](./media/image1.png)

3.  Select **Create a new repository** under **Use this template** menu.

    ![](./media/image2.png)

4.  Enter the following details and select **Create Repository**.

- Repository name: +++skills-introduction-to-secret-scanning+++

- Repository type: **Public**

    ![](./media/image3.png)

### **Task 2: Enable secret scanning** 

1.  On the landing page of the newly created repository, select
    **Settings** from the top navigation bar.

    ![](./media/image4.png)

2.  In the **Security** section on the Sidebar, select **Advanced**.

**Note**: You need to scroll down to see the **Security** menu

    ![](./media/image5.png)

3.  Scroll down to the bottom of the page and click **Enable** for
    secret protection.

    **Note**: If you see a **Disable** button, it means that secret scanning
    is already enabled for the repository. If **Enable** button is visible
    in your case, you can enable this option by clicking on the **Enable**
    button.

    ![](./media/image6.png)

**Note:** When secret scanning is enabled, an email notification about
credentials in the repository is sent to the mail ID associated to the
account. The tokens in this Skills repo are inactive. There is no risk
to the environment.

Now that secret scanning is enabled in this repository, let's commit a
new token to see how it works.

## Exercise 2: Commit a token

In this exercise, you'll commit an AWS key and access ID to the
repository. This is an inactive token that can't be used to log in to
AWS.

1.  In the top left pane of the main navigation bar, click the **Code**
    tab and select the **credentials.yml** file.

    ![](./media/image7.png)

2.  Click the Edit button to the right.

    ![](./media/image8.png)

3.  Copy the following text and paste it below the existing code in the
    edit pane of the **credentials.yml** file.

    ```
    default:
    aws_access_key_id: AKIAQYLPMN5HNM4OZ56B
    aws_secret_access_key: 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
    output: json
    region: us-east-2
    ```

    ![](./media/image9.png)

4.  Click the **Commit changes** button in the top right corner and
    click **Commit Changes** again in the **Commit Changes** window.

    ![](./media/image10.png)

    Note: After you commit the changes, you will receive an alert in your
    mailbox associated with your GitHub account.

    ![A screenshot of a computer Description automatically
    generated](./media/image11.png)

# Summary:

Now you have gained a practical understanding of how to enable and test
secret scanning to protect your code and data.
