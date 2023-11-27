# Kubernetes

Configuração de containers para rodar projetos 
gerenciamentos dos recursos computacionais do ambiente 

## Artefados configurados no kubernetes

- pods
- deployment

## Services

- kind [started](https://kind.sigs.k8s.io/docs/user/configuration/#getting-started)
```
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

```

- kubectl (aplicativo de gerenciamento do kubernete)
- api https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-strong-getting-started-strong-
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```
### Criando cluster 

Atenção testes realizados precisa estar com vpn fechada proble4ma na redação do network  

```bash

kind create cluster
kind get clusters
kind delete clusters #<nome do cluster>

# verificando o cluster criado 
kubectl cluster-info --context kind-kind

# ou
docker ps
# kind-control-plane 

```

### Arquivo de configuração do cluster

configurando ambiente de cluster localmente  

```bash
#criando cluster customizado
kind create cluster --config=k8s/kind.yml --name=fullcycle

# parando cluster
kind delete clusters fullcycle

# gerenciando clusters na sua maquina listar e mudar o context 
kubectl config get-clusters
kubectl config use-context <nome do cluster>

```

 - no visualstudio utilize essa extension
 - ms-kubernetes-tools.vscode-kubernetes-tools

## Aplicação teste

configurando pod via kubctl , criando arquivo pod.yml definindo as informações da aplicação   
criando arquivo pod.yml

para fazer criação de imagens docker dentro do cluster é necessário estar logado no dockehub e usar tags fixas
sem ser latest

comando para criar pod
```
kubectl apply -f k8s/pod.yaml

kubectl get pods -o wide

# Apagando pods
kubectl delete pod serverhttp

kubectl drain fullcycle-worker3 --ignore-daemonsets --delete-emptydir-data --force

# Informações
kubectl get event

# port-forwarding
kubectl port-forward pod/serverhttp 8080:8080

# replicaset não consegue fazer alteração das imagens se mudar imagem
# Dados do pod
kubectl describe pod

kubectl get replicasets

kubectl delete replicaset serverhttp

kubectl rollout history deployment serverhttp
kubectl rollout undo deployment serverhttp
```

    imagem de teste para funcionamento dentro dos kubernets
    - pacalexandre/server-http:0.0.1


## configuração de authentication repositorio docker 

