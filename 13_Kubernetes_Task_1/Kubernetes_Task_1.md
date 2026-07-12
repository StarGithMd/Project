
#########################################################################################################################
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ GUVI Assignment 13 Task -1 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#########################################################################################################################

### Kubernetes Task -1
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
- 01_Q. Setup minikube at your local and explore creating namespaces (Go through official documentation).

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ Activity GUVI Assignment 13 Task -1  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To set up Minikube and explore namespaces on Ubuntu 24.04, follow the steps below. Afterward, push the project files to a GitHub repository.

To setting up minikube on ubuntu 24.04 and exploring Kubernetes namespaces

Prerequisites:
Requirement	Notes
OS:						Ubuntu 24.04 LTS
CPU:					2 vCPUs minimum
RAM:					4 GB minimum (8 GB recommended)
Disk:					20 GB free space
Container/VM runtime:	Docker (recommended driver)
User privileges:		sudo access


Step 01: Update the Ubuntu 24.04 LTS system after deploying a new VM and installing OS version. 
$ sudo apt update && sudo apt upgrade -y && sudo reboot

Step 02: Install Docker (container runtime / driver) after adding the docker repository and docker's official GPG key.
$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
 
$ sudo apt install -y ca-certificates curl gnupg
$ sudo apt update; sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

Step 03: Allow your user to run docker without sudo and verify:
$ sudo docker version

$ sudo usermod -aG docker $USER
$ newgrp docker

Step 04: Install minikube and Install kubectl, start the cluster and verify the cluster
$ curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
$ sudo install minikube-linux-amd64 /usr/local/bin/minikube
$ rm minikube-linux-amd64

curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/

Step 4: Start cluster:
minikube start --driver=docker

Step 5: Explore Namespaces (Namespaces help organize resources in Kubernetes clusters. By default):
kubectl get namespaces

Step 6: Create Custom Namespaces (You can create namespaces either via YAML or CLI).
Using CLI:
kubectl create namespace development

Using YAML:
$ cat service.yaml
apiVersion: v1
kind: Service
metadata:
  name: hello-minikube
  namespace: dev
spec:
  selector:
    app: hello-minikube
  ports:
    - port: 8080
      targetPort: 8080
	  
$ cat deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-minikube
  namespace: dev
spec:
  replicas: 1
  selector:
    matchLabels:
      app: hello-minikube
  template:
    metadata:
      labels:
        app: hello-minikube
    spec:
      containers:
      - name: hello-minikube
        image: k8s.gcr.io/echoserver:1.4
        ports:
        - containerPort: 8080


Apply it:
kubectl apply -f namespace-dev.yaml

Step 7: Deploy into a namespace: (Deploy resources into a namespace):
kubectl create deployment nginx --image=nginx --namespace=development

Verify: List resources in a namespace:
kubectl get all -n dev

Switch default namespace (optional):
kubectl config set-context --current --namespace=development


Steps 10: Push to GitHub Repository
git init
git add .
git commit -m "Minikube setup with namespaces"

git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main

