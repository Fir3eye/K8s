# 📢Minikube Installation Guide🚀
---
## 🎖️Install docker
```
sudo apt-get install docker.io
```
## 🏅Download minikube from the internet
```
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```
## 🥇Copy and give permission of minikube
```
sudo cp minikube-linux-amd64 /usr/local/bin/minikube
sudo chmod 755 /usr/local/bin/minikube
```
## 🥈Download kubectl from the internet
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
```
## 🥉Give Permissions and Move to bin directory
```
chmod +x kubectl
mv kubectl /usr/local/bin/Kubectl
minikube start --driver=docker
sudo usermod -aG docker $USER && newgrp docker
Minikube status
```


