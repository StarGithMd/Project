
#########################################################################################################################
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ GUVI Assignment 13 Task -1 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#########################################################################################################################

## Kubernetes Task -1
https://docs.google.com/document/d/1d_cLx9yw-Fx1eiVnG0KnUOMEt45G5CqVapb3OH9ar7A/edit?usp=sharing

## Techstacks needs to be used : 
   - AWS EBS
   - AWS EC2

## How do I submit my work?
   - Push all your work files to GitHub (O/P screenshot images must).
   - Submit your URLs in the portal.

## Terms and Conditions?
   - You agree to not share this confidential document with anyone. 
   - You agree to open-source your code (it may even look good on your profile!). Do not mention our company’s name anywhere in the code.
   - We will never use your source code under any circumstances for any commercial purposes; this is just a basic assessment task. 

   - NOTE: Any violation of Terms and conditions is strictly prohibited. You are bound to adhere to it.

## Task Description:
- 01_Q. Setup minikube at your local and explore creating namespaces (Go through official documentation).

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ Activity GUVI Assignment 13 Task -1  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

## To set up Minikube and explore namespaces on Ubuntu 24.04, follow the steps below. Afterward, push the project files to a GitHub repository.

## To setting up minikube on ubuntu 24.04 and exploring Kubernetes namespaces

## Prerequisites:
## Requirement				Notes
## OS:						Ubuntu 24.04 LTS
## CPU:					2 vCPUs minimum
## RAM:					4 GB minimum (8 GB recommended)
## Disk:					20 GB free space
## Container/VM runtime:	Docker (recommended driver)
## User privileges:		sudo access


## Step 01: Update the Ubuntu 24.04 LTS system after deploying a new VM and installing OS version. 
$ sudo apt update && sudo apt upgrade -y && sudo reboot

## Step 02: Install Docker (container runtime / driver) after adding the docker repository and docker's official GPG key.
$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
 
$ sudo apt install -y ca-certificates curl gnupg
$ sudo apt update; sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

## Step 03: Allow your user to run docker without sudo and verify:
$ sudo docker version

$ sudo usermod -aG docker $USER
$ newgrp docker

## Step 04: Install minikube and Install kubectl, start the cluster and verify the cluster
$ curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
$ sudo install minikube-linux-amd64 /usr/local/bin/minikube
$ rm minikube-linux-amd64

## curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
$ chmod +x kubectl
$ sudo mv kubectl /usr/local/bin/

## Step 4: Start cluster:
$ minikube start --driver=docker

## Step 5: Explore Namespaces (Namespaces help organize resources in Kubernetes clusters. By default):
& kubectl get namespaces

## Step 6: Create Custom Namespaces (You can create namespaces either via YAML or CLI).
# Using CLI:
$ kubectl create namespace development

## Using YAML:
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


## Apply it:
$ kubectl apply -f namespace-dev.yaml

## Step 07: Deploy into a namespace: (Deploy resources into a namespace):
$ kubectl create deployment nginx --image=nginx --namespace=development

## Verify: List resources in a namespace:
$ kubectl get all -n dev

## Switch default namespace (optional):
$ kubectl config set-context --current --namespace=development


## Steps 08: Push to GitHub Repository
md_rustam@DESKTOP-CPK0PUB:~/Project$ git add .
md_rustam@DESKTOP-CPK0PUB:~/Project$ git commit -m "13_Kubernetes_Task_1"
[main ab7cad0] 13_Kubernetes_Task_1
 2 files changed, 137 insertions(+)
 create mode 100644 13_Kubernetes_Task_1/Deploy_minikube.jpg
 create mode 100644 13_Kubernetes_Task_1/Kubernetes_Task_1.md
md_rustam@DESKTOP-CPK0PUB:~/Project$ git push
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 8 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 2.59 MiB | 708.00 KiB/s, done.
Total 5 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/StarGithMd/Project.git
   0a306d4..ab7cad0  main -> main

