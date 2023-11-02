# 📢Kubeadm Installation Guide🚀

This guide outlines the steps needed to set up a Kubernetes cluster using kubeadm.

## 🎡Pre-requisites

* t2.medium instance type or higher
* Ubuntu OS (Xenial or later)
* sudo privileges
* Internet access
---

## 🎡Both 🥇Master & 🥈Worker Node🎡

Run the following commands on both the master and worker nodes to prepare them for kubeadm.

```bash
# using 'sudo su' is not a good practice.
sudo apt update
sudo apt-get install -y apt-transport-https ca-certificates curl
sudo apt install docker.io -y

sudo systemctl enable --now docker # enable and start in single command.

# Adding GPG keys.
curl -fsSL "https://packages.cloud.google.com/apt/doc/apt-key.gpg" | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/kubernetes-archive-keyring.gpg

# Add the repository to the sourcelist.
echo 'deb https://packages.cloud.google.com/apt kubernetes-xenial main' | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt update 
sudo apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y
```
## 🥇Master Node🚀

1. Initialize the Kubernetes master node.

    ```bash
    sudo kubeadm init
    ```
    <kbd>![image](https://github.com/paragpallavsingh/kubernetes-kickstarter/assets/40052830/4fed3d68-eb41-423d-b83f-35c3cc11476e)</kbd>

    After succesfully running, your Kubernetes control plane will be initialized successfully.



3. Set up local kubeconfig (both for root user and normal user):

    ```bash
    mkdir -p $HOME/.kube
    sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
    sudo chown $(id -u):$(id -g) $HOME/.kube/config
    ```

4. Apply Weave network:

    ```bash
    kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
    ```

5. Generate a token for worker nodes to join:

    ```bash
    sudo kubeadm token create --print-join-command
    ```
6. Copy token on worker node
    ```
    what ever code have you generate cony on worker node 
    ```
   
7. Expose port 6443 in the Security group for the `Worker` to connect to Master Node
    ```
    # GO on our master EC2 instance and define port on security group 
    ```
---

## 🥈Worker Node🚀

1. Run the following commands on the worker node.

    ```bash
    sudo kubeadm reset pre-flight checks
    ```

2. Paste the join command you got from the master node and append `--v=5` at the end.
*Make sure either you are working as sudo user or use `sudo` before the command*

   After succesful join->
   <kbd>![image](https://github.com/paragpallavsingh/kubernetes-kickstarter/assets/40052830/c530b65a-4afd-4b1d-9748-421c216d64cd)</kbd>

---

## 🎢Verify Cluster Connection

On Master Node:

```bash
kubectl get nodes
```
<kbd>![image](https://github.com/paragpallavsingh/kubernetes-kickstarter/assets/40052830/4ed4dcac-502a-4cc1-a63e-c9cbb0199428)</kbd>

---
