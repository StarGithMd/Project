
#########################################################################################################################
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ GUVI Assignment 12 Task -3 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#########################################################################################################################

### Docker Task -3
https://docs.google.com/document/d/1zLfIH2e_9-vVCsxpeFuLJx6YP9pLKIzJj8LUf4fXhG8/edit?usp=sharing

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
- 01_Q. Create a custom docker image for nginx and deploy it using docker compose, where the volume bind mount should be at /var/opt/nginx location. Push the created custom docker image to your docker-hub.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ Activity GUVI Assignment 10 Task -2  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a custom Nginx Docker image, deploy it with Docker Compose follow the below steps and then push the image to Docker Hub.

Create Project Structure: Create a directory and create files inside it.

mkdir nginx-custom; cd nginx-custom

1. vi Dockerfile
# Use official Nginx base image
FROM nginx:latest

# Copy custom HTML file into image
COPY index.html /usr/share/nginx/html/index.html

# Expose port 80
EXPOSE 80

2. vi index.html
<!DOCTYPE html>
<html>
<head>
    <title>Custom Nginx</title>
</head>
<body>
    <h1>Hello from Custom Nginx!</h1>
    <p>This is a custom Docker image deployed via Docker Compose.</p>
</body>
</html>


3. vi docker-compose.yml
services:
  web:
    build: .
    container_name: custom-nginx
    ports:
      - "8080:80"
    volumes:
      - ./html:/var/opt/nginx


4. The bind mount maps your local ./html folder to /var/opt/nginx inside the container.
mkdir html; echo "<h2>Mounted Content</h2>" > html/index.html

5. Build & Run
docker compose up -d --build

Check logs:
docker logs custom-nginx

6. Visit : http://localhost:8080


7. Tag & Push to Docker Hub
docker login
docker tag nginx-custom <your-dockerhub-username>/nginx-custom:latest

docker push <your-dockerhub-username>/nginx-custom:latest


Now custom Nginx image is live on Docker Hub and it can be pulled anywhere with:
















