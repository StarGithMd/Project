

#########################################################################################################################
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ GUVI Assignment 11 Task -2 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#########################################################################################################################

### Docker Task -2
https://docs.google.com/document/d/190CsA4QFz0GOe7nEcXjykgK1Y5RZpDPDGuNX6lHSQCw/edit?usp=sharing

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
- 01_Q. Create a dockerfile, docker-compose file which when executed must display your basic details in the website.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ Activity GUVI Assignment 10 Task -2  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Create a file "Dockerfile" under Project directory with the following contents, nginx:alpine to serve a static HTML page.

# vi Dockerfile
# Use lightweight Nginx image
FROM nginx:alpine

# Set working directory
WORKDIR /usr/share/nginx/html

# Copy static HTML file into container
COPY index.html .

# Expose port 80
EXPOSE 80

Created one other file "index.html" with the webpage content as showing the details.

# vi index.html
<!DOCTYPE html>
<html>
<head>
  <title>Copilot Basic Details</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 40px; background: #f4f4f9; }
    h1 { color: #2c3e50; }
    p { font-size: 18px; }
    .card { background: white; padding: 20px; border-radius: 8px; box-shadow: 0 2px 6px rgba(0,0,0,0.2); }
  </style>
</head>
<body>
  <div class="card">
    <h1>Microsoft Copilot</h1>
    <p>Role: AI Companion</p>
    <p>Purpose: Increase knowledge & understanding</p>
    <p>Skills: Information synthesis, productivity support, debate & discussion</p>
    <p>Creator: Microsoft</p>
  </div>
</body>
</html>

Created on more file "docker-compose.yml" to maps container port 80 to host port 8080.
# vi docker-compose.yml
services:
  copilot-web:
    build: .
    ports:
      - "8080:80"

Verify the created three file as below
.
├── Dockerfile
├── docker-compose.yml
└── index.html

1 directory, 3 files

finally excuted the docker-composer file from the directiry successfully
$ docker compose up -d --build
[+] Building 5.6s (9/9) FINISHED
 => [internal] load local bake definitions                                                                         0.0s
 => => reading from stdin 570B                                                                                     0.0s
 => [internal] load build definition from Dockerfile                                                               0.0s
 => => transferring dockerfile: 209B                                                                               0.0s
 => [internal] load metadata for docker.io/library/nginx:alpine                                                    4.9s
 => [internal] load .dockerignore                                                                                  0.0s
 => => transferring context: 2B                                                                                    0.0s
 => [1/2] FROM docker.io/library/nginx:alpine@sha256:20316569d8f81a160065d7d2a5eeffc7ca97d79022462ee255fd23fa103a  0.1s
 => => resolve docker.io/library/nginx:alpine@sha256:20316569d8f81a160065d7d2a5eeffc7ca97d79022462ee255fd23fa103a  0.1s
 => [internal] load build context                                                                                  0.0s
 => => transferring context: 32B                                                                                   0.0s
 => CACHED [2/2] COPY index.html /usr/share/nginx/html/index.html                                                  0.0s
 => exporting to image                                                                                             0.2s
 => => exporting layers                                                                                            0.0s
 => => exporting manifest sha256:392998ac5ff60db0254e2e4c038f10b5aed947f8e3770351f12e2633ec8fba15                  0.0s
 => => exporting config sha256:e65d28f8062fda65dcee1f3dc24e5465adc519a7be299a71e375df8eae1a97e7                    0.0s
 => => exporting attestation manifest sha256:0f492716b52ee6354727d9a3f2d57a2797f08b4711524cfe500aec7bcca8eb48      0.1s
 => => exporting manifest list sha256:4d6c2a1b485d262ddf3c49cf7a25891e83fd37cafbe062faf7a8a7cbb04a0648             0.0s
 => => naming to docker.io/library/11_docker_task_2-copilot-web:latest                                             0.0s
 => => unpacking to docker.io/library/11_docker_task_2-copilot-web:latest                                          0.0s
 => resolving provenance for metadata file                                                                         0.0s
[+] up 2/2
 ✔ Image 11_docker_task_2-copilot-web       Built                                                                   5.8s
 ✔ Container 11_docker_task_2-copilot-web-1 Started                                                                 0.4s
md_rustam@DESKTOP-CPK0PUB:~/Project/11_Docker_Task_2$ http://localhost:8080
-bash: http://localhost:8080: No such file or directory
md_rustam@DESKTOP-CPK0PUB:~/Project/11_Docker_Task_2$ http://localhost
-bash: http://localhost: No such file or directory
md_rustam@DESKTOP-CPK0PUB:~/Project/11_Docker_Task_2$ http://localhost:80
-bash: http://localhost:80: No such file or directory



Verified the access the web page

http://172.19.101.31:8080/

This is the test Copilot
Role: AI Companion

Purpose: Increase knowledge and understanding

Skills: Information synthesis, productivity support, debate & discussion

Created by: Microsoft

