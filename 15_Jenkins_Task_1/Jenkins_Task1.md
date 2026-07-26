#########################################################################################################################
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ GUVI Assignment 15 Task -1 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#########################################################################################################################

### Jenkins_Task -1
https://docs.google.com/document/d/1D65ggbFHm7AVrnMe7mzf7kmN0JYpzgXQapmz6rUYbbg/edit?usp=sharing

#### Techstacks needs to be used : 
   - AWS EBS
   - AWS EC2

#### How do I submit my work?
   - Push all your work files to GitHub (O/P screenshot images must).
   - Submit your URLs in the portal.

#### Terms and Conditions?
   - You agree to not share this confidential document with anyone. 
   - You agree to open-source your code (it may even look good on your profile!). Do not mention our company’s name anywhere in the code.
   - We will never use your source code under any circumstances for any commercial purposes; this is just a basic assessment task. 

   - NOTE: Any violation of Terms and conditions is strictly prohibited. You are bound to adhere to it.

#### Task Description:
- 01_Q. Launch jenkins and explore creating projects and users.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ Activity GUVI Assignment 15 Task -1  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To setting it up jenkins on ubuntu, create projects and manage users is a core skill for DevOps. Let’s walk through the essentials step by step. Afterward, push the project files to a GitHub repository.

System Requirements and Operating System:
Linux (Ubuntu/Debian, CentOS/RHEL)
Windows (Server or Desktop)
macOS (less common, but possible)

Java:
Jenkins requires Java (JDK or JRE).
Recommended: Java 11 or Java 17 (LTS versions).

Hardware:
Minimum: 256 MB RAM, 1 GB disk space.
Recommended: 1 GB+ RAM, 10 GB+ disk space (for plugins and builds).

Network & Access
Ports: Jenkins runs on 8080 by default. Ensure firewall/security groups allow access.
Browser: Modern browser (Chrome, Firefox, Edge) for Jenkins UI.
Internet Access: Needed to install plugins and updates.

Dependencies
Git (for SCM integration):
Build Tools (depending on project type):
Maven/Gradle for Java projects.
Docker for container builds.
Node.js for JavaScript pipelines.
java -version

vi jenkins.sh
sudo apt update
sudo apt install openjdk-11-jdk -y
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y

Start Jenkins:
Linux:  sudo systemctl start jenkins
		sudo systemctl status jenkins


Access Jenkins UI:
Open browser → http://localhost:8080
Unlock Jenkins using the initial admin password:
sudo cat /var/lib/jenkins/secrets/initialAdminPassword

Creating Projects (Jobs):
From Jenkins dashboard → New Item.

Enter a project name → choose type:
Freestyle Project → simple build/test/deploy tasks.
Pipeline → scripted CI/CD pipelines using Jenkinsfile.
Multibranch Pipeline → auto-detects branches in Git repos.

Configure:
Source Code Management (SCM) → Git, GitHub, Bitbucket.
Build Triggers → e.g., poll SCM, webhook from GitHub.
Build Steps → shell scripts, Maven, Gradle, Docker commands.
Post-build Actions → notifications, deploy artifacts.

Managing Users
Go to Manage Jenkins → Manage Users.

Add new user:
Username, password, full name, email.

Configure Security:
Enable Matrix-based security or Role-based strategy (plugin).
Assign roles: Admin, Developer, Viewer.

For enterprise setups:
Integrate with LDAP/Active Directory.
Use GitHub OAuth or SAML for single sign-on.

md_rustam@DESKTOP-CPK0PUB:~/Project$ git add .; git commit -m "15_Jenkins_Task_1"; git push
[main 2d4f1e7] 15_Jenkins_Task_1
 2 files changed, 100 insertions(+)
 create mode 100644 15_Jenkins_Task_1/Jenkins_Task1.jpg
 create mode 100644 15_Jenkins_Task_1/Jenkins_Task1.md
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 8 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 1.65 MiB | 2.87 MiB/s, done.
Total 5 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/StarGithMd/Project.git
   8bfeeae..2d4f1e7  main -> main