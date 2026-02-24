instal k3s in ubanut 22.04 core server os lts

We will now do a clean, production-style setup from zero using k3s on your Ubuntu server (same LAN), then deploy nginx and verify from your laptop.

After you reinstall Ubuntu 22.04 on the server:
🧹 PART 1 — Clean Reset (Fresh System)

sudo apt update && sudo apt upgrade -y

sudo apt install -y curl  (required)

🚀 PART 2 — Install k3s (Lightweight Kubernetes)

curl -sfL https://get.k3s.io | sh -

🔎 Verify k3s Service

sudo systemctl status k3s

🔧 PART 3 — Configure kubectl For Your User
k3s stores kubeconfig here:  /etc/rancher/k3s/k3s.yaml  

Copy it to your user:
mkdir -p ~/.kube
sudo cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
sudo chown $USER:$USER ~/.kube/config

Now test:

kubectl get nodes

🌐 PART 4 — Allow NodePort Traffic (Firewall)

sudo ufw allow 6443/tcp
sudo ufw allow 30000:32767/tcp

sudo ufw status


🚀 PART 5 — Deploy nginx 

kubectl create deployment nginx --image=nginx
Verify pod running
kubectl get pods
🌍 PART 6 — Expose nginx via NodePort
kubectl expose deployment nginx --type=NodePort --port=80
kubectl get svc


🧠 Network Flow Now

Laptop
   ↓
192.168.3.28:31245
   ↓
k3s NodePort
   ↓
nginx pod

🔎 Extra Verification Commands

Check cluster info:

kubectl cluster-info

Check all system pods:

kubectl get pods -A

Check node details:

kubectl describe node

🧹 Cleanup (If Needed)

kubectl delete deployment nginx
kubectl delete service nginx
