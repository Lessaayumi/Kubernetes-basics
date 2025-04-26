# Kubernetes-basics

![Kubernetes Logo](https://upload.wikimedia.org/wikipedia/commons/3/39/Kubernetes_logo_without_workmark.svg)

Este projeto foi idealizado com o objetivo de proporcionar aprendizado introdutório sobre a ferramenta Kubernetes, a qual possui grande relevância no cenário tecnológico atual. Trata-se de um tutorial básico e didático, que orienta o usuário de maneira clara e detalhada sobre as etapas iniciais de utilização do Kubernetes, apresentando um passo a passo para facilitar o entendimento e a prática dos primeiros comandos.

## 🧠 O que é Kubernetes?

**Kubernetes** é um sistema de código aberto para automação de implantação, escalonamento e gerenciamento de aplicações em containers.

Foi desenvolvido pelo Google e agora é mantido pela Cloud Native Computing Foundation.

---

## 📦 Pré-requisitos

Antes de começar, você precisa ter:

- [Docker](https://docs.docker.com/get-docker/) instalado
- [kubectl](https://kubernetes.io/docs/tasks/tools/) instalado (CLI do Kubernetes)
- Uma instalação local do Kubernetes, como:
  - [Minikube](https://minikube.sigs.k8s.io/docs/start/) (para testes locais)
  - Ou um cluster Kubernetes em nuvem (AWS, Azure, GCP)

---

## 🚀 Começando com Kubernetes

### 1. Iniciar o Minikube (para testes locais)

```bash
minikube start
```

Este comando cria um cluster Kubernetes local.

### 2. Verificar o status do cluster

```bash
kubectl cluster-info
```

Se tudo estiver correto, o Kubernetes vai informar onde está rodando seu cluster.

### 3. Criar um arquivo de Deployment (deployment.yaml)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: meu-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: meu-app
  template:
    metadata:
      labels:
        app: meu-app
    spec:
      containers:
      - name: meu-container
        image: nginx
        ports:
        - containerPort: 80
```
Este arquivo define um deployment com 2 réplicas rodando o container NGINX.

### 4. Aplicar o Deployment

```bash
kubectl apply -f deployment.yaml
```

### 5. Verificar o Deployment e os Pods

```bash
kubectl get deployments
kubectl get pods
```

### Criar um Service para expor o app (service.yaml)

```yaml
apiVersion: v1
kind: Service
metadata:
  name: meu-servico
spec:
  type: NodePort
  selector:
    app: meu-app
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30007
```

Aplicar o Service:

```bash
kubectl apply -f service.yaml
```

### 7. Acessar o aplicativo

Pegue o IP do Minikube:

```bash
minikube ip
```

Depois acesse no navegador:

**http://<IP-DO-MINIKUBE>:30007**

Você verá a página inicial do NGINX rodando no Kubernetes! 

**🧹 Como limpar tudo:**

Para deletar os recursos criados:****

```bash
kubectl delete -f deployment.yaml
kubectl delete -f service.yaml
```

E para parar o Minikube:

```bash
minikube stop
```

🛠️ Tecnologias usadas 
- Kubernetes
- Minikube
- Docker
































