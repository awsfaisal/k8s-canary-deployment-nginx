# Canary Deployment on Kubernetes (NGINX)

## 📌 Project Overview
This project demonstrates a real-world Canary Deployment strategy on Kubernetes using an NGINX web application. The goal is to gradually shift traffic from a stable version (v1) to a new version (v2) by controlling the number of replicas, enabling safe and production-style rollouts.

---

## 🎯 Canary Deployment Goal
- Deploy v1 (stable) and v2 (canary) versions side-by-side
- Split traffic using a single Kubernetes Service
- Gradually increase traffic to v2
- Safely roll back if issues occur

---

## 🗂️ Namespace Setup (Optional)
```bash
kubectl create namespace canary-demo
kubectl config set-context --current --namespace=canary-demo
kubectl get pods
⚙️ Deployment – Version v1 (Stable)

Deployed NGINX v1 with 3 replicas

Labelled pods with version: v1

File: k8s/nginx-v1.yml

kubectl apply -f k8s/nginx-v1.yml

⚙️ Deployment – Version v2 (Canary)

Deployed NGINX v2 with 1 replica

Labelled pods with version: v2

File: k8s/nginx-v2.yml

kubectl apply -f k8s/nginx-v2.yml

🌐 Service Configuration

Single LoadBalancer Service

Routes traffic to both v1 and v2 pods using labels

AWS ELB used for external access

File: k8s/nginx-service.yml

kubectl apply -f k8s/nginx-service.yml

🌍 Access Application

Access the app via ELB DNS name

Refresh browser multiple times to hit:

NGINX v1 pods

NGINX v2 pod

📈 Progressive Canary Rollout
Increase Traffic to v2
kubectl scale deployment nginx-v2 --replicas=2

Reduce Traffic to v1
kubectl scale deployment nginx-v1 --replicas=1

Complete Rollout (100% v2)
kubectl scale deployment nginx-v1 --replicas=0

🧰 Technologies Used

Kubernetes

NGINX

Deployments

Services

Labels & Selectors

Canary Deployment Strategy

AWS LoadBalancer (ELB)
## 📂 Recommended Repo Structure
kubernetes-canary-deployment/
├── README.md
└── k8s/
├── nginx-v1.yml
├── nginx-v2.yml
└── nginx-service.yml

