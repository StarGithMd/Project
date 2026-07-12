
#########################################################################################################################
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ GUVI Assignment 14 Task -2 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#########################################################################################################################

### Kubernetes Task -2
https://docs.google.com/document/d/1xtSk7JeY5thbslsgr7_0aj0iASzNbq86JowWTC8TJTk/edit?usp=sharing

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
- 01_Q. Create the K8s EKS,further you have to do the deployment of the Nginx application and access the application outside the cluster.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ Activity GUVI Assignment 14 Task -2  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To setup K8S, EKS and deployment of the Nginx application, follow the steps below. Afterward, push the project files to a GitHub repository.

## System Prerequisites for Kubernetes on Ubuntu 24.04

## Requirement			:	Notes
## OS					:	Ubuntu 24.04 LTS
## CPU					:	2 vCPUs minimum
## RAM					:	4 GB minimum (8 GB recommended)
## Disk					:	20 GB free space
## Container/VM runtime	:	Docker (recommended driver)
## User privileges		:	sudo access
## Network				:	Full connectivity between nodes, unrestricted outbound internet access
## Unique identifiers	:	Each node must have a unique hostname, MAC address, and product UUID

## Prepare Hostnames and Networking
$ sudo hostnamectl set-hostname manager01   # Control plane
$ sudo hostnamectl set-hostname worker01  # Worker node
$ sudo hostnamectl set-hostname worker02  # Worker node

## Update /etc/hosts on all nodes:
cat << EOF | sudo tee -a /etc/hosts
192.168.110.131	master01
192.168.110.128	worker01
192.168.110.129	worker02
EOF

## Install prerequisites on all nodes:
$ bash ~/install_kubernetes.sh

# create a bash script to deploy kubernatese on ubuntu 24.04
cat ~/install_kubernetes.sh

# !/bin/bash
# Disable swap (required for Kubernetes)
sudo swapoff -a
sudo sed -i '/swap/d' /etc/fstab

# Load kernel modules
cat << EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF
sudo modprobe overlay
sudo modprobe br_netfilter

# Sysctl params
cat << EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
EOF
sudo sysctl --system

# Install containerd
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl gpg containerd
sudo mkdir -p /etc/containerd
containerd config default | sudo tee /etc/containerd/config.toml
sudo sed -i 's/SystemdCgroup = false/SystemdCgroup = true/' /etc/containerd/config.toml
sudo systemctl restart containerd
sudo systemctl enable containerd

# Add Kubernetes apt repository
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.31/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.31/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

# Install kubeadm, kubelet, kubectl
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl conntrack
sudo apt-mark hold kubelet kubeadm kubectl
sudo systemctl enable kubelet

# Initialize cluster (control plane node only)
sudo kubeadm init --pod-network-cidr=10.244.0.0/16

# Configure kubectl
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

# Install Calico CNI
kubectl apply -f https://raw.githubusercontent.com/projectcalico/calico/v3.28.0/manifests/calico.yaml

# Verify
kubectl get nodes
kubectl get pods -A

--------------------------------------------------------

## Run On the manager node to Initialize Kubernetes
$ sudo kubeadm init --pod-network-cidr=10.244.0.0/16

## After initialization, set up kubeconfig:
$ mkdir -p $HOME/.kube
$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id -u):$(id -g) $HOME/.kube/config

## Install a pod network (e.g., Calico or Flannel)
$ kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml

## Join Worker Nodes (Run On the control plane to generate the join command):
$ kubeadm token create --print-join-command

# Verify the Cluster
$ kubectl get nodes -o wide
$ kubectl get pods -A


## On each worker node, run the prerequisites above (containerd + kubeadm/kubelet), then:

# Paste the join command from above
sudo kubeadm join <control-plane-ip>:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>

# Verify the Cluster
$ kubectl get nodes -o wide
$ kubectl get nodes
$ kubectl get pods -A

## Deploy Nginx Application (Create a deployment)
$ kubectl create deployment nginx --image=nginx
$ kubectl scale deployment nginx --replicas=3

# Expose Nginx Outside the Cluster
$ kubectl expose deployment nginx --port=80 --type=NodePort

## Check the service:
kubectl get svc

## Access Nginx via the external port: 80.
$ curl http://<any-node-ip>:80

