
# Azure DevOps Autoscaling Agents on AKS with KEDA

This repository automates the deployment of **self-hosted Azure DevOps agents** on Azure Kubernetes Service (AKS) using **KEDA (Kubernetes Event-Driven Autoscaling)**. The setup dynamically scales agents based on pipeline demand, reducing costs and improving efficiency for parallel jobs.

---

## 📌 Overview

This solution provisions Azure DevOps agents as Kubernetes pods that scale up/down based on the number of queued jobs. Key components:
- **Azure DevOps**: Hosts pipelines and triggers agent scaling.
- **AKS (Azure Kubernetes Service)**: Manages agent pods.
- **KEDA**: Autoscales pods using the Azure Pipelines scaler.
- **Ephemeral Agents**: Agents terminate after job completion, minimizing resource waste.

---

## 🚀 Features

- **Dynamic Scaling**: Spawn agents only when jobs are queued.
- **Cost Optimization**: Scale to zero when idle (no fixed costs).
- **Parallel Job Support**: Run multiple jobs concurrently (e.g., 5 jobs → 5 pods).
- **Simplified Management**: Helm-managed KEDA and Kubernetes-native agents.

---

## ⚙️ Prerequisites

1. **Azure Resources**:
   - AKS Cluster (with [ACR integration](https://learn.microsoft.com/en-us/azure/aks/cluster-container-registry-integration)).
   - Azure DevOps Organization with Agent Pool (Default or Custom).
2. **Tools**:
   - Azure CLI (`az`).
   - Kubernetes CLI (`kubectl`).
   - Helm (`helm`).


## 🛠️ Installation

### 1. Install KEDA via Helm
```bash
helm repo add kedacore https://kedacore.github.io/charts
helm repo update
helm install keda kedacore/keda --namespace keda --create-namespace