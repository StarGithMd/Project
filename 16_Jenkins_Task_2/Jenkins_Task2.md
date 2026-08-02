#########################################################################################################################
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ GUVI Assignment 16 Task -2 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#########################################################################################################################

### Jenkins_Task -2
https://docs.google.com/document/d/1ztLa3XYOL9QSxY_Td3-fzoqxOTCDFvmnDyt-KBjzAvo/edit?usp=sharing

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
- 01_Q. Create a simple script file and push it to repo. Create a project in Jenkins connected to your GitHub repository. When a commit is made to your repo, automatically build must get triggered from Jenkins and the output must be shared to me via email.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ Activity GUVI Assignment 16 Task -2  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

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

Step 1: Created a Simple Bash Script File that prints system info:
touch script.sh; vi script.sh
# !/bin/bash
echo "Build started..."
echo "System Info:"

uname -a
echo "Build completed successfully!"

Make the script executable:
chmod +x script.sh

Commit and push to the GitHub repo.
git add .; git commit -m "16_Jenkins_Task_2"; git push
