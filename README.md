# What Is Argo CD?
 Argo CD is a declarative, GitOps continuous delivery tool for Kubernetes.

 # Why Argo CD?
Application definitions, configurations, and environments should be declarative and version controlled. Application deployment and lifecycle management should be automated, auditable, and easy to understand.

# Architecture 
![Screenshot from 2024-06-26 10-49-31](https://github.com/udhaya1148/argocd/assets/59645398/c14a11f5-88c5-4301-a5b1-85938e5a8a75)

# Argo CD installion 

## Requirements :
        Installed kubectl command-line tool.
        Have a kubeconfig file (default location is ~/.kube/config).
        CoreDNS. Can be enabled for microk8s by 
            microk8s enable dns && microk8s stop && microk8s start

## 1) Install Argo CD into Kubernetes cluster :
         kubectl create namespace argocd
         kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

## 2) Download Argo CD CLI
        curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
        sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
        rm argocd-linux-amd64

## 3) Access The Argo CD API Server¶
By default, the Argo CD API server is not exposed with an external IP. To access the API server, choose one of the following techniques to expose the Argo CD API server:

## Service Type Load Balancer
Change the argocd-server service type to LoadBalancer:

    kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'

                       or

## Port Forwarding
Kubectl port-forwarding can also be used to connect to the API server without exposing the service.

    kubectl port-forward svc/argocd-server -n argocd 8080:443

## 4) Login Using The CLI 
    argocd login <ARGOCD_SERVER ip & port>

## Retrive initial password to login :
    argocd admin initial-password -n argocd

## 5) Register A Cluster To Deploy Apps :
First list all clusters contexts in your current kubeconfig:

    kubectl config get-contexts -o name

Installs a ServiceAccount (argocd-manager), into the kube-system namespace of that kubectl context, and binds the service account to an admin-level ClusterRole. Argo CD uses this service account token to perform its management tasks (i.e. deploy/monitoring).

    argocd cluster add <cluster name>



