# Cluster Kubernetes Local com Kind e Terraform

## 1. Objetivo

Esta atividade teve como objetivo provisionar um cluster Kubernetes local utilizando Kind (Kubernetes in Docker), com todo o processo de criação realizado através do Terraform.

O cluster foi criado sem executar manualmente o comando `kind create cluster`.

## 2. Identificação do cluster

- Nome do cluster: `devops`
- Tecnologia utilizada: Kind (Kubernetes in Docker)
- Provisionamento: Terraform
- Orquestrador: Kubernetes

## 3. Topologia

O cluster possui três nodes:

- 1 node control-plane
- 2 nodes workers

Representação da topologia:

```text
                 Kubernetes Cluster
                       devops
                         |
             +-----------+-----------+
             |                       |
      control-plane              workers
             |                 +-----+-----+
             |                 |           |
        devops-control-     devops-    devops-
           plane            worker     worker2

```
## 4. Arquivos Terraform

#### main.tf

O arquivo main.tf define o provider do Kind e o recurso kind_cluster, responsável por solicitar ao Terraform a criação do cluster.

Também é definida a topologia do cluster, contendo um node com função control-plane e dois nodes com função worker.

### variables.tf

O arquivo variables.tf define a variável utilizada para o nome do cluster.

O valor padrão utilizado é: devops

### outputs.tf

O arquivo outputs.tf apresenta como saída o nome do cluster criado pelo Terraform.

## 5. Principais componentes do cluster

### Control Plane

O control plane é responsável pelo gerenciamento do cluster Kubernetes.

Entre seus principais componentes estão:

    - kube-apiserver: recebe e processa as requisições para a API do Kubernetes.
    - etcd: armazena os dados e o estado do cluster.
    - kube-scheduler: decide em qual node os novos Pods devem ser executados.
    - kube-controller-manager: executa os controllers responsáveis por manter o estado desejado do cluster.

### Worker Nodes

Os workers são responsáveis pela execução das aplicações e Pods.

Entre os componentes relacionados à execução estão:

    - kubelet: agente executado em cada node e responsável por garantir que os Pods estejam funcionando.
    - kube-proxy: auxilia na implementação da comunicação de rede dos Services.
    - Container Runtime: responsável pela execução dos containers.

### CoreDNS

O CoreDNS fornece resolução de nomes dentro do cluster Kubernetes.

Por exemplo, permite que aplicações encontrem Services utilizando seus nomes DNS.
CNI / Kindnet

O componente de rede fornece a conectividade necessária entre Pods e nodes do cluster.

No ambiente Kind, o kindnet é utilizado para a rede dos Pods.

