# ♾️ End-to-End Cloud-Native CI/CD Platform (GitOps)

This repository demonstrates a complete, production-ready DevOps workflow and GitOps deployment strategy. It features automated infrastructure provisioning on AWS, continuous integration for a complex microservices application, and pull-based continuous deployment.

> 💡 **Note:** The underlying microservices application deployed via this pipeline is the [OpenTelemetry Astronomy Shop Demo](https://github.com/open-telemetry/opentelemetry-demo). The core focus of this repository is the **infrastructure, automation, and CI/CD platform** built to deploy and manage it.

## 🚀 Key Achievements
- **Infrastructure as Code (IaC):** Provisioned highly available AWS infrastructure and Kubernetes (EKS) clusters from scratch using **Terraform** manifests.
- **Continuous Integration (CI):** Engineered automated build pipelines using **GitHub Actions** to build, tag, and push Docker images for multiple microservices upon code commits.
- **Continuous Deployment (CD):** Implemented a GitOps methodology using **Argo CD** for pull-based, automated sync deployments to the Kubernetes cluster.

## 🛠️ Tech Stack & Tools
- **Cloud Provider:** AWS (Amazon Web Services)
- **Infrastructure as Code:** Terraform
- **Containerization:** Docker
- **Orchestration:** Kubernetes (EKS)
- **CI/CD:** GitHub Actions, Argo CD
- **Application:** OpenTelemetry Microservices Demo (Go, Python, Java, Node.js)

## 🏗️ Architecture & Pipeline Flow
1. **Infrastructure Provisioning:** `Terraform` scripts define and deploy the VPC, networking, and the Amazon EKS cluster.
2. **Code Commit:** Developers push code changes to the repository.
3. **CI Pipeline:** `GitHub Actions` detects changes, runs tests, builds the respective Docker containers, and pushes the new images to the container registry.
4. **Manifest Update:** The CI pipeline updates the Kubernetes deployment manifests with the new image tags.
5. **CD Pipeline (GitOps):** `Argo CD`, running inside the Kubernetes cluster, detects the drift in the Git repository and automatically pulls and syncs the new state, achieving a zero-touch deployment.

## 📂 Repository Structure
*(Note: Highlight your DevOps directories here)*
```text
devops-project-mydemo/
│
├── .github/workflows/       # GitHub Actions CI pipelines for Docker builds
├── terraform/               # Terraform IaC manifests for AWS and EKS provisioning
├── k8s-manifests/           # Kubernetes deployment & service YAMLs
├── argocd/                  # Argo CD application configuration files
├── src/                     # OpenTelemetry microservices source code
└── README.md                # Project documentation
```

## 🚀 Getting Started

1. Provision Infrastructure
       
    Navigate to the terraform directory and provision the AWS EKS cluster:
    ```bash
    cd terraform
    terraform init
    terraform plan
    terraform apply --auto-approve
    ```

2. Configure Kubernetes Access

    Update your local kubeconfig to interact with the newly created cluster:

    ```bash
    aws eks update-kubeconfig --region <your-region> --name <your-cluster-name>
    ```

3. Setup Argo CD

    Install Argo CD in your Kubernetes cluster:

    ```bash
    kubectl create namespace argocd
    kubectl apply -n argocd -f [https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml](https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml)
    ```

4. Deploy the Application

    Apply the Argo CD application manifest to point to this repository and initiate the GitOps sync:

    ```bash
    kubectl apply -f argocd/application.yaml
    Argo CD will automatically deploy the OpenTelemetry Astronomy Shop microservices based on the configurations in the k8s-manifests folder.
    ```

### 🧹 Clean Up

To destroy all provisioned AWS resources and avoid unexpected cloud charges:
```bash   
cd terraform
terraform destroy --auto-approve
```

<br>
<br>

### Let's Connect:

<br>

Created by **Satya Sourav Patel**.

Subscribe to my [Substack](https://satyasouravpatel.substack.com/) for deep dives into DevOps, MLOps, and System Design.
