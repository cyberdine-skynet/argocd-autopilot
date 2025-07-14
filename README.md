# argocd-autopilot

A repository for bootstrapping and managing ArgoCD and related applications using GitOps best practices.

## Overview

This repository provides a structured approach to deploying and managing Kubernetes resources with ArgoCD. It includes manifests and kustomizations for core infrastructure components and applications, such as:

- **[ArgoCD](https://argo-cd.readthedocs.io/)**: GitOps continuous delivery tool for Kubernetes.
- **[Traefik](https://traefik.io/)**: Ingress controller for managing external access.
- **[Pi-hole](https://pi-hole.net/)**: Network-wide ad blocker.
- **[cert-manager](https://cert-manager.io/)**: Automated management and issuance of TLS certificates.

## Repository Structure

- `bootstrap/`: Core manifests and kustomizations for initial cluster setup and ArgoCD bootstrapping.
- `apps/`: Application-specific manifests and kustomizations (e.g., `pihole`, `traefik`).
- `projects/`: ArgoCD project definitions and related resources.

## Getting Started

1. **Clone the repository:**
   ```sh
   git clone https://github.com/your-org/argocd-autopilot.git
   cd argocd-autopilot
   ```

2. **Apply the bootstrap manifests:**
   ```sh
   kubectl apply -k bootstrap/
   ```

3. **Access ArgoCD:**
   - Follow the instructions in `bootstrap/argo-cd/ingress.yaml` to access the ArgoCD UI.
   - Retrieve the initial admin password:
     ```sh
     kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
     ```

4. **Sync Applications:**
   - Use the ArgoCD UI or CLI to sync the defined applications and projects.

## Customization

- Edit the manifests in `apps/` and `bootstrap/` to fit your cluster’s requirements.
- Add new applications by creating new directories under `apps/` and updating the relevant kustomization files.

## Documentation

- See the `README.md` files in each subdirectory for more details on specific components and configuration options.

## License

This project is licensed under the terms of the [MIT License](LICENSE).
