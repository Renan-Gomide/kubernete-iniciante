# Introdução a Kubernetes

Kubernetes é uma plataforma open-source para gerenciar aplicações containerizadas em múltiplos hosts, fornecendo mecanismos básicos para a implantação, manutenção e escalonamento de aplicações.

## Kubectl

`kubectl` é a ferramenta de linha de comando para interagir com o Kubernetes. Com ele, você pode executar comandos no seu cluster Kubernetes, como criar, atualizar, excluir e visualizar recursos.

### Comandos básicos do kubectl

| Comando | Descrição |
|---------|------------|
| `kubectl get svc` | Lista todos os serviços no cluster. |
| `kubectl get nodes --watch` | Monitora os nós do cluster em tempo real. |

## AWS CLI para criar e acessar um Kubernetes (EKS)

O Amazon Elastic Kubernetes Service (EKS) é um serviço gerenciado que facilita a execução do Kubernetes na AWS sem precisar instalar e operar seu próprio plano de controle Kubernetes.

### Instalando a AWS CLI

Para instalar a AWS CLI, siga as instruções oficiais da [documentação da AWS](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html).

### Comandos para EKS

| Comando | Descrição |
|---------|------------|
| `aws eks --region sa-east1 describe_cluster --name aaa --query cluster.status` | Descreve o status do cluster EKS. |
| `aws eks --region sa-east1 update-kubeconfig --name aaa` | Atualiza o kubeconfig para acessar o cluster EKS. |

## Config do kubectl para acessar a AWS

Após configurar a AWS CLI, você precisa configurar o `kubectl` para acessar seu cluster EKS. Use o comando `aws eks update-kubeconfig` para atualizar seu arquivo kubeconfig com as credenciais do cluster.

## Criando nós na AWS

Os nós são as máquinas (físicas ou virtuais) que executam as aplicações containerizadas e outros componentes do Kubernetes. No EKS, você pode criar nós usando grupos de nós gerenciados ou autoescaladores.

### Criando um grupo de nós gerenciados

1. Acesse o console do EKS.
2. Selecione seu cluster.
3. Vá para a seção "Compute" e clique em "Add Node Group".
4. Siga as instruções para configurar e criar o grupo de nós.

## Criando Kubernetes no GCP (GKE)

O Google Kubernetes Engine (GKE) é um serviço gerenciado que facilita a execução do Kubernetes no Google Cloud Platform (GCP).

### Criando um cluster GKE

1. Acesse o console do GCP.
2. Vá para a seção "Kubernetes Engine".
3. Clique em "Create Cluster".
4. Siga as instruções para configurar e criar o cluster.

## Instalar CLI gcloud no Linux e acessar pelo terminal

A CLI gcloud é a ferramenta de linha de comando para interagir com o Google Cloud Platform.

### Instalando a CLI gcloud

1. Baixe e instale a CLI gcloud seguindo as instruções da [documentação oficial](https://cloud.google.com/sdk/docs/install).

### Autenticando e configurando

1. Execute `gcloud init` para inicializar a CLI e configurar seu projeto.
2. Use `gcloud container clusters get-credentials [CLUSTER_NAME]` para configurar o `kubectl` para acessar seu cluster GKE.

### Resumo dos Comandos

| Comando | Descrição |
|---------|------------|
| `aws eks --region sa-east1 describe_cluster --name aaa --query cluster.status` | Descreve o status do cluster EKS. |
| `aws eks --region sa-east1 update-kubeconfig --name aaa` | Atualiza o kubeconfig para acessar o cluster EKS. |
| `kubectl get svc` | Lista todos os serviços no cluster. |
| `kubectl get nodes --watch` | Monitora os nós do cluster em tempo real. |

## Criando YAML do Kubernetes

Para criar recursos no Kubernetes, você pode usar arquivos YAML. Aqui estão alguns exemplos de tipos de recursos que você pode definir:

- `kind: Pod`
- `kind: Deployment`

### Estrutura de um arquivo YAML

Um arquivo YAML para Kubernetes geralmente contém as seguintes seções:

- `apiVersion`: A versão da API do Kubernetes que você está usando.
- `kind`: O tipo de recurso que você está criando (por exemplo, Pod, Deployment).
- `metadata`: Metadados sobre o recurso, como nome e rótulos.
- `spec`: A especificação do recurso, que varia dependendo do tipo de recurso.

### Exemplo de YAML para um Pod

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: meu-pod
spec:
  containers:
  - name: meu-container
    image: nginx
```

### Exemplo de YAML para um Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: meu-deployment
spec:
  replicas: 3
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
```

### Exemplo de YAML para um LoadBalancer

```yaml
apiVersion: v1
kind: Service
metadata:
  name: meu-loadbalancer
spec:
  type: LoadBalancer
  selector:
    app: meu-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
```

### Diferenças entre Pod, Deployment e LoadBalancer

| Característica | Pod | Deployment | LoadBalancer |
|----------------|-----|------------|--------------|
| `kind` | Pod | Deployment | Service |
| Escalabilidade | Não escalável por si só | Suporta escalabilidade | N/A |
| Atualizações | Não suporta atualizações automáticas | Suporta atualizações automáticas | N/A |
| Uso | Usado para executar um único contêiner ou um grupo de contêineres | Usado para gerenciar um conjunto de réplicas de Pods | Usado para expor serviços para fora do cluster |

### Criando recursos com YAML

Para criar recursos definidos em um arquivo YAML, use o comando:

```sh
kubectl apply -f <arquivo.yaml>
```

### Escalando e expondo recursos

- `kubectl scale`: Escala o número de réplicas de um recurso.
- `kubectl expose`: Expõe um recurso como um serviço.

Exemplo de uso:

```sh
kubectl scale deployment <nome-do-deployment> --replicas=<número-de-réplicas>
kubectl expose deployment <nome-do-deployment> --type=LoadBalancer --name=<nome-do-serviço>
```
