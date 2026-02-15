# Lab 05: Code with Codespaces and Visual Studio Code

In this lab, you’ll explore how GitHub Codespaces and Visual Studio Code
work together to provide a cloud-based development environment. You’ll
create and manage a Codespace, make code changes directly in VS Code,
and learn how to customize and personalize your development setup to
improve productivity and consistency.

### **Objective:**

- Create and launch a GitHub Codespace from a repository

- Use Visual Studio Code within a Codespace to edit and manage code

- Commit and push code changes from a Codespace to GitHub

- Configure a custom development container using devcontainer.json

- Customise a Codespace with extensions and startup settings

- Execute commands automatically when a Codespace is created

- Personalise the development environment using dotfiles

## **Task 1: Start a Codespace**

1. Sign in to GitHub with your GitHub account.

2. Browse to the following repository- +++https://github.com/skills/code-with-codespaces.git+++

    ![A screenshot of a computer Description automatically
    generated](./media/image1.png)

3. Navigate to **Code** menu and create a **new Codespace** on the main branch.

    ![A screenshot of a computer Description automatically
    generated](./media/image2.png)

4.  Wait about 2 minutes for the Codespace to spin itself up. It's a
    virtual machine spinning up in the background.

    ![A screenshot of a computer Description automatically
    generated](./media/image3.png)

5.  Once the Codespace is ready, select the **src** folder from the
    explorer in the left pane.

  ![A screenshot of a computer Description automatically
  generated](./media/image4.png)

6.  Create a **new file** under the src folder.

    ![A screenshot of a computer Description automatically
    generated](./media/image5.png)

## **Task 2: Push code to your repository from the Codespace**

1. Enter the file name as +++index.html+++

  ![](./media/image6.png)

2. Select the **index.html** file. Enter the code below:

  ```
  <html>
  <h1> Hello from the codespace!</h1>
  </html>
  ```

**Note**: The file should autosave.

    ![A screenshot of a computer Description automatically
    generated](./media/image7.png)

3.  Once the code is added, navigate to **Source control** tab from the
    left pane.

  ![A screenshot of a computer Description automatically
  generated](./media/image8.png)

4. Enter commit message as +++updated index.html+++ and commit the changes.

    ![](./media/image9.png)

5.  Select **Yes** to stage all your changes and commit them directly.

  ![](./media/image10.png)

6.  Sync the changes.

  ![A screenshot of a computer Description automatically
  generated](./media/image11.png)

7.  Click on **OK** to confirm.

  ![](./media/image12.png)

8.  Navigate to **GitHub repository** and select **src** folder.

  ![A screenshot of a computer Description automatically
  generated](./media/image13.png)

9.  View the **index.html** to verify that the new code was pushed to
    your repository.

  ![A screenshot of a computer Description automatically
  generated](./media/image14.png)

10. You can see the code is now successfully pushed to the repository.

  ![A screenshot of a computer Description automatically
  generated](./media/image15.png)

11. Select the **repository name** to switch back to the main page.

  ![A screenshot of a computer Description automatically
  generated](./media/image16.png)

## **Task 3: Add a custom image to your Codespace**

*You created your first codespace and pushed code using VS Code!*

You can configure the development container for a repository so that any
codespace created for that repository will give you a tailored
development environment, complete with all the tools and runtimes you
need to work on a specific project.

**What are development containers?** Development containers, or dev
containers, are Docker containers that are specifically configured to
provide a fully featured development environment. Whenever you work in a
codespace, you are using a dev container on a virtual machine.

A dev container file is a JSON file that lets you customise the default
image that runs your codespace, VS Code settings, run custom code,
forward ports and much more!

Let's add a devcontainer.json file and add a custom image.

1.  On the repository’s homepage, click on **Add file** dropdown.

  ![](./media/image17.png)

2.  Select the **Create new file** option from the dropdown menu.

  ![](./media/image18.png)

3.  Enter the folder name as **.devcontainer** followed by a slash **/**
    to enter the file name in the next step. Hence, you need to enter
    the folder name as:

    +++.devcontainer/+++
 
    ![A screenshot of a computer Description automatically
    generated](./media/image19.png)
    
    ![A screenshot of a computer Description automatically
    generated](./media/image20.png)

4.  Now, enter +++devcontainer.json+++ as the file name.

    ![A screenshot of a computer Description automatically
    generated](./media/image21.png)

5.  In the body of the new **.devcontainer/devcontainer.json** file, add
    the following content. Click **Commit changes**.

    ```
    {
    // Name this configuration
    "name": "Codespace for Skills!",
    // Use the base codespace image
    "image": "mcr.microsoft.com/vscode/devcontainers/universal:latest",
    "remoteUser": "codespace",
    "overrideCommand": false
    }
    ```
 
  ![](./media/image22.png)

6.  Copilot has already generated the **commit message**. Then, select
    **commit changes** button.

  ![](./media/image23.png)

## **Task 4: Customise your Codespace- Add customisations to the devcontainer file**

You created a codespace with a custom image!

You can customise your codespace by adding VS Code extensions, adding
features, setting host requirements, and much more.

Let's customise some settings in the devcontainer.json file!

1.  Navigate to the **.devcontainer/devcontainer.json** file. Click on
    **Edit.**

  ![A screenshot of a computer Description automatically
  generated](./media/image24.png)

2.  Add the following customisations to the body of the file **before
    the** **last curly bracket }**. Click **Commit changes** 

    ```
    // Add the IDs of extensions you want installed when the container is created.
    "customisations": {
        "vscode": {
            "extensions": [
                "GitHub.copilot"
            ]
        },
        "codespaces": {
            "openFiles": [
                "codespace.md"
            ]
        }
    }
    ```
  ![](./media/image25.png)

3.  Select **Commit changes directly to the main branch**.

  ![](./media/image26.png)

4.  Click on the **repository name** to switch back to the main page.

  ![A screenshot of a computer Description automatically
  generated](./media/image27.png)

5.  Expand the **Code** section.

  ![A screenshot of a computer Description automatically
  generated](./media/image28.png)

6.  Create a **New Codespace** by clicking **+** icon.

  ![A screenshot of a computer Description automatically
  generated](./media/image29.png)

7.  Wait about **2 minutes** for the codespace to spin itself up.

  ![A screenshot of a computer Description automatically
  generated](./media/image30.png)

8.  Once the codespace is ready, navigate to the **Extensions** tab.

  ![A screenshot of a computer Description automatically
  generated](./media/image31.png)

9.  Search for **GitHub Copilot** in the extensions search bar and make sure this extension is installed.

  ![](./media/image32.png)

Next, let’s add some code to run upon creation of the codespace!

## **Task 5: Execute code upon creation of the codespace**

1.  Navigate to the GitHub repository and **edit**
    the **devcontainer.json** file.

  ![A screenshot of a computer Description automatically
  generated](./media/image33.png)

2.  Add the following **postCreateCommand** to the body of the file
    **before the last curly bracket }.** After that, **commit** the
    changes.

    ```
    ,
    "postCreateCommand": "echo '# Writing code upon codespace creation!'
    \ \  codespace.md"
    ```

    ![A screenshot of a computer Description automatically
    generated](./media/image34.png)

3.  With the commit message, click on **commit changes**.

    ![](./media/image35.png)

## Task 6: Personalise your codespace- Enable a dotfile for your codespace

When using any development environment, customising the settings and
tools to your preferences and workflows is an important step. GitHub
Codespaces offers two main ways of personalising your
codespace: Settings Sync with VS Code and dotfiles.

Dotfiles will be the focus of this activity.

**What are dotfiles?** Dotfiles are files and folders on Unix-like systems
starting with . that control the configuration of applications
and shells on your system. You can store and manage your dotfiles in a
repository on GitHub.

Let's see how this works!

1.  Start from the landing page of your repository. In the upper-right
    corner of any page, click your profile icon, and then
    click **Settings**.

  ![](./media/image36.png)

2.  In the **Code, planning, and automation** section of the sidebar,
    click **Codespaces**.

  ![](./media/image37.png)

3.  Under **Dotfiles**, select **Automatically install dotfiles** so
    GitHub Codespaces automatically installs your dotfiles into
    every new codespace you create.

  ![A screenshot of a computer Description automatically
  generated](./media/image38.png)

4.  Click **Select repository** and then choose your current skills
    working repository as the repository from which to install dotfiles.

  ![](./media/image39.png)

## **Task 7: Add a dotfile to your repository and run your codespace**

1.  Once the repository is selected, click on the **hamburger** icon to
    navigate to the main page of the repository.

  ![](./media/image40.png)

2.  Select your repository.

  ![A screenshot of a computer Description automatically
  generated](./media/image41.png)

3.  Select Code and under the codespaces, delete the codespace that you
    have created initially in this lab.

![](./media/image42.png)

4.  Once one codespace is deleted, start a **new codespace** because
    maximum of two codespaces are allowed to be created.

![](./media/image43.png)

5.  From inside the codespace in the VS Code explorer window, create a
    new file.

  ![A screenshot of a computer Description automatically
  generated](./media/image44.png)

6.  Provide a name to the new file as +++setup.sh+++

  ![](./media/image45.png)

7.  Enter the following code into the file:

    ```
    #!/bin/bash
    sudo apt-get update
    sudo apt-get install sl
    echo "export PATH=\$PATH:/usr/games" >> ~/.bashrc
    ```

    ![](./media/image46.png)

    **Note**: The file should autosave.

8.  From the **VS Code terminal**, enter the command below and press
    **Enter**:

    ```
    git add setup.sh --chmod=+x
    ```

  ![](./media/image47.png)

9.  Now, enter the commit message through this command:

    ```
    git commit -m "Adding setup.sh from the codespace!"
    ```

  ![](./media/image48.png)

10. Navigate to **Source Control.**

  ![](./media/image49.png)

11. Update the commit message and commit the changes.

  ![A screenshot of a computer Description automatically
  generated](./media/image50.png)

12. Click on **Yes** to stage all changes and commit them directly.

  ![A screenshot of a computer Description automatically
  generated](./media/image51.png)

## **Summary:**

**Congratulations, you've completed this lab and learned a lot about
GitHub Codespaces!**

In this lab, you learned how to use GitHub Codespaces as a fully
featured cloud development environment with Visual Studio Code. You
practiced creating and managing codespaces, pushing code changes,
customizing the development container, and personalizing your setup
using extensions and dotfiles. These skills help you create consistent,
efficient, and reproducible development environments for yourself and
your team
