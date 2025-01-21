# JenkinsStarterProject
The repository contains a project carried out as part of learning DevOps technologies.

## Used Technologies:

- GitHub 🐙
- Jenkins 🤖

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

# Configuring Git in Jenkins and Connecting a GitHub Repository

### Step 1: Configuring the Git Path in Jenkins
1. Open the command prompt (cmd).
2. Enter the following command:  
   `where git`
3. Copy the resulting path to the Git executable, e.g.:  
   `C:\Program Files\Git\cmd\git.exe`.
4. In Jenkins, navigate to **Manage Jenkins > Global Tool Configuration**.
5. In the **Git** section, click **Git installations > Add Git**:
   - In the **Path to Git executable** field, paste the copied path.
6. Click **Apply** and **Save**.

---

### Step 2: Connecting the GitHub Repository in Jenkins
1. Navigate to the desired Jenkins job (e.g., **Jenkins > FIRST_DEVOPS_PROJECT**).
2. Click **Configure**.
3. In the **Source Code Management** section, select **Git**.
4. In the **Repository URL** field, enter your GitHub repository URL, e.g.:  
   `https://github.com/WiolaWysopal/JenkinsGitHubCI.git`.

---

### Step 3: Creating Global Credentials
1. In Jenkins, go to:  
   **Manage Jenkins > Credentials**  
   or directly via:  
   `http://localhost:8080/manage/credentials/`.
2. In the **Stores scoped to Jenkins** section, select:  
   **System > Global credentials (unrestricted)**.
3. Click **+ Add Credentials**.
4. Fill in the following fields:
   - **Kind:** Username with password.
   - **Username:** Your GitHub username (or a personal access token if applicable).
   - **Password:** Your GitHub password (or the personal access token).
   - **ID:** Optional (you can specify a unique identifier for these credentials, e.g., `WiolaDevOps`).
5. Save the changes.

---

### Step 4: Adding Credentials to the Project
1. Navigate to the Jenkins job (e.g., **FIRST_DEVOPS_PROJECT > Configure**).
2. In the **Git > Credentials** section, select the previously created credentials.
3. Expand the **Advanced** section and fill in the following fields:
   - **Name:** The repository name (e.g., `origin`).
   - **Refspec:** If you want to fetch only a specific branch, e.g., `main`, use:  
     `+refs/heads/main:refs/remotes/origin/main`.

---

### Step 5: Verifying the Configuration
1. Open your Jenkins job (e.g., **FIRST_DEVOPS_PROJECT**).
2. Click **Build Now**.
3. Check the console logs:  
   **FIRST_DEVOPS_PROJECT > Build History > Click the current build > Console Output**.
   - A successful configuration will show the following message:  
     ```
     BUILD SUCCESS
     Finished: SUCCESS
     ```
   - Configuration issues will appear as error messages in the logs.

---


### Examples of Using Jenkins with GitHub Integration

After properly setting up Jenkins and connecting it to GitHub, you can use this integration for various purposes. Here are some examples:

---

#### 1. **Building an Application on Every Push to the Repository**
   - Configure a webhook in GitHub to send `push` events to Jenkins.
   - In Jenkins, set the trigger in the **Build Triggers** section to `GitHub hook trigger for GITScm polling`.
   - On every `push`, Jenkins will automatically trigger the job that can, for example, build the application and create a `.jar` or `.war` file.

---

#### 2. **Automatically Running Unit Tests**
   - After each application build, Jenkins can run unit tests using tools like Maven or Gradle.
   - Configure the **Build** section in the project to run a command like:
     ```
     mvn clean test
     ```
   - Test reports will be saved in Jenkins and visible in the **Test Results** section.

---

#### 3. **Creating a CI/CD Pipeline**
   - Connect Jenkins with Docker and Kubernetes to automate application deployments.
   - Example process:
     1. Jenkins builds the application and creates a Docker image.
     2. The Docker image is pushed to a registry (e.g., Docker Hub).
     3. Jenkins runs a script that deploys the application on a Kubernetes cluster.

---

#### 4. **Monitoring Code Quality with SonarQube**
   - Configure Jenkins so that after each `push`, the code is analyzed by SonarQube.
   - In the **Build** section, add a step to run the analysis, such as:
     ```
     mvn sonar:sonar
     ```
   - The code quality analysis results will be available in the SonarQube dashboard.

---

#### 5. **Generating Reports from Task Execution**
   - Jenkins can generate and store reports from building the application, tests, or deployments.
   - In the **Post-build Actions** section, add a step to save artifacts or reports:
     ```
     target/*.jar
     ```

---

#### 6. **Automatic Versioning**
   - You can configure Jenkins to automatically increment the application version on every build.
   - In the **Build** section, use a Bash script or a tool like Maven to automatically modify the version number in the `pom.xml` file.

---

#### 7. **Build Result Notifications**
   - Set up notifications to Slack, email, or another tool to receive information about task results.
   - In the **Post-build Actions** section, add a step to configure, for example, an email with the build results.

---
