# Introdução a Kubernetes

Kubernetes é uma plataforma open-source para gerenciar aplicações containerizadas em múltiplos hosts, fornecendo mecanismos básicos para a implantação, manutenção e escalonamento de aplicações.

## Kubectl

`kubectl` é a ferramenta de linha de comando para interagir com o Kubernetes. Com ele, você pode executar comandos no seu cluster Kubernetes, como criar, atualizar, excluir e visualizar recursos.

### Comandos básicos do kubectl:
| Comando | Descrição |
|---------|------------|
| `kubectl get svc` | Lista todos os serviços no cluster. |
| `kubectl get nodes --watch` | Monitora os nós do cluster em tempo real. |

## AWS CLI para criar e acessar um Kubernetes (EKS)

O Amazon Elastic Kubernetes Service (EKS) é um serviço gerenciado que facilita a execução do Kubernetes na AWS sem precisar instalar e operar seu próprio plano de controle Kubernetes.

### Instalando a AWS CLI

Para instalar a AWS CLI, siga as instruções oficiais da [documentação da AWS](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html).

### Comandos para EKS:
| Comando | Descrição |
|---------|------------|
| `aws eks --region sa-east1 describe_cluster --name aaa --query cluster.status` | Descreve o status do cluster EKS. |
| `aws eks --region sa-east1 update-kubeconfig --name aaa` | Atualiza o kubeconfig para acessar o cluster EKS. |

## Config do kubectl para acessar a AWS

Após configurar a AWS CLI, você precisa configurar o `kubectl` para acessar seu cluster EKS. Use o comando `aws eks update-kubeconfig` para atualizar seu arquivo kubeconfig com as credenciais do cluster.

## Criando nós na AWS

Os nós são as máquinas (físicas ou virtuais) que executam as aplicações containerizadas e outros componentes do Kubernetes. No EKS, você pode criar nós usando grupos de nós gerenciados ou autoescaladores.

### Criando um grupo de nós gerenciados:
1. Acesse o console do EKS.
2. Selecione seu cluster.
3. Vá para a seção "Compute" e clique em "Add Node Group".
4. Siga as instruções para configurar e criar o grupo de nós.

## Criando Kubernetes no GCP (GKE)

O Google Kubernetes Engine (GKE) é um serviço gerenciado que facilita a execução do Kubernetes no Google Cloud Platform (GCP).

### Criando um cluster GKE:
1. Acesse o console do GCP.
2. Vá para a seção "Kubernetes Engine".
3. Clique em "Create Cluster".
4. Siga as instruções para configurar e criar o cluster.

## Instalar CLI gcloud no Linux e acessar pelo terminal

A CLI gcloud é a ferramenta de linha de comando para interagir com o Google Cloud Platform.

### Instalando a CLI gcloud:
1. Baixe e instale a CLI gcloud seguindo as instruções da [documentação oficial](https://cloud.google.com/sdk/docs/install).

### Autenticando e configurando:
1. Execute `gcloud init` para inicializar a CLI e configurar seu projeto.
2. Use `gcloud container clusters get-credentials [CLUSTER_NAME]` para configurar o `kubectl` para acessar seu cluster GKE.

### Resumo dos Comandos:
| Comando | Descrição |
|---------|------------|
| `aws eks --region sa-east1 describe_cluster --name aaa --query cluster.status` | Descreve o status do cluster EKS. |
| `aws eks --region sa-east1 update-kubeconfig --name aaa` | Atualiza o kubeconfig para acessar o cluster EKS. |
| `kubectl get svc` | Lista todos os serviços no cluster. |
| `kubectl get nodes --watch` | Monitora os nós do cluster em tempo real. |