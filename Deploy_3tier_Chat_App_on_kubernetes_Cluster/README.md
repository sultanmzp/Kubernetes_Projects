# Three-Tier Chat Application – Kubernetes Deployment

## 📌 Project Overview
This project demonstrates the **end-to-end deployment of a three-tier application** using **Docker and Kubernetes**, following real-world **DevOps best practices**. The application consists of:

- **Frontend:** React
- **Backend:** Node.js (Express)
- **Database:** MongoDB

The goal of this project is to showcase containerization, orchestration, persistent storage, service discovery, and application exposure through Kubernetes.

---

## 🎯 Project Objective
To design, containerize, and deploy a **production-ready three-tier application** using **React, Node.js, and MongoDB**, while implementing Kubernetes resources such as **namespaces, deployments, services, persistent volumes, ingress, and load balancing**, enabling browser-based access to the application.

---

## 🛠️ Technologies Used

- **Containerization:** Docker
- **Orchestration:** Kubernetes (AWS EC2)
- **Frontend:** React
- **Backend:** Node.js (Express)
- **Database:** MongoDB
- **Container Registry:** Docker Hub
- **Persistent Storage:** Kubernetes PersistentVolume & PersistentVolumeClaim

---

## 🚀 Deployment Steps

### 1️⃣ Build and Push Docker Images
```bash
docker build -t <dockerhub-username>/chatapp-backend:latest ./backend
docker push <dockerhub-username>/chatapp-backend:latest

docker build -t <dockerhub-username>/chatapp-frontend:latest ./frontend
docker push <dockerhub-username>/chatapp-frontend:latest
```

---

### 2️⃣ Create Namespace
```bash
kubectl apply -f k8s/namespace.yaml
```

---

### 3️⃣ Configure MongoDB Persistent Storage
```bash
kubectl apply -f k8s/mongodb-pv.yaml
kubectl apply -f k8s/mongodb-pvc.yaml
```

---

### 4️⃣ Deploy MongoDB
```bash
kubectl apply -f k8s/mongodb-deployment.yaml
kubectl apply -f k8s/mongodb-service.yaml
```

---

### 5️⃣ Deploy Backend and Frontend
```bash
kubectl apply -f k8s/backend-deployment.yaml
kubectl apply -f k8s/backend-service.yaml

kubectl apply -f k8s/frontend-deployment.yaml
kubectl apply -f k8s/frontend-service.yaml
```

---

## 🌐 Accessing the Application (EC2)

Services are exposed using **NodePort** or **kubectl port-forward**.

### Option 1: Port Forward
```bash
kubectl port-forward svc/frontend-service 3000:80 -n chat-app-ns
```
Access in browser:
```
http://localhost:3000
```

### Option 2: NodePort
```bash
kubectl get svc -n chat-app-ns
```
```
http://<EC2-PUBLIC-IP>:<NodePort>
```

---

## 🧪 Verification Commands

```bash
kubectl get pods -n chat-app-ns
kubectl get svc -n chat-app-ns
kubectl logs <pod-name> -n chat-app-ns
```

---

## 🧠 Key Learnings

- Kubernetes service discovery using **ClusterIP**
- Persistent storage with **PV & PVC**
- Debugging **CrashLoopBackOff** and DNS issues
- Environment variable management
- Exposing applications from EC2 clusters

---

👤 **Author:** Sultan Faizuddin

