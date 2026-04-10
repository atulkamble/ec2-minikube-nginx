# 🚀 EC2 + Minikube + NGINX Deployment

Deploy a simple **NGINX application on Kubernetes using Minikube**, with optional EC2-based setup for real-world DevOps practice.

---

## 📌 Project Overview

This project demonstrates how to:

* Set up a local Kubernetes cluster using Minikube
* Deploy an NGINX application using Kubernetes Deployment
* Expose the application using a Service (NodePort)
* Access the application from browser

It is designed as a **beginner-friendly Kubernetes lab**. ([GitHub][1])

---

## 🏗️ Architecture

```
User → NodePort → Service → Deployment → Pods (NGINX)
```

---

## ⚙️ Prerequisites

Make sure the following are installed:

* Docker
* Minikube
* kubectl
* Internet connection

Verify:

```bash
minikube version
kubectl version --client
docker --version
```

---

## 🚀 Step 1: Start Minikube

```bash
minikube start
minikube status
kubectl get nodes
```

---

## 📦 Step 2: Deployment YAML

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx
          ports:
            - containerPort: 80
```

Apply:

```bash
kubectl apply -f deployment.yaml
kubectl get pods
```

---

## 🌐 Step 3: Service YAML

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30007
```

Apply:

```bash
kubectl apply -f service.yaml
kubectl get svc
```

---

## 🌍 Step 4: Access Application

### Option 1 (Recommended)

```bash
minikube service nginx-service
```

### Option 2

```bash
minikube ip
```

Then open:

```
http://<MINIKUBE-IP>:30007
```

---

## 🔍 Verification Commands

```bash
kubectl get pods
kubectl get deployments
kubectl get services
```

---

## 🧹 Cleanup

```bash
kubectl delete -f deployment.yaml
kubectl delete -f service.yaml
minikube stop
```

---

## 💡 Key Concepts

* **Deployment** → Manages Pods
* **Service** → Exposes application
* **NodePort** → External access
* **Minikube** → Local Kubernetes cluster

---

## 📚 Use Cases

* Kubernetes beginner practice
* DevOps interview preparation
* Local testing before EKS/AKS deployment

---

## 👨‍💻 Author

**Atul Kamble**
Cloud Solutions Architect | DevOps Trainer

---

## ⭐ Support

If you found this useful:

```bash
⭐ Star the repo
🍴 Fork the project
```

---
