# Lab 02: Enable CodeQL to secure your source code**

Objective:

Imagine you're a software developer working on a critical project for
your company, where ensuring the security of your application is a top
priority. With growing concerns about cyber threats and data breaches,
it’s essential to make sure that your code is free from vulnerabilities
and insecure coding practices.

In this hands-on lab, you will enable GitHub Code Scanning to
automatically review your source code for potential security issues.

## Exercise 1: Create a new repository from a public template

1.  Sign in to your GitHub account.

2.  Browse to the following link:
    <https://github.com/skills/introduction-to-codeql>

  In this lab you will create the repository using a public template
  “**skills-introduction-to-codeql**”.

  ![](./media/image1.png)

3.  Select **Create a new repository** under **Use this template** menu.

  ![A screenshot of a computer Description automatically
  generated](./media/image2.png)

4.  Enter the following details and select **Create Repository**.

- Repository name: +++skills-introduction-to-codeql+++

- Repository type: **Public**

  ![](./media/image3.png)

## Exercise 2: Enable code scanning with CodeQL

1.  On the landing page of the newly created repository navigate to the
    **Settings** tab.

  ![A screenshot of a computer Description automatically
  generated](./media/image4.png)

2.  Under the **Security** section on the left sidebar, select
    **Advanced Security**.

  ![](./media/image5.png)

3.  Scroll down to the section titled Code scanning, click the
    **Set-up** dropdown menu and choose **Default**.

  ![](./media/image6.png)

4.  Select the following options and click **Enable CodeQL**

- **Languages** to analyze: These are the languages that will be scanned
  by CodeQL. In this case, we will be scanning in **Python**.

- **Query suites:** CodeQL queries are packaged in bundles called
  "suites". This section allows you to choose which query suite to use.
  We'll leave this set as **Default** for this exercise.

- **Events**: This section tells CodeQL when to scan. In this case, it's
  set to scan on any pull request to the main branch.

  ![](./media/image7.png)

5.  Wait about 20 seconds and you’ll see the first automatic code scan.

  ![A screenshot of a computer Description automatically
  generated](./media/image8.png)

**Summary:**

In this lab, you have enabled GitHub Code Scanning to automatically
review your source code for potential security issues.
