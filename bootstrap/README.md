# Bootstrap Directory

This folder contains the core manifests and kustomizations for setting up your Kubernetes cluster with ArgoCD and related applications.

## Structure and Content

### Top-Level Files

- **argo-cd.yaml**  
  Defines an ArgoCD Application resource for deploying and managing ArgoCD itself. Points to the `bootstrap/argo-cd` directory for its manifests and deploys ArgoCD into the `argocd` namespace with automated sync, pruning, and self-healing.

- **argocd-workflows-app.yaml**  
  Defines an ArgoCD Application for deploying Argo Workflows using the official Helm chart. Installs into the `argo-workflows` namespace with automated sync, pruning, and self-healing.

- **cert-manager-app.yaml**  
  Defines an ArgoCD Application for deploying cert-manager. Points to `bootstrap/cluster-resources/in-cluster/cert-manager` for manifests and installs into the `cert-manager` namespace. Handles CRD differences and enables automated sync, pruning, and self-healing.

- **cluster-resources.yaml**  
  Defines an ArgoCD ApplicationSet for managing cluster-wide resources. Uses a Git generator to apply all JSON files in `bootstrap/cluster-resources/` and ensures resources are preserved on deletion.

- **pihole-app.yaml**  
  Defines an ArgoCD Application for deploying Pi-hole. Points to `apps/pihole` for manifests and installs into the `pihole` namespace with automated sync, pruning, and self-healing.

- **root.yaml**  
  The root ArgoCD Application, acting as the entry point for bootstrapping all other applications and resources. Points to the `projects` directory and enables automated sync, pruning, and self-healing.

- **traefik-app.yaml**  
  Defines an ArgoCD Application for deploying Traefik. Points to `apps/traefik` for manifests and installs into the `traefik` namespace with automated sync, pruning, and self-healing.

### Subdirectories

- **argo-cd/**  
  Contains additional manifests and kustomizations for configuring ArgoCD itself, such as:
  - `ingress.yaml`: Configures external access to the ArgoCD UI.
  - `kustomization.yaml`: Kustomize file for managing overlays and resources.

- **cluster-resources/**  
  Contains cluster-wide resource definitions, including:
  - `in-cluster.json`: Manifest for in-cluster resources.
  - `pi-hole-ns.yaml`: Namespace definition for Pi-hole.
  - `in-cluster/`: Subdirectory for further breakdown, such as:
    - `argo-workflows.yaml`: Manifests for Argo Workflows.
    - `argocd-ns.yaml`: Namespace definition for ArgoCD.
    - `cert-manager.yaml`: Manifests for cert-manager.
    - `traefik-ns.yaml`: Namespace definition for Traefik.
    - `cert-manager/`: Contains cert-manager specific manifests and kustomization.

## Summary Table

| File/Folder                | Purpose                                                                                  |
|---------------------------|------------------------------------------------------------------------------------------|
| argo-cd.yaml              | Deploys and manages ArgoCD via ArgoCD Application                                       |
| argocd-workflows-app.yaml | Deploys Argo Workflows using Helm                                                        |
| cert-manager-app.yaml     | Deploys cert-manager and handles CRDs                                                    |
| cluster-resources.yaml    | Manages cluster-wide resources using ApplicationSet                                      |
| pihole-app.yaml           | Deploys Pi-hole application                                                              |
| root.yaml                 | Root application for bootstrapping all resources                                         |
| traefik-app.yaml          | Deploys Traefik ingress controller                                                       |
| argo-cd/                  | ArgoCD-specific manifests and kustomizations                                             |
| cluster-resources/        | Cluster-wide resource definitions and supporting manifests                               |

---

For more details on each application or resource, see the respective YAML files and subdirectory READMEs if available.
