# DevOpsKickstart
The repository contains a project carried out as part of learning DevOps technologies.

## Used Technologies:

- GitHub 🐙
- Jenkins 🤖
- Docker 🐳
- Amazon EC2 ☁️
- Maven 🔧

## Jenkins installation

1. Make sure you have JDK installed on your computer (required version: 11, 17 or 21). On Windows 10, you can use the following commands on admin account: `winget search jdk`, `winget install Oracle.JDK.21`
2. Download and install [Jenkins](https://www.jenkins.io/download/). For a detailed guide on the installation process, you can refer to this [video](https://www.youtube.com/watch?v=XdgNWJlVeEg).
3. After a successful installation, Jenkins runs by default on `http://localhost:8080/` (the port can be changed in the `jenkins.xml` file located in the installation directory). To complete the installation process, navigate to the location `C:\ProgramData\Jenkins\.jenkins\secrets\initialAdminPassword` and copy the secret hidden in the file. Paste it into the form.
4. Complete the installation by installing the suggested plugins and creating an admin account.

### Project configuration

**Using the Public Over SSH Plugin in Jenkins**

In my Jenkins configuration, I use the Public Over SSH plugin to automate remote deployments and run commands on external servers securely. This plugin allows Jenkins to connect to remote machines via SSH using public-private key authentication, ensuring a safe and efficient process for managing tasks like application deployments and system maintenance.

**Publish Over SSH configuration**

1. Install _Publish Over SSH_ plugin.
2. Go to `Jenkins > Manage Jenkins > System`.
3. Scroll down to the end of the page to the _Publish Over SSH_ section and add new server: `SSH Servers > Add`.
4. Give the `name`, `hostname` and `username` obligatory.
5. Click `Apply > Save`.

**Creating a New Project in Jenkins**

1. After configuring the _Publish Over SSH_ connection, create a new project by navigating to `Jenkins > New Item`.
2. Ensure that you add the `pom.xml` file to your remote repository on GitHub. This file should contain the necessary configuration for your Maven project.
3. Provide the URL of the remote repository.
4. Specify the branch to pull in Jenkins. By default, Jenkins may show the `master` branch, but the default branch on GitHub is `main`.
5. Set the appropriate Maven version and goals.
6. Click `Apply`, then `Save`.
7. On the project page, click `Build Now`.
8. If you encounter any issues, check the `Console Logs` in the project directory on Jenkins for more information.
