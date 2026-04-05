# Kubernetes Local Development Setup Guide

This guide provides step-by-step instructions to install **Minikube** and **kubectl** on a Linux system, start a local cluster, and deploy your first pod.

## Prerequisites

Before installing, ensure your system meets the following requirements:
- **OS**: Linux (Ubuntu, Debian, Fedora, CentOS, etc.)
- **CPU**: 2+ cores
- **Memory**: 2GB+ free RAM
- **Disk**: 20GB+ free disk space
- **Container Runtime**: Docker (recommended) or other drivers (VirtualBox, KVM, Podman)

---

## 1. Install Dependencies

First, update your package index and install necessary utilities (`curl`, `wget`, `git`, and `docker`).

```bash
# Update package index
sudo apt-get update  # For Debian/Ubuntu
# OR
sudo dnf check-update # For Fedora/CentOS

# Install dependencies
sudo apt-get install -y curl wget git docker.io
# OR
sudo dnf install -y curl wget git docker

# Start and enable Docker service
sudo systemctl start docker
sudo systemctl enable docker

# Add your user to the docker group to run docker without sudo
sudo usermod -aG docker $USER
# Note: You must log out and log back in for this to take effect.

#-----------------------------
#--  Install minikubes
#-----------------------------

# Download the latest Minikube binary
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

# Install it to the system path
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# Verify installation
minikube version

# Download the latest Minikube binary
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

# Install it to the system path
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# Verify installation
minikube version

#-----------------------------
#--  Install kubectl
#-----------------------------

# Download the latest stable version
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

# Verify the download (optional but recommended)
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check

# Make executable and move to path
chmod +x kubectl
sudo mv kubectl /usr/local/bin/

# Verify installation
kubectl version --client


#-----------------------------
#--  Start the Cluster
#-----------------------------

# Start the cluster
minikube start --driver=docker

# Verify the cluster is running
minikube status
kubectl get nodes

#-----------------------------
#--  Deploy Pod
#-----------------------------

## See deployment, service and dependencies in yaml files

#-----------------------------
#--  Access plot
#-----------------------------

# Access via minikube service command
minikube service <service-name>
# Access http://localhost:port in a browser
