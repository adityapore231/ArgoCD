
# Argo CD - GitOps

This repository shows how to Set up argoCD in Minikube Cluster.



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
Copy the encoded pass and decode through 
```bash
  echo ************************ | base64 --decode
```
Now you have two options :

-> use UI 

-> write application.yaml file

e.g of application.yaml file




#### Declarative
#### application.yaml

```yaml
apiVersion: argoproj.io/v1alpha
kind: Application
metadata:
  name: myapp
  namespace: argocd
spec: 
  project: default
  source:
    repoURL : https://github.com/adityapore231/ArgoCD.git  #github is the source
    targetRevision: HEAD                                   # HEAD measn last commit to repo
    path: dev                                              # specific path to sync
  destination:
    server: https://kubernetes.default.svc   #kubernetes api server is the destination
    namespaces: default

  syncPolicy:
    syncOptions:
    - CreateNamespace=True        #create namespace if not already exists

    automated:                     #track and sync
      selfHeal: true              #changes mado to the live cluster will trigger automated sync (default is false)
      prune: true                 #automatic sync wto delete resources                  

```

