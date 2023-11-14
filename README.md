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
