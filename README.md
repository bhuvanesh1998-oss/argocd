Argo CD installion 

Requirements :
        Installed kubectl command-line tool.
        Have a kubeconfig file (default location is ~/.kube/config).
        CoreDNS. Can be enabled for microk8s by microk8s enable dns && microk8s stop && microk8s start

1) Install Argo CD into Kubernetes cluster :
        ```kubectl create namespace argocd
         kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml```

2) Download Argo CD CLI
           `curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
        sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
        rm argocd-linux-amd64`
