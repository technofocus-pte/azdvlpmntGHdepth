# **Lab 12: Secure your DevOps Pipeline with GitHub Advanced Security (GHAS)**

In modern software development, securing the DevOps pipeline is as
critical as delivering features quickly. GitHub Advanced Security (GHAS)
provides integrated tools to detect vulnerabilities, enforce security
policies, and prevent sensitive data leaks directly within your
repositories. This lab demonstrates how to enable CodeQL scanning,
identify insecure coding patterns, and configure secret scanning with
push protection to safeguard your applications. By the end, you will
understand how GHAS acts as a security quality gate, ensuring that
unsafe code and secrets never reach production.

## **Objectives**

- Enable CodeQL scanning for automated vulnerability detection

- Test GHAS by introducing insecure code patterns

- Use CodeQL checks to block unsafe merges

- Configure secret scanning with push protection

- Continuously monitor and fix security issues in GitHub

### **Exercise 1: Automate Security with CodeQL Scanning**

**Goal:** You will enable CodeQL scanning in your repository. This sets
up a workflow that automatically checks your code for vulnerabilities
whenever you push changes or open a pull request.

1.  Sign in to your +++https://github.com/+++ account.

2.  Click on the **+** icon and create **a new repository**.

    ![A screenshot of a computer Description automatically
    generated](./media/image1.png)

3.  Set the repository name as +++payments-api+++. Make sure repository is
    set to **Public** and add a README file. Click on **Create
    repository**.

    ![A screenshot of a computer Description automatically
    generated](./media/image2.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image3.png)

4.  On the payments-api repository, select **create a new file** from
    the **Add file** dropdown.

    ![A screenshot of a computer Description automatically
    generated](./media/image4.png)

5.  Enter file name as **app.js** and add the below code. **Commit** the
    changes.

    ```
    function getUser(userId) {
    const query = `SELECT * FROM users WHERE id = ${userId}`;
    return query;
    }

    module.exports = { getUser };
    ```

    ![A screenshot of a computer Description automatically
    generated](./media/image5.png)

6.  Add the commit message and click **commit changes**.

    ![A screenshot of a computer Description automatically
    generated](./media/image6.png)

7.  Once the changes are committed, navigate to repository **Settings**.

    ![A screenshot of a web page Description automatically
    generated](./media/image7.png)

8.  Select **Advanced Security** option from the left pane.

    ![A screenshot of a computer Description automatically
    generated](./media/image8.png)

9.  Scroll down to **CodeQL Analysis** and select **Advanced** setup.

    ![A screenshot of a computer Description automatically
    generated](./media/image9.png)

10. Keep the file name as is and **replace** the code with the below
    code and **commit** the changes:

    ```
    name: "CodeQL"

    on:
    push:
        branches: [ "main" ]
    pull_request:
        branches: [ "main" ]
    schedule:
        - cron: '0 0 * * 0'

    jobs:
    analyze:
        name: Analyze
        runs-on: ubuntu-latest

        permissions:
        actions: read
        contents: read
        security-events: write

        strategy:
        fail-fast: false
        matrix:
            language: [ 'javascript' ]   # change to 'java' if needed

        steps:
        - name: Checkout repository
            uses: actions/checkout@v4

        - name: Initialize CodeQL
            uses: github/codeql-action/init@v3
            with:
            languages: ${{ matrix.language }}

        - name: Autobuild
            uses: github/codeql-action/autobuild@v3

        - name: Perform CodeQL Analysis
            uses: github/codeql-action/analyze@v3
    ```

    ![A screenshot of a computer Description automatically
    generated](./media/image10.png)

11. Update the **commit message** and commit changes.

    ![A screenshot of a computer Description automatically
    generated](./media/image11.png)

12. Navigate to Actions tab and select **CodeQL** from the left pane.
    You’ll see a workflow and wait for it till the status shows
    successful.

    ![A screenshot of a computer Description automatically
    generated](./media/image12.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image13.png)

### **Exercise 2: Detect Vulnerabilities in Practice**

**Goal:** You will introduce insecure code patterns on a separate branch
and create a pull request. CodeQL will detect the issues and block
unsafe merges, showing how security checks protect your main branch.

1.  Navigate to the **Code** tab and create a **new codespace** on main.

    ![A screenshot of a computer Description automatically
    generated](./media/image14.png)

2.  Wait for 4-5 mins for the codespace to load all the dependencies and
    packages.

3.  Open the terminal and run the command to switch to a new branch
    named **security/codeql-test** so you can isolate changes for CodeQL
    security testing without affecting the main branch.

    +++git checkout -b security/codeql-test+++

    ![A screenshot of a computer Description automatically
    generated](./media/image15.png)

4.  Open the existing **app.js** file and **replace** the code with the
    below code:

    ```
    const express = require('express');
    const app = express();

    // Simulated request handler
    app.get('/user', (req, res) => {
    const userId = req.query.id;

    const query = "SELECT * FROM users WHERE id = " + userId;

    const file = req.query.file;
    res.sendFile('/uploads/' + file);
    });

    app.listen(3000);
    ```
    ![A screenshot of a computer Description automatically
    generated](./media/image16.png)

5.  Stage the modified file in the current directory for commit. Run the
    command:  
      
    +++git add .+++

    ![A screenshot of a computer Description automatically
    generated](./media/image17.png)

6.  Create the **commit** with the staged changes and the given message.
    Run the command:  
      
    +++git commit -m "test: add real vulnerable patterns"+++

    ![A screenshot of a computer Description automatically
    generated](./media/image18.png)

7.  Now, upload the commits to the remote repository on the branch
    (security/codeql-test). Run the command:  
      
    +++git push origin security/codeql-test+++

    ![A screenshot of a computer Description automatically
    generated](./media/image19.png)

8.  Navigate to your GitHub repository and select **compare and pull request** notification.

    ![A screenshot of a computer Description automatically
    generated](./media/image20.png)

9.  Proceed with creating a **pull request**.

    ![A screenshot of a computer Description automatically
    generated](./media/image21.png)

10. You’ll see CodeQL will do the quality checks before merging the pull
    request.

    ![A screenshot of a computer Description automatically
    generated](./media/image22.png)

11. Some checks were not successful — 1 failing check. CodeQL acts like
    a **security quality gate**. It can:

    - Block unsafe code

    - Highlight vulnerabilities before merge

    After reviewing the checks, **merge** the pull request.

    ![A screenshot of a chat Description automatically
    generated](./media/image23.png)

12. If you merge the PR with unresolved issues, the vulnerable code goes
    into main. **Confirm** the merge.

    ![A screenshot of a computer Description automatically
    generated](./media/image24.png)

13. Navigate to **Actions** tab and make sure the **merge** **workflow**
    run is **succeeded** before moving to the next step.

    ![A screenshot of a computer Description automatically
    generated](./media/image25.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image26.png)

14. Navigate to **Security and quality** tab. On the **code scanning
    alerts** option, select **view alerts**.

    ![A screenshot of a computer Description automatically
    generated](./media/image27.png)

15. Navigate to **Security and quality** tab. On the **code scanning alerts** option, select **view alerts**.

    CodeQL scans code using predefined security rules and detects risky
    patterns.  
    After merging, these findings are stored in the Security tab of GitHub
    to track vulnerabilities in the main codebase. This helps teams monitor
    and fix security issues continuously.

    ![A screenshot of a computer Description automatically
    generated](./media/image28.png)

### **Exercise 3: Prevent Secret Leaks with Push Protection**

**Goal:** You will test secret scanning by committing a fake token. Push
protection will block the commit, demonstrating how GitHub prevents
sensitive credentials from being exposed.

1.  Navigate to **Settings** tab and select **Advanced security** option
    from the left pane.

    ![A screenshot of a computer Description automatically
    generated](./media/image29.png)

2.  Make sure **Push Protection** is enabled.

    ![A screenshot of a computer Description automatically
    generated](./media/image30.png)

3.  Now, open the **codespace** and in terminal, run the below command.
    This command will write a fake GitHub personal access token into a file
    named **.env.test**

    +++echo ' ghp_abcdefghijklmnopqrstuvwxyz1234567890abcd' > .env.test+++

    ![A screenshot of a computer Description automatically
    generated](./media/image31.png)

4.  Run the below command to stage the .env.test file so it will be
    included in the next commit:

    +++git add .env.test+++

    ![A screenshot of a computer Description automatically
    generated](./media/image32.png)

5.  Run the below command. This creates a commit containing the staged
    file with a message indicating it’s for secret detection testing.

    +++git commit -m "test secret detection"+++

    ![A screenshot of a computer Description automatically
    generated](./media/image33.png)

6.  Upload the commit to the repository on the current branch, so secret
    scanning tools can detect the test token.

    +++git push+++

    **Expected result:**

    **GitHub will block your push because of the secret detection.** This
    error occurs because GitHub detected a sensitive value (like an API
    key) in your commit during git push. Push protection blocks the upload
    to prevent secrets from being exposed in the repository. It means you
    must remove or secure the secret before the code can be pushed.

    ![A screenshot of a computer Description automatically
    generated](./media/image34.png)

## **Conclusion**

Securing a DevOps pipeline requires proactive detection and prevention
of risks at every stage of development. Through this lab, you enabled
CodeQL analysis to identify vulnerabilities, tested GHAS’s ability to
block unsafe code merges, and configured secret scanning to prevent
credential leaks. Together, these exercises highlight how GitHub
Advanced Security strengthens the integrity of your repository by
embedding security checks directly into the developer workflow. By
adopting GHAS, teams can ensure that security is not an afterthought but
a continuous, automated safeguard within their DevOps lifecycle.
