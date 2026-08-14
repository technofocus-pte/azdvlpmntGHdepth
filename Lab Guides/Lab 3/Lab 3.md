---
lab:
  title: 'Lab 03: Build, Automate & Deploy a Task Manager App using GitHub Copilot'
  description: This lab provides a comprehensive understanding of how modern development teams build, automate, and deploy applications using DevOps practices. By integrating AI-assisted coding with CI/CD pipelines and deployment strategies, you experienced how to accelerate development while maintaining quality and control. The use of GitHub for version control, automation, and hosting demonstrates how a single platform can support the entire software delivery lifecycle, preparing you for real-world development and deployment scenarios.
  duration: 162 minutes
  level: 300
  islab: true
  primarytopics:
    - GitHub
---

# Lab 03: Build, Automate & Deploy a Task Manager App using GitHub Copilot

Zava, a fast-growing digital health company, is planning to launch a
lightweight Task Manager application to streamline internal team
operations and improve productivity across departments. As part of the
engineering team, you are responsible for building this application
using modern development practices. To accelerate delivery and maintain
high quality, Zava adopts AI-assisted development with GitHub Copilot
and implements a complete DevOps workflow using GitHub. In this lab, you
will simulate this real-world scenario by planning tasks, developing
backend and frontend components, automating CI/CD pipelines, and
deploying the application to a live environment with controlled
approvals.

## **Objectives:**

- Plan and manage project tasks using GitHub Issues and Projects

- Implement a branching strategy for collaborative development

- Build backend and frontend components using AI assistance (Copilot)

- Create and manage pull requests with automated code reviews

- Configure a CI workflow using GitHub Actions

- Debug and fix pipeline failures effectively

- Upload and manage build artifacts in workflows

- Deploy the frontend application using GitHub Pages

### **Exercise 1: Project Setup and Planning**

#### **Task 1: Create a Repository in GitHub**

1.  Sign in to your +++https://github.com/+++ account.

2.  Click **"+" (top-right corner)** and select **"New repository"**.

    ![A screenshot of a computer Description automatically
    generated](./media/image1.png)

3.  Fill details:

- Enter **Repository name** → +++task-manager-ai+++

- Add **Description (optional)** → +++Task Manager with AI features+++

- Select repository visibility as **Public**

- Add a README file

    Click **Create repository.**

    ![A screenshot of a computer Description automatically
    generated](./media/image2.png)

#### **Task 2: Enable Issues and Projects**

1.  Go to **Settings** tab from the top menu in the repository.

    ![A screenshot of a computer Description automatically
    generated](./media/image3.png)

2.  In the **General** section, scroll to **Features** section and
    check **Issues** checkbox.

    ![A screenshot of a computer Description automatically
    generated](./media/image4.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image5.png)

3.  Similarly, also enable to **Projects** Feature.

    ![A screenshot of a computer Description automatically
    generated](./media/image6.png)

#### **Task 3: Create Issues in the repository**

1.  Navigate to **Issues** tab from the top menu and **create a new issue**.

    **Note:** You will be creating 4 issues in the further steps.

    ![A screenshot of a computer Description automatically
    generated](./media/image7.png)

2.  Enter the **Issue title** as +++Task API+++ and **description** as
    +++Build backend API for task management (CRUD operations)+++.

    Click on **Create**.

    ![A screenshot of a computer Description automatically
    generated](./media/image8.png)

3.  Proceed with creating the **second** **issue** by clicking on **New issue** button.

    ![A screenshot of a computer Description automatically
    generated](./media/image9.png)

4.  Enter the **Issue title** as +++UI Page+++ and **description** as
    +++Create frontend UI for task manager+++

    Click on **Create**.

    ![A screenshot of a computer Description automatically
    generated](./media/image10.png)

5.  Create **third** **issue**.

    ![A screenshot of a computer Description automatically
    generated](./media/image11.png)

6.  Enter the **Issue title** as +++Add Tests+++ and **description** as
    +++Add unit and integration tests+++

    Click on **Create**.

    ![A screenshot of a computer Description automatically
    generated](./media/image12.png)

7.  Create **fourth issue**.

    ![A screenshot of a computer Description automatically
    generated](./media/image13.png)

8.  Enter the **Issue title** as +++Deploy App+++ and **description** as
    +++Deploy application to cloud platform+++

    Click on **Create**.

    ![A screenshot of a computer Description automatically
    generated](./media/image14.png)

9.  You have created four issues.

    ![A screenshot of a computer Description automatically
    generated](./media/image15.png)

#### **Task 4: Create Project Board**

1.  Navigate to **Projects** tab from the top menu and **create a new project**.

    ![A screenshot of a computer Description automatically
    generated](./media/image16.png)

2.  Select **Board** option.

    ![A screenshot of a search engine Description automatically
    generated](./media/image17.png)

3.  **Rename** the project as +++Task Manager Board+++ and click **Create project**.

    ![A screenshot of a computer Description automatically
    generated](./media/image18.png)

4.  By default, project board creates columns – **Todo/ In progress/Done.**

    **Notice that Issues are already linked to your project.**

    ![A screenshot of a computer Description automatically
    generated](./media/image19.png)

#### **Task 5: Setup Branch Strategy**

1.  Go back to the **Projects** tab.

    ![A screenshot of a computer Description automatically
    generated](./media/image20.png)

2.  Navigate to **Repositories** tab and select **Task-Manager-ai**
    repository.

    ![A screenshot of a computer Description automatically
    generated](./media/image21.png)

3.  Make sure you are on the **Code** tab. Expand the **main** branch
    dropdown.

    ![A screenshot of a computer Description automatically
    generated](./media/image22.png)

4.  In the search box, type +++feature/backend+++

    You’ll see – **Create branch: feature/backend from ‘main’. Click that option.**

    ![A screenshot of a computer Description automatically
    generated](./media/image23.png)

5.  Backend Branch created successfully.

    ![A screenshot of a computer Description automatically
    generated](./media/image24.png)

6.  Click the **branch** **dropdown** again and first select **main**
    branch and then, type +++feature/frontend+++

    Click – **Create branch: feature/frontend from ‘main’.**

    ![A screenshot of a computer Description automatically
    generated](./media/image25.png)

7.  Frontend branch is created successfully.

    ![A screenshot of a computer Description automatically
    generated](./media/image26.png)

8.  Go to **Settings** tab from the top menu and select **Branches**
    from the sidebar.

    Under **Branch protection rules**, select **Add branch** ruleset.

    ![A screenshot of a computer Description automatically
    generated](./media/image27.png)

9.  Enter **ruleset** **name** as +++Protect main branch+++

    ![A screenshot of a computer Description automatically
    generated](./media/image28.png)

10. Under **Target branches** dropdown, select **Include by pattern**.

    ![A screenshot of a computer Description automatically
    generated](./media/image29.png)

11. Enter +++main+++ branch as naming pattern and click **Add inclusion pattern**.

    ![A screenshot of a computer Description automatically
    generated](./media/image30.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image31.png)

12. Enable **Require Pull request before merging**.

    ![A screenshot of a computer Description automatically
    generated](./media/image32.png)

13. **Create** the ruleset.

    ![A screenshot of a computer Description automatically
    generated](./media/image33.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image34.png)

You now have the **protected main** branch and two new branches –
**feature/backend** and **feature/frontend.**

### **Exercise 2: Build Application using Copilot**

#### **Task 1: Build Backend (AI-assisted)**

1.  Navigate to the **Code** tab and switch the branch to **feature/backend**.

    ![A screenshot of a computer Description automatically
    generated](./media/image35.png)

2.  From the **Code** dropdown, create a **new codespace**.

    ![A screenshot of a computer Description automatically
    generated](./media/image36.png)

3.  Wait for a few minutes to load all the dependencies and packages.

    ![A screenshot of a computer Description automatically
    generated](./media/image37.png)

4.  Navigate to **Extensions** tab from the left pane and make sure **GitHub Copilot** extension is installed. 

    ![A screenshot of a chat Description automatically
    generated](./media/image38.png)

5.  Again, navigate to **Explorer** tab and create **a new folder** and
    name it as +++backend+++

    ![A screenshot of a computer Description automatically
    generated](./media/image39.png)

6.  Select the folder and click on **new file** option and name it as +++app.js+++

    ![A screenshot of a computer Description automatically
    generated](./media/image40.png)

7.  Open **app.js** file and enter this **comment**:

    +++// Create an Express API for task management with GET and POST endpoints+++

    ![A screenshot of a computer Description automatically
    generated](./media/image41.png)

8.  Press **Enter** to see the copilot’s suggestions and press **Tab**
    to accept the suggestions. Your code should look similar as it is in
    the image below.

    ![](./media/image42.png)

9.  Open the **Terminal** and install **Express** by running the below
    command:

    +++npm install express+++

    ![](./media/image43.png)

10. Make sure **express** is imported in app.js file by adding the below
    code as the first line of your file: (Ignore if it’s already there)

    +++const express = require('express');+++

    ![](./media/image44.png)

11. Now, run the application:

    +++node backend/app.js+++

    You should see something like**: Server running on port 3000**

    ![A screenshot of a computer Description automatically
    generated](./media/image45.png)

12. Go to **Source Control** icon (left sidebar) and you’ll see changes
    in **backend/app.js** and **package.json**

    ![](./media/image46.png)

13. Enter commit message: +++Add backend API+++ and commit the changes.

    ![A screenshot of a computer Description automatically
    generated](./media/image47.png)

14. Click **Yes** to stage all you changes and commit them directly.

    ![A screenshot of a computer Description automatically
    generated](./media/image48.png)

15. **Sync** the committed changes.

    ![A screenshot of a computer Description automatically
    generated](./media/image49.png)

16. Click **OK** to confirm.

    ![A screenshot of a computer Description automatically
    generated](./media/image50.png)

17. Go to the GitHub repository and you’ll receive a **pull request**
    notification.

    ![](./media/image51.png)

18. Keep the title as it is and create a pull request.

    ![A screenshot of a computer Description automatically
    generated](./media/image52.png)

19. After creating the pull request, select **Copilot** under the
    **Reviewers**. Here, we are requesting copilot for the review before
    merging the pull request.

    ![](./media/image53.png)

20. After a few minutes, copilot will review and suggest the changes.
    You can either commit the suggestions or resolve the conversation if
    you don’t want to commit.

    ![A screenshot of a computer Description automatically
    generated](./media/image54.png)

21. You can now proceed with **merging** the pull request.

    ![A screenshot of a computer Description automatically
    generated](./media/image55.png)

22. Confirm the merge.

    ![A screenshot of a chat Description automatically
    generated](./media/image56.png)

23. Pull request successfully merged and closed.

    ![A screenshot of a computer Description automatically
    generated](./media/image57.png)

#### **Task 2: Build Frontend (AI-assisted)**

1.  Navigate to your **codespace** again and change the branch to **feature/frontend**.  
    To change the branch, select **feature/backend** branch from the bottom left corner.

    ![A screenshot of a computer Description automatically
    generated](./media/image58.png)

2.  Then, switch to **feature/frontend** branch. Notice the branch name
    changed to frontend in the bottom left corner. Also, you can open a
    new terminal see the branch name you are associated with.

    ![A screenshot of a computer Description automatically
    generated](./media/image59.png)

    ![](./media/image60.png)

3.  Create **a new folder** named +++frontend+++ just like you did in the
    previous task for backend.

    ![A screenshot of a computer Description automatically
    generated](./media/image61.png)

4.  Under the **frontend** folder, create a file named as +++index.html+++

    ![A screenshot of a computer Description automatically
    generated](./media/image62.png)

5.  Open **Copilot chat** and make sure **Agent** mode is selected.
    Write the prompt as:

    +++Create a simple UI to add and list tasks using JavaScript+++

    ![A screenshot of a computer Description automatically
    generated](./media/image63.png)

6.  Copilot will add the related code in index.html file. Keep the
    changes.

    ![A screenshot of a computer Description automatically
    generated](./media/image64.png)

7.  Navigate to **Source Control** tab. Add a **commit message** as
    +++Add frontend UI+++ and **commit** the changes.

    ![A screenshot of a computer program Description automatically
    generated](./media/image65.png)

8.  Click **Yes** to stage all your changes and commit them directly.

    ![A screenshot of a computer Description automatically
    generated](./media/image66.png)

9.  **Sync** the committed changes.

    ![A screenshot of a computer Description automatically
    generated](./media/image67.png)

10. Click **OK** to confirm.

    ![A screenshot of a computer Description automatically
    generated](./media/image68.png)

11. Switch to the **GitHub repository** and create a **pull request**.

    ![A screenshot of a computer Description automatically
    generated](./media/image69.png)

12. Keep the title as it is and create a pull request.

    ![A screenshot of a computer Description automatically
    generated](./media/image70.png)

13. Before merging the pull request, you can get it reviewed with
    copilot. Click **Request** under **Reviewers**.

    ![A screenshot of a computer Description automatically
    generated](./media/image71.png)

14. Copilot will share the review feedback. You can commit the
    suggestions or merge the pull request directly.

    ![A screenshot of a computer Description automatically
    generated](./media/image72.png)

15. **Merge** the pull request.

    ![A screenshot of a computer Description automatically
    generated](./media/image73.png)

16. **Confirm** the merge. Here, you’ll be merging the frontend into the
    main branch.

    ![A screenshot of a computer Description automatically
    generated](./media/image74.png)

17. Pull request is successfully merged and closed.

    ![A screenshot of a computer Description automatically
    generated](./media/image75.png)

### **Exercise 3: CI/CD with GitHub Actions** 

#### **Task 1: Generate workflow using Copilot**

1.  For this task, you need to switch to the **feature/backend** branch again. Run the below command:

    +++git checkout feature/backend+++

    ![](./media/image76.png)

2.  Create a new folder as +++.github+++

    ![A screenshot of a computer Description automatically
    generated](./media/image77.png)

3.  Again, under .github folder – create another folder as +++workflows+++

    ![A screenshot of a computer Description automatically
    generated](./media/image78.png)

4.  Under the workflows folder, create a new file as +++ci.yml+++

    ![A screenshot of a computer Description automatically
    generated](./media/image79.png)

5.  Open copilot chat and enter the prompt:

    ```
    Create a simple GitHub Actions CI workflow for a Node.js app.
    The project has no tests or build step.
    It should:
    - Run on push to main
    - Install dependencies
    - Run a basic node command to verify the app
    ```

    ![A screenshot of a computer Description automatically
    generated](./media/image80.png)

6.  **Keep** the file changes and review the code generated by copilot
    that it must have trigger on push, Install dependencies and run
    build.

    ![A screenshot of a computer Description automatically
    generated](./media/image81.png)

7.  Navigate to **Source control** tab. Add the commit message –
    +++Added CI workflow+++ and commit the changes.

    ![A screenshot of a computer Description automatically
    generated](./media/image82.png)

8.  Click **Yes** to stage all your changes and commit them directly.

    ![A screenshot of a computer Description automatically
    generated](./media/image83.png)

9.  **Sync** the changes.

    ![A screenshot of a computer Description automatically
    generated](./media/image84.png)

10. Click **OK** to confirm.

    ![A screenshot of a computer Description automatically
    generated](./media/image85.png)

11. Create a pull request.

    ![](./media/image86.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image87.png)

12. Merge the pull request.

    ![A screenshot of a computer Description automatically
    generated](./media/image88.png)

#### **Task 2: Break the pipeline**

13. Once the pull request is merged, go to **Actions** tab check if the
    CI workflow is successful.

    ![A screenshot of a computer Description automatically
    generated](./media/image89.png)

14. Navigate to the Codespace again and open **ci.yml** file and add
    these below code at the end of the file.

    ```
    - name: Break the pipeline intentionally
      run: exit 1
    ```

    ![A screenshot of a computer Description automatically
    generated](./media/image90.png)

15. Add a **commit message** and **commit** the changes like you did
    previously.

16. Open a **pull request** and **merge** the changes.

    ![A screenshot of a computer Description automatically
    generated](./media/image91.png)

    ![A screenshot of a chat Description automatically
    generated](./media/image92.png)

17. Once merged, navigate to the **Actions** tab and you’ll see the **Action
    failure** because of the exit code 1.

    ![A screenshot of a computer Description automatically
    generated](./media/image93.png)

18. Now, open the **copilot chat** in your **codespace** and enter the
    below prompt:

    +++Why did my workflow fail and how to fix it?+++

    ![A screenshot of a computer Description automatically
    generated](./media/image94.png)

19. Copilot will let you know the reason of the failure and to fix – it
    will tell you to update the file and remove the added code. Make
    sure you keep the file changes.

    ![A screenshot of a computer Description automatically
    generated](./media/image95.png)

20. Now, again you can **commit** the changes to verify the Actions.

    ![A screenshot of a computer Description automatically
    generated](./media/image96.png)

21. Open a pull request and merge the changes.

    ![A screenshot of a computer Description automatically
    generated](./media/image97.png)

    ![A screenshot of a chat Description automatically
    generated](./media/image98.png)

22. Navigate to the **Actions** tab again and you’ll the succeeded status on
    the recent action. Surprisingly, Copilot can fix the errors as well!

    ![A screenshot of a computer Description automatically
    generated](./media/image99.png)

### **Exercise 4: Deploy to Production**

#### **Task 1: Deploy Frontend to GitHub Pages**

Host your **frontend/index.html** live using GitHub Pages.

1.  Navigate to **Code** tab and edit the **ci.yml** file.

    ![A screenshot of a computer Description automatically
    generated](./media/image102.png)

2.  **Add deployment step**. Add the below code at the end of **steps**:

    ```
    - name: Deploy Pages
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./frontend
    ```

    ![A screenshot of a computer Description automatically
    generated](./media/image103.png)

3.  Add this at the **top of file** below **name**. Without this the
    deployment will fail.

    ```
    permissions:
      contents: write
    ```

    ![A screenshot of a computer Description automatically
    generated](./media/image104.png)

4.  **Commit** the changes and write the **commit message** as: +++Add GitHub Pages deployment and create a pull request+++

    ![A screenshot of a computer Description automatically
    generated](./media/image105.png)

5.  **Merge** the pull request.

    ![A screenshot of a chat Description automatically
    generated](./media/image106.png)

6.  Go to **settings** and select **Pages** section. Under Deploy from
    branch, select **gh-pages** branch from the dropdown. **Save** the
    changes.

    ![A screenshot of a computer Description automatically
    generated](./media/image107.png)

7.  Navigate to **Actions** tab and select the recent **pages build and deployment** workflow.

    ![A screenshot of a computer Description automatically
    generated](./media/image108.png)

8.  Once the status shows succeeded, click the deployed url similar to
    +++https://\your-username.github.io/task-manager-ai/+++

    ![A screenshot of a computer Description automatically
    generated](./media/image109.png)

9.  This will open a new tab in your browser and you’ll that **FRONTEND IS LIVE**!

    ![A screenshot of a computer Description automatically
    generated](./media/image110.png)

## **Conclusion**

This lab provides a comprehensive understanding of how modern
development teams build, automate, and deploy applications using DevOps
practices. By integrating AI-assisted coding with CI/CD pipelines and
deployment strategies, you experienced how to accelerate development
while maintaining quality and control. The use of GitHub for version
control, automation, and hosting demonstrates how a single platform can
support the entire software delivery lifecycle, preparing you for
real-world development and deployment scenarios.
