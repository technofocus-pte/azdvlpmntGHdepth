# **Lab 13: Automating Code Security: Blocking eval() with GitHub Actions and Semgrep**

As a developer on the Octomatch team, you have already established a
robust testing setup that generates valuable reports for your
application.

### **Objectives**

- Create and configure GitHub Actions workflows

- Upload workflow artifacts such as test coverage reports

### **Exercise 1: Create the repository and baseline app**

1.  Sign in to your +++https://github.com/+++ account.

2.  Click on the **+** icon and create **a new repository**.

    ![A screenshot of a computer Description automatically
    generated](./media/image1.png)

3.  Set the repository name as +++agentic-governance-lab+++. Make sure
    repository is set to **Public** and add a **README** file. Click on
    **Create repository**.

    ![](./media/image2.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image3.png)

4.  Once the repository is created, **create a new file** from the **Add
    file** dropdown.

    ![A screenshot of a computer Description automatically
    generated](./media/image4.png)

5.  Enter the file name as +++index.js+++ and enter the below **code**.
    Once done, **commit** the changes.

    ```
    // Simple Node HTTP app used by the lab
    const http = require('http');

    const server = http.createServer((req, res) => {
    if (req.url === '/health') {
        res.writeHead(200, { 'Content-Type': 'application/json' });
        res.end(JSON.stringify({ status: 'ok' }));
        return;
    }
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello agentic governance lab');
    });

    if (require.main === module) {
    const port = process.env.PORT || 3000;
    server.listen(port, () => {
        console.log(`Server listening on port ${port}`);
    });
    }
    module.exports = server;
    ```

    ![A screenshot of a computer Description automatically
    generated](./media/image5.png)

6.  Keep the copilot’s suggested commit message and **commit** changes
    directly to **main**.

    ![A screenshot of a computer Description automatically
    generated](./media/image6.png)

7.  Navigate to **Code** tab and create **a new file**.

    ![A screenshot of a computer Description automatically
    generated](./media/image7.png)

8.  Enter the file name as +++package.json+++ and paste the below code
    into the file. Once done, **commit** the changes.

    ```
    {
    "name": "agentic-governance-lab",
    "version": "0.1.0",
    "private": true,
    "scripts": {
        "start": "node index.js",
        "test": "node test.js"
    },
    "dependencies": {},
    "devDependencies": {}
    }
    ```

    ![A screenshot of a computer Description automatically
    generated](./media/image8.png)

9.  Add the **commit message** and **commit** changes directly to the
    main branch.

    ![A screenshot of a computer Description automatically
    generated](./media/image9.png)

### **Exercise 2: Enable branch protection and push restrictions**

1.  Navigate to the **Settings** tab and select **Branches** from the
    left pane. Select **Add classic branch protection rule**.

    ![A screenshot of a computer Description automatically
    generated](./media/image10.png)

2.  Enter the Branch name pattern as +++main+++

    ![A screenshot of a computer Description automatically
    generated](./media/image11.png)

3.  Enable **Require a pull request before merging** and make sure atleast 1 approval is selected. 
    Then, enable **Require status checks to pass before merging**

    ![A screenshot of a computer screen Description automatically
    generated](./media/image12.png)

4.  Enable **Require conversation resolution before merging** and Click on **Create**. 

    ![](./media/image13.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image14.png)

### **Exercise 3: Add Semgrep for pattern detection**

1.  Navigate to the Code tab. Click **Add file** (green button) then
    **Create new file**.

    ![A screenshot of a computer Description automatically
    generated](./media/image15.png)

2.  In the **Name your file** box type +++.semgrep.yml+++

3.  Paste the Semgrep YAML content into the editor:

    ```
    rules:
    - id: no-eval
        pattern: eval(...)
        message: "Avoid eval() — dynamic code execution is risky."
        severity: ERROR
        languages:
        - javascript

    - id: no-child-process-exec
        pattern: exec(...)
        message: "Avoid child_process.exec; prefer spawn with sanitized inputs."
        severity: WARNING
        languages:
        - javascript
    ```

    ![A screenshot of a computer Description automatically
    generated](./media/image16.png)

4.  Scroll down to **Commit new file**. Enter a commit message like +++Add Semgrep rules+++.

5.  Choose **Create a new branch** and name it as +++fix/semgrep-rule-eval+++. Click on Propose changes. 

    ![A screenshot of a computer Description automatically
    generated](./media/image17.png)

6.  Click **Commit new file** and create a pull request and review it. 

    ![](./media/image18.png)

    ![](./media/image19.png)

#### **Task 1: Create the Semgrep GitHub Action workflow via the web UI**

1.  Switch to the newly created branch i.e., **fix/Semgrep-rule-eval**.

    ![](./media/image20.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image21.png)

2.  From the repo root, click **Add file → Create new file**.
    
    ![A screenshot of a computer Description automatically
    generated](./media/image22.png)

3.  In the filename box type +++.github/workflows/semgrep.yml+++

    ![A screenshot of a computer Description automatically
    generated](./media/image23.png)

4.  Paste the workflow content:

    ```
    name: Semgrep Scan
    on:
    pull_request:
        types: [opened, synchronize, reopened]
    jobs:
    semgrep:
        runs-on: ubuntu-latest
        steps:
        - uses: actions/checkout@v4
        - name: Setup Python
            uses: actions/setup-python@v4
            with:
            python-version: '3.x'
        - name: Install semgrep
            run: pip install semgrep
        - name: Run semgrep
            run: semgrep --config .semgrep.yml --json --output semgrep-results.json
        - name: Upload results
            uses: actions/upload-artifact@v4
            with:
            name: semgrep-results
            path: semgrep-results.json
        - name: Fail on errors
            run: |
            if [ ! -f semgrep-results.json ]; then echo "No results file"; exit 0; fi
            COUNT=$(jq '.results | length' semgrep-results.json)
            if [ "$COUNT" -gt 0 ]; then
                echo "Semgrep found issues:"
                jq -r '.results[] | "- " + .check_id + " " + .path + ":" + (.start.line|tostring) + " - " + .extra.message' semgrep-results.json
                exit 1
            fi
    ```

    ![A screenshot of a computer Description automatically
    generated](./media/image24.png)

5.  Commit the file with message +++Add Semgrep workflow+++ and commit to
    the branch (**fix/Semgrep-rule-eval**) branch that you have created
    in the previous steps.

    ![A screenshot of a computer Description automatically
    generated](./media/image25.png)

6.  Navigate to **Actions** tab and make sure the workflow is successful.

    ![A screenshot of a computer Description automatically
    generated](./media/image26.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image27.png)

#### **Task 2: Triggering and Observing Semgrep on a Pull Request**

This step shows students how insecure code (like eval()) is
automatically detected by the Semgrep workflow. They learn how CI checks
block unsafe merges.

1.  In your repo, click the **Code** tab and switch again to
    **fix/semgrep-rule-eval** branch.

    ![A screenshot of a computer Description automatically
    generated](./media/image28.png)

2.  In that branch, click **Add file → Create new file**.

    ![A screenshot of a computer Description automatically
    generated](./media/image29.png)

3.  Name it +++bad.js+++ and **paste** the below code and **commit** the changes:

    +++eval("console.log('unsafe')");+++

    ![A screenshot of a computer Description automatically
    generated](./media/image30.png)

4.  Keep the copilot suggested commit message and commit directly to
    **fix/Semgrep-rule-eval** branch.

    ![A screenshot of a computer Description automatically
    generated](./media/image31.png)

5.  Navigate to **Actions** tab and observe the recent workflow which is
    failed to run.

    ![A screenshot of a computer Description automatically
    generated](./media/image32.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image33.png)

6.  In the run, click the job semgrep → expand Run semgrep and Fail on
    errors steps.

    ![A screenshot of a computer Description automatically
    generated](./media/image34.png)

7.  You’ll see JSON output and the printed findings.

8.  Scroll down → under Artifacts, click **semgrep-results** to download the
    JSON file.

**The purpose of adding eval() was to trigger the Semgrep rule.**

**This means Semgrep found something it considers an error and exited
with a non‑zero code (exit code 7). The failure is intentional in this
lab: it demonstrates that risky code (like eval()) blocks the PR from
merging. Branch protection rules will now enforce this — the PR cannot
be merged until the check passes (i.e., you remove or fix the insecure code).**

#### **Task 3: Adding Semgrep as a Required Status Check in Branch Protection**

1.  Go to your repo → click **Settings** (top menu).

2.  In the left sidebar, click **Branches**.

3.  Under **Branch protection rules**, click **Add classic branch protection rule**.

4.  In **Branch name pattern**, type main.

    ![A screenshot of a computer Description automatically
    generated](./media/image35.png)

5.  Scroll down → check **Require pull request reviews before merging**.

6.  Check **Require status checks to pass before merging**.

7.  Enter **Semgrep** as the status check (the name must match exactly what you saw in Actions).

8.  Scroll down → check **Require branches to be up to date before
    merging** and **Require conversation resolution before merging**.

Note: BY adding this, GitHub blocks merges until Semgrep passes. This
enforces your governance policy — unsafe code (like eval()) cannot be
merged into main. Once you do, any PR with risky code will show a red ❌
and merging will be blocked until the issue is fixed.

![A screenshot of a computer Description automatically
    generated](./media/image36.png)

9.  Click **Create** or **Save changes**.

    ![A screenshot of a computer Description automatically
    generated](./media/image37.png)
