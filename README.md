# Deploy Mate – GitOps with Argo CD

A hands-on demo project showcasing GitOps-driven Kubernetes deployments using Argo CD, Helm, and Terraform (optional). This repo contains a simple NGINX Helm chart and Argo CD configuration to automate deployments on a local Kubernetes cluster (Minikube).

---

## 🚀 Tech Stack

* Kubernetes (Minikube)
* Argo CD (GitOps)
* Helm (Kubernetes package manager)
* Docker (Minikube driver)
* Optional: Terraform (infra provisioning)

---

## 📁 Project Structure

```text
DeployMate-GitOps/
├── argo-cd/                # Argo CD Application manifests
│   └── app-config.yaml     # Example Argo CD Application
├── helm/                   # Helm charts for your apps
│   └── my-nginx/           # NGINX Helm chart
│       ├── Chart.yaml
│       ├── values.yaml
│       └── templates/
├── .gitignore
└── README.md
```

---

## ⭐ Key Features

* **Declarative deployments**: Store your app manifests in Git and let Argo CD sync them automatically.
* **Helm integration**: Package apps with Helm for versioned releases.
* **Rollback support**: Use Git history to roll back broken deployments.
* **Local dev ready**: Run everything on Minikube using Docker, no cloud required.

---

## 🛠 Prerequisites

* \[WSL Ubuntu] or macOS/Linux terminal
* Docker installed and running
* \[Minikube]
* `kubectl`
* `helm`
* `argocd` CLI (optional)

---

## ⚡ Setup & Run

### 1. Clone the Repo

```bash
git clone https://github.com/<your-username>/DeployMate-GitOps.git
cd DeployMate-GitOps
```

### 2. Start Minikube

```bash
minikube start --driver=docker --memory=2500mb
kubectl config use-context minikube
```

### 3. Install Argo CD

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Port-forward the UI:

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Open: [http://localhost:8080](http://localhost:8080)

Login:

```bash
kubectl get secret argocd-initial-admin-secret -n argocd \
 -o jsonpath="{.data.password}" | base64 -d && echo
argocd login localhost:8080 --username admin --password <password> --insecure
```

### 4. Deploy the NGINX Helm Chart via Argo CD

1. Push this repo to GitHub (if not already):

   ```bash
   ```

git remote add origin [https://github.com/](https://github.com/)<your-username>/DeployMate-GitOps.git
git push -u origin main

````

2. In the Argo CD UI, create a new Application:
   - **App name**: `nginx-app`
   - **Repo URL**: `https://github.com/<your-username>/DeployMate-GitOps.git`
   - **Path**: `helm/my-nginx`
   - **Cluster**: `https://kubernetes.default.svc`
   - **Namespace**: `default`
   - Sync policy: Manual

3. Click **Sync** → **Synchronize**. Wait for pods and service to appear:
   ```bash
kubectl get pods
kubectl get svc
````

---

## 🎓 What You’ll Learn

* How to implement GitOps with Argo CD
* Packaging Kubernetes apps with Helm
* Local Kubernetes cluster management with Minikube
* Basic secret handling (next phase)

---

## 🔮 Next Steps

* Add **Sealed Secrets** for secure secret management.
* Provision cloud infra (EKS/GKE) using **Terraform**.
* Extend with **CI/CD** pipelines (GitHub Actions).

---

## 👤 Author

SaiPranay Akkinepally – DevOps Engineer passionate about GitOps and automation.

Feel free to ⭐ the repo and reach out on [LinkedIn](https://www.linkedin.com/in/saipranay-akkinepally-devops)!
