# **Lab 02: Automate Docker Image Publishing with GitHub Actions**

You and your team have been working hard on an awesome web-based game
called **Stackoverflown**. It's a hit, and now you want to **package and
version** it for distribution so players everywhere can easily run it
and deploy it on their servers.

To make this happen efficiently, let's automate the process of packaging
new versions of your app using GitHub Actions! By automating the build
and deployment process, you will enable seamless versioning and
distribution of your application through the GitHub Container Registry.
This hands-on exercise demonstrates how modern DevOps practices simplify
application delivery and ensure consistency across environments.

## **Objectives**

- Set up a development environment using GitHub Codespaces

- Create a GitHub Actions workflow to build and publish Docker images

- Run and test the published Docker image locally

- Enhance workflows using official Docker actions

- Configure multiple triggers and metadata for dynamic image tagging

- Implement a feature using branching and commits

- Create and validate a Pull Request workflow

- Publish a release with version tagging

### **Exercise 1: Set up the development environment**

Let's use **GitHub Codespaces** to set up a cloud-based development
environment and work in it for the remainder of the exercise!

1.  Open the repository in your browser:
    +++https://github.com/skills/publish-docker-images+++ and select **Use this template** and choose **Create new repository.**

    ![A screenshot of a computer Description automatically
    generated](./media/image1.png)

2.  Enter the repository name as +++publish-docker-images+++ and enable
    **include all branches** toggle. Make sure repository visibility is
    set to **Public**.

    Click on **Create repository**.

    ![A screenshot of a computer Description automatically
    generated](./media/image2.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image3.png)

3.  Navigate to repository **settings**.

    ![A screenshot of a computer Description automatically
    generated](./media/image4.png)

4.  Expand **Actions** settings and then, select **General**.

    ![A screenshot of a computer Description automatically
    generated](./media/image5.png)

5.  Scroll down and Provide **Read and Write Permissions** to the
    workflow and Enable **Allow GitHub Actions to create and approve
    pull requests.**

    **Save** the configuration.

    ![A screenshot of a computer Description automatically
    generated](./media/image6.png)

6.  Navigate to the **Code** tab.

    ![A screenshot of a computer Description automatically
    generated](./media/image7.png)

7.  Select the **Code** dropdown and and **create codespace on main.**

    ![A screenshot of a computer Description automatically
    generated](./media/image8.png)

### **Exercise 2: Create Basic Docker Publish Workflow**

Let's start off by creating a workflow to build and publish
our **Stackoverflown** game as a docker image.

1.  In your codespace, within the **.github/workflows** directory.

    ![A screenshot of a computer Description automatically
    generated](./media/image9.png)

2.  Create a new workflow file named: +++docker-publish.yml+++

    ![A screenshot of a computer Description automatically
    generated](./media/image10.png)

3.  Within that file, let's start by defining the workflow name, event
    trigger and permissions:

    ```
    name: Docker Publish

    on:
    push:
        branches:
        - main

    permissions:
    contents: read
    packages: write
    ```

    This workflow will run on all commits pushed to the main branch with
    permissions to read the repository contents and push packages to the
    GitHub Container Registry.

    ![A screenshot of a computer Description automatically
    generated](./media/image11.png)

4.  Add the **build-and-push** job to the end of the file:

    **Important:** Replace **\<GITHUB_USERNAME\>** with your actual GitHub
    username in lowercase before running the workflow. For example, if
    your username is ContosoTech, use contosotech.

    ```
    jobs:
    build-and-push:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v6
      - name: Log in to the Container registry
        uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}
      - name: Build and push Docker image
        run: |
            docker build . --tag ghcr.io/<GITHUB_USERNAME>/publish-docker-images/stackoverflown:main
            docker push ghcr.io/<GITHUB_USERNAME>/publish-docker-images/stackoverflown:main

    ```

    This job checks out the repository code, authenticates to the GitHub
    Container Registry using GITHUB_TOKEN, builds the Docker image, and
    publishes it to the registry under your GitHub account.

    **Note**: The docker build follows the instructions in the
    **Dockerfile** file present in the repository on how to package the application.

    ![](./media/image12.png)

5.  Go to **Source Control** tab and add a **commit message** as +++Build workflow+++ and push
    your changes to the **main** branch.

    ![A screenshot of a computer Description automatically
    generated](./media/image13.png)

6.  Click **Yes** to stage all your changes and commit them directly to
    main branch.

    ![A screenshot of a computer Description automatically
    generated](./media/image14.png)

7.  **Sync** the committed changes.

    ![A screenshot of a computer Description automatically
    generated](./media/image15.png)

8.  Click **OK** to confirm.

    ![A screenshot of a computer Description automatically
    generated](./media/image16.png)

9.  When you push your changes, the workflow you just created should
    also run for the first time. Monitor it in the **Actions** tab
    and **ensure it completes successfully**.

    ![A screenshot of a computer Description automatically
    generated](./media/image17.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image18.png)

### **Exercise 3: Pull and run your docker image**

The commit from your previous step should have triggered the first run
of your workflow and published a Docker image to the GitHub Container
Registry.

Let's pull that image and run it in your codespace to see the game
running!

10. Go to your repository’s main page and on the right side, under
    the **Packages** section,
    click **skills-publish-docker-images/stackoverflown**

    ![A screenshot of a computer Description automatically
    generated](./media/image19.png)

11. **Copy** the command that starts with **docker pull ...**

    ![A screenshot of a computer Description automatically
    generated](./media/image20.png)

12. Back in your **codespace**, open the terminal and run that command
    
    (that you have copied in the previous step) in the terminal to download the image from the container registry.

    ![A screenshot of a computer Description automatically
    generated](./media/image21.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image22.png)

13. Verify the image is available locally by running:

    +++docker images+++

    ![A screenshot of a computer Description automatically
    generated](./media/image23.png)

14. Run the following command to start a container from your published
    image. **Replace \<github-username\> with your GitHub username in
    lowercase.**

    ```
    docker run -p 8080:80 ghcr.io/\<github-username\>/publish-docker-images/stackoverflown:main
    ```

    **Note:** replace your account name in the url and run the command.

    ![A screenshot of a computer Description automatically
    generated](./media/image24.png)

15. You will receive a notification to open the application in browser
    or You can access the application through the **Ports tab - on port 8080**

    ![A screenshot of a computer Description automatically
    generated](./media/image25.png)

16. This will open a new tab in your browser. Review the application.  
      
    ![A screenshot of a video game Description automatically
    generated](./media/image26.png)

17. You can stop the application from running by hitting **Ctrl + C** back in the terminal.

    ![A screenshot of a computer Description automatically
    generated](./media/image27.png)

### **Exercise 4: Leverage open source Docker Actions**

Let's edit the workflow to use the official Docker actions for a more
robust and feature-rich build process.

18. Open the **.github/workflows/docker-publish.yml** file.

19. Remove your existing **Build and push Docker image** step
    with docker commands. We will replace that with open source actions.

    Caution:** Only remove the Build and push Docker image step. Do **not** remove the steps with actions/checkout and docker/login-action actions.**

    ![](./media/image28.png)

20. Now, add these following three steps in place of the Build and push
    Docker image step you just removed.

    These steps will set up QEMU for multi-architecture builds, set up
    Docker Buildx, and then build and push the Docker image with two
    different tags.

    **Important Note: Replace \<github-username\> with your GitHub username in lowercase before saving the file.**

    ```
    - name: Set up QEMU
      uses: docker/setup-qemu-action@v3
    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v3
    - name: Build and push Docker image
      uses: docker/build-push-action@v6
      with:
        context: .
        push: true
        platforms: linux/amd64,linux/arm64
        tags: |
        ghcr.io/<github-username>/publish-docker-images/stackoverflown:main
        ghcr.io/<github-username>/publish-docker-images/stackoverflown:${{ github.sha }}
    ```

    Ensure the **yaml** indentation is setup correctly!

    **Tip:** You can run actionlint command in the terminal to see if the
    workflow is properly formatted.

    In case you need it, here is the full content of the updated workflow file:

    ```
    name: Docker Publish

    on:
    push:
        branches:
        - main

    permissions:
    contents: read
    packages: write

    jobs:
    build-and-push:
        runs-on: ubuntu-latest
        steps:
        - uses: actions/checkout@v6
        - name: Log in to the Container registry
            uses: docker/login-action@v3
            with:
            registry: ghcr.io
            username: ${{ github.actor }}
            password: ${{ secrets.GITHUB_TOKEN }}
        - name: Set up QEMU
            uses: docker/setup-qemu-action@v3

        - name: Set up Docker Buildx
            uses: docker/setup-buildx-action@v3

        - name: Build and push Docker image
            uses: docker/build-push-action@v6
            with:
            context: .
            push: true
            platforms: linux/amd64,linux/arm64
            tags: |
                ghcr.io/contosotech/publish-docker-images/stackoverflown:main
                ghcr.io/contosotech/publish-docker-images/stackoverflown:${{ github.sha }}
    ```

    ![](./media/image29.png)

21. Navigate to **Source Control** and add a **commit message** as +++Set up Docker Buildx+++ to push your changes to   the **main** branch.

    ![](./media/image30.png)

22. Monitor your workflow run in the **Actions** tab of your repository
    and select **Docker Publish** from the left pane. **Ensure the
    workflow completes successfully**.

    ![A screenshot of a computer Description automatically
    generated](./media/image31.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image32.png)

### **Exercise 5: Adding additional triggers and metadata action**

Let's update our workflow to support multiple triggers and use the
metadata action for dynamic docker image tagging.

1.  Navigate to the codespace. Edit
    the **.github/workflows/docker-publish.yml** file and update the
    event triggers part of the workflow to include all of the following
    triggers.

    ```
    on:
      push:
        branches:
        - main
        tags:
        - "v*"
      pull_request:
        branches:
        - main
      workflow_dispatch:
    ```

    ![](./media/image33.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image34.png)

2.  Add a step to extract metadata for Docker images

    **Important Note: Place it before the docker/build-push-action step.
    Replace \<github-username\> with your GitHub username in lowercase.**

    ```
    - name: Extract metadata for Docker
      id: meta
      uses: docker/metadata-action@v5
      with:
        images: ghcr.io/<github-username>/publish-docker-images/stackoverflown
    ```

    ![A screenshot of a computer Description automatically
    generated](./media/image35.png)

3.  Update the **docker/build-push-action** step to use the generated
    tags.

    ```
    - name: Build and push Docker image
      uses: docker/build-push-action@v5
      with:
        context: .
        push: true
        platforms: linux/amd64,linux/arm64
        tags: ${{ steps.meta.outputs.tags }}
    ```

    Ensure the yaml indentation is setup correctly!

    ![A screenshot of a computer Description automatically
    generated](./media/image36.png)

4.  Go to **Source Control** tab and add a **commit message** - +++Add Docker metadata+++ and **commit** and push your changes to
    the main branch.

    ![A screenshot of a computer Description automatically
    generated](./media/image37.png)

5.  Click **Yes** to stage all your changes and commit them directly.

    ![A screenshot of a computer Description automatically
    generated](./media/image38.png)

6.  **Sync** the committed changes.

    ![A screenshot of a computer Description automatically
    generated](./media/image39.png)

7.  Click **OK** to confirm.

    ![A screenshot of a computer Description automatically
    generated](./media/image40.png)

8.  Go to **Actions** tab and review the recent workflow as **Add Docker metadata.** Make sure it’s successful.

    ![A screenshot of a computer Description automatically
    generated](./media/image41.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image42.png)

### **Exercise 6: Add a feature**

Let's start off by adding a simple code change to our source code.

1.  Go to your codespace. Start by switching to a new branch
    called **feature/add-high-score**:

    +++git branch feature/add-high-score+++

    +++git checkout feature/add-high-score+++

    ![A screenshot of a computer Description automatically
    generated](./media/image43.png)

2.  Open the **src/index.html** file.

    ![A screenshot of a computer Description automatically
    generated](./media/image44.png)

3.  At line 20, replace the **info-section** area about scoring with the
    below example.

    ```
    <div class="info-section">
       <h3>Current Score</h3>
       <div class="score" id="score">0</div>
       <h3>High Score</h3>
       <div class="high-score" id="high-score">0</div>
    </div>
    ```

    This will demonstrate 3 kinds of changes:

    - Modify the Score label to Current Score

    - Add the High Score information.

    - Remove the status information.

    ![A screenshot of a computer Description automatically
    generated](./media/image45.png)

4.  Open your terminal and run these command to commit and push your
    changes to the **feature/add-high-score** branch:

    +++git add src/index.html+++

    **(This will stage the file for the next commit)**

    ![A screenshot of a computer Description automatically
    generated](./media/image46.png)

    +++git commit -m "Add high score display+++

    **(It creates a commit with the changes you previously staged)**

    ![A screenshot of a computer Description automatically
    generated](./media/image47.png)

    +++git push -u origin feature/add-high-score+++

    **(It pushes your local branch to GitHub and sets it as the default upstream branch)**

    ![A screenshot of a computer Description automatically
    generated](./media/image48.png)

### **Exercise 7: Create a pull request**

Now that you have your feature branch ready, let's create a Pull Request
to see if your workflow builds the image with the appropriate pr-X tag.

1.  In a new browser tab, navigate to the **Pull Requests** tab of your
    repository.

    ![A screenshot of a computer Description automatically
    generated](./media/image49.png)

2.  Create a Pull Request targeting main branch from the branch you just created.

    **Wait: Don't merge it yet!**

    ![A screenshot of a computer Description automatically
    generated](./media/image50.png)

3.  Go to the **Actions** tab and watch the Docker Publish workflow run
    triggered by the Pull Request.

    - This run will build the image with the pr-X tag (e.g., pr-2).

    ![](./media/image51.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image52.png)

4.  Once the workflow finishes successfully verify the image is present
    in the **Packages** section of your repository on the **Code** tab.

    ![A screenshot of a computer Description automatically
    generated](./media/image53.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image54.png)

5.  You can pull and run the image in your codespace to see the changes in action before merging!

    **Important Note: Replace \<github-username\> with your GitHub
    username in lowercase and \<PR_NUMBER\> with your actual Pull Request number.**

    ```
    docker run -d -p 8080:80 ghcr.io/\<github-username\>/publish-docker-images/stackoverflown:pr-\<PR_NUMBER\>
    ```

    ![A screenshot of a computer Description automatically
    generated](./media/image55.png)

    You can access the application through the **Ports tab - on port 8080.** 

    ![A screenshot of a computer Description automatically
    generated](./media/image56.png)

6.  See the new high score feature!

    ![A screenshot of a game Description automatically
    generated](./media/image57.png)

### **Exercise 8: Merge the pull request and create a release**

Alright! Now let's merge the pull request and create a stable release
with a proper version tag.

1.  Go back to the **Pull Request** and **merge** it into main.

    **Note: This will also trigger a new Docker Publish workflow run**

    ![A screenshot of a computer Description automatically
    generated](./media/image58.png)

2.  **Confirm** the merge.

    ![A screenshot of a computer Description automatically
    generated](./media/image59.png)

3.  Go to the **Code** tab of your repository and click on **Create a
    new** **release** (on the right sidebar).

    ![A screenshot of a computer Description automatically
    generated](./media/image60.png)

4.  Enter the details for a new release:

    - Choose a tag: Enter +++v1.0.0+++ (Create new tag)

    ![A screenshot of a computer Description automatically
    generated](./media/image61.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image62.png)

    - Target: **main**

    ![A screenshot of a computer Description automatically
    generated](./media/image63.png)

    - **Release Title**: +++v1.0.0+++

    ![A screenshot of a computer Description automatically
    generated](./media/image64.png)

    - **Release notes:** +++First official release with high score tracking!+++

    ![A screenshot of a computer Description automatically
    generated](./media/image65.png)

5.  At the bottom, click the **Publish release** button.

    ![A screenshot of a computer Description automatically
    generated](./media/image66.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image67.png)

6.  Go to the **Actions** tab one last time. You should see a workflow
    run triggered by the new tag.

    - This run will build the image with the v1.0.0 tag.

    ![A screenshot of a computer Description automatically
    generated](./media/image68.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image69.png)

7.  Once the workflow finishes successfully verify the
    image v1.0.0 image is present in the **Packages** section of your
    repository.

    ![A screenshot of a computer Description automatically
    generated](./media/image70.png)

    ![A screenshot of a computer Description automatically
    generated](./media/image71.png)

## **Conclusion**

In this lab, you successfully automated the process of building,
tagging, and publishing Docker images using GitHub Actions. You also
practiced branching, pull requests, and release management to simulate a
real-world development workflow. This end-to-end experience highlights
how CI/CD pipelines improve efficiency, maintain consistency, and
support scalable application deployment.
