# 🚀 Node Web App Project (React + Node.js on Kubernetes)

This project demonstrates how to build, containerize, and deploy a **Node + React web application** using **Docker** and **Kubernetes**.  
It covers local development, containerization, Kubernetes deployments, services, and version management with rollouts & rollbacks.

---

## 📂 Project Structure
```
NODE-WEB-APP-PROJECT/
│── src/                # React source code
│── Dockerfile          # Dockerfile for Node app
│── pod-definition.yml  # Pod definition (YAML)
│── service.yml         # Service definition (YAML)
│── deployment.yml      # Deployment definition (YAML)
│── README.md           # Documentation
```

---

## ⚡ Prerequisites
- Node.js & npm
- Docker
- Kubernetes (Minikube or any cluster)
- kubectl CLI

---

## 🛠️ Steps

### 1️⃣ Create React App
```bash
npx create-react-app testapp
cd testapp
npm start
```

📸 *Screenshot:* App running locally  
`/screenshots/local-react-app.png`

---

### 2️⃣ Dockerize the App
**Dockerfile**
```dockerfile
FROM node:18
WORKDIR /myapp
COPY . .
RUN npm install
EXPOSE 3000
CMD ["npm","start"]
```

**Build & Push Image**
```bash
docker build -t <dockerhub-username>/webapp_image:latest .
docker push <dockerhub-username>/webapp_image:latest
```

📸 *Screenshot:* Successful Docker build & push  
`/screenshots/docker-build-push.png`

---

### 3️⃣ Deploy on Kubernetes

**Create Deployment**
```bash
kubectl create deployment testappnew --image=<dockerhub-username>/webapp_image:latest
```

**Expose Deployment**
```bash
kubectl expose deployment testappnew --type=NodePort --port=3000
```

📸 *Screenshot:* Deployment + Service running  
`/screenshots/kubectl-deploy-svc.png`

---

### 4️⃣ Rollout & Rollback
Check rollout:
```bash
kubectl rollout status deployment/testappnew
```

Rollback if needed:
```bash
kubectl rollout undo deployment/testappnew
```

📸 *Screenshot:* Rollout / Rollback commands  
`/screenshots/rollout-rollback.png`

---

### 5️⃣ Apply YAML Definitions
You can also deploy using YAML files:

**Pod**
```bash
kubectl apply -f pod-definition.yml
```

**Service**
```bash
kubectl apply -f service.yml
```

**Deployment**
```bash
kubectl apply -f deployment.yml
```

📸 *Screenshot:* YAML apply results  
`/screenshots/yaml-apply.png`

---

### 6️⃣ Access Application
Get Minikube IP:
```bash
minikube ip
```

Open in browser:
```
http://<minikube-ip>:<nodeport>
```

Or directly:
```bash
minikube service testappnew
```

📸 *Screenshot:* App running in browser via Minikube  
`/screenshots/app-browser.png`

---

## 📖 Learnings
- Building a Node.js + React app  
- Dockerizing and pushing to DockerHub  
- Deploying with Kubernetes (`kubectl run`, `create deployment`, `apply -f`)  
- Exposing Pods/Deployments with Services  
- Performing rollouts & rollbacks  
- Writing Kubernetes YAML manifests  

---

## 👩‍💻 Author
**Alfiya**  
🔗 [GitHub](https://github.com/Alfiya-git)
