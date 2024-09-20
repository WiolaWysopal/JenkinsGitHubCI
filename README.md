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

##