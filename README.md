# ArgoCD installer
This project provides an easy way to install Argo CD on your system from the official ArgoCD repository and change it with customize.

Using kustomize, we make the following changes to the Argo CD deployment:  

- Add annotations for reloader: We add annotations to the deployment manifest to enable automatic reloading of the Argo CD server whenever a configuration change is detected. This ensures that any changes to the Argo CD configuration are immediately reflected in the running server.

- Enable monitoring through annotations: We also add annotations to enable monitoring of the Argo CD deployment using Prometheus and Grafana. This provides metrics for monitoring the health and performance of the Argo CD server.

- Remove standard configmaps, RBAC, and Argo CD: Finally, we remove the standard configmaps, RBAC rules, and the Argo CD deployment that are included in the official manifest. This is because we prefer to manage these components separately, outside of the Argo CD installation. By removing them, we can avoid conflicts and ensure that our custom configuration is applied correctly.

## Prerequisites
Before you can install Argo CD, you need to have the following tools installed on your system:
- kubectl: The Kubernetes command-line tool.
- kustomize: Kubernetes native configuration management

## Installation
To install Argo CD, simply run the following command:
if you want switch on terminal in UI 
```
kustomize build overlays/staging  > install-kustomization.yaml
kubectl create ns argocd
kubectl apply -f install-kustomization.yaml -n argocd
```

Without terminal
```
kustomize build overlays/prod  > install-kustomization.yaml
kubectl create ns argocd
kubect

If you want to install Argo CD with the standard argocd and argocd-rbac-cm components included in the official manifest, you can enable them by commenting out a block in the kustomization.yaml file.
To do this, find the following block in the kustomization.yaml file:
```
- path: delete-configmaps.yaml
  target:
  kind: ConfigMap
  name: argocd-cm
- path: delete-configmaps.yaml
  target:
  kind: ConfigMap
  name: argocd-rbac-cm
```

## Support
If you encounter any issues with this project, please open an issue on the GitHub repository. We will do our best to help you resolve the issue as quickly as possible.

## License
This project is licensed under the MIT License. See the LICENSE file for details.