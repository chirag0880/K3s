# K3s
K3s is a lightweight, certified Kubernetes distribution designed for resource-constrained environments like edge computing, IoT, and development workflows. It is developed by Rancher Labs (now part of SUSE) and is fully compliant with upstream Kubernetes, meaning it works with standard Kubernetes tools and manifests.

Key Features of K3s
Lightweight

Packaged as a single binary (~50MB), reducing dependencies and overhead.

Uses SQLite as the default storage backend (instead of etcd), but supports etcd, MySQL, and PostgreSQL.

Simplified Deployment

Easy to install with a single command, making it ideal for edge/IoT devices and CI/CD pipelines.

Reduced Resource Usage

Optimized for low CPU/memory environments (can run on a Raspberry Pi!).

Batteries-Included but Modular

Includes bundled components like:

Containerd (default runtime, but can use Docker)

Flannel (default CNI)

CoreDNS

Traefik (Ingress controller)

Unnecessary components (like cloud providers) are removed.

Security

Supports TLS by default for secure communication.

Auto-generates certificates for nodes.

Air-Gap Friendly

Can be installed offline with all dependencies bundled.

ARM Support

Works on ARM64 and ARMv7 (great for Raspberry Pi and edge devices).

Use Cases for K3s
Edge/IoT deployments (low-power devices).

Development & Testing (faster than minikube/kind).

Homelabs & Raspberry Pi clusters.

CI/CD pipelines (lightweight Kubernetes for testing).

Embedded systems where full K8s is too heavy.

K3s vs. K8s vs. MicroK8s vs. Minikube
Feature	K3s	Full Kubernetes (K8s)	MicroK8s (Canonical)	Minikube (Local Dev)
Size	~50MB	Large	~200MB	~200MB+
Memory	~512MB+	2GB+	~1GB+	~2GB+
Use Case	Edge/Production	Production	Dev/Edge	Local Dev
Complexity	Low	High	Medium	Medium
Storage	SQLite (default)	etcd	etcd	varies
Installing K3s
Quick Install (Single Node)
bash
curl -sfL https://get.k3s.io | sh -
Kubeconfig is saved at /etc/rancher/k3s/k3s.yaml.

Access with:

bash
sudo kubectl get nodes
Multi-Node Cluster
Master Node:

bash
curl -sfL https://get.k3s.io | K3S_TOKEN=mytoken sh -s - server --cluster-init
Worker Nodes:

bash
curl -sfL https://get.k3s.io | K3S_TOKEN=mytoken K3S_URL=https://master-ip:6443 sh -
Uninstall K3s
bash
/usr/local/bin/k3s-uninstall.sh
K3s Components
Component	Role	Replaceable?
SQLite	Default storage backend	Yes (etcd, MySQL, etc.)
Flannel	Default CNI (networking)	Yes (Calico, Cilium, etc.)
Traefik	Default Ingress Controller	Yes (Nginx, Istio, etc.)
Containerd	Default container runtime	Yes (Docker, CRI-O)
