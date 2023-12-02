
# Argo CD

This repository shows how to Set up argoCD in Minikube Cluster




## ArgoCD Installation

https://argo-cd.readthedocs.io/en/stable/getting_started/

```bash
  kubectl create namespace argocd
  kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

```
This will create a new namespace, argocd, where Argo CD services and application resources will live.

Now We need access to argoCD UI, for this forword the port to 8080
```bash
  kubectl port-forward svc/argocd-server -n argocd 8080:443

```
Access the argoCD UI page with your localhost e.g 127.0.0.1:8080

Username : Admin (defualt)

to get password :
```bash
  kubectl get secret argocd-initial-admin-secret-n argocd -o yaml
```
Copy the encrepted pass and decrept through 
```bash
  echo ************************ | base64 --decode
```
Now you have two options :

-> use UI 

-> write application.yaml file

e.g of application.yaml file


This repository shows how to Set UP in Minikube Cluster



