# Aula – Containers & Serverless na AWS (ECS, EKS, Lambda)

---

## Amazon ECS (Elastic Container Service)

O Amazon ECS é um serviço totalmente gerenciado para executar containers Docker na AWS.

### Características
- Gerenciamento nativo AWS
- Integração com IAM, ALB, Auto Scaling e CloudWatch
- Modos de execução:
  - EC2
  - Fargate (serverless)

### Quando usar
- Não precisa de Kubernetes
- Quer simplicidade operacional
- Arquitetura baseada em containers

---

## ECS Cluster

Um ECS Cluster é um agrupamento lógico onde os containers são executados.

### Componentes
- Task Definition
- Task
- Service

### Tipos
- EC2-based
- Fargate-based (mais cobrado na prova)

---

## ECS Auto Scaling

Permite escalar automaticamente tasks ou instâncias.

### Baseado em
- CPU
- Memória
- Métricas do CloudWatch

---

## Amazon ECR (Elastic Container Registry)

Registry privado de imagens Docker.

### Características
- Integração com ECS e EKS
- Scan de vulnerabilidades
- Controle via IAM

---

## Amazon EKS (Elastic Kubernetes Service)

Serviço gerenciado de Kubernetes.

### Quando usar
- Necessidade de Kubernetes padrão
- Portabilidade multi-cloud

### ECS vs EKS
| Critério | ECS | EKS |
|--------|-----|-----|
| Facilidade | Alta | Média |
| Kubernetes | Não | Sim |
| Integração AWS | Alta | Alta |

---

## AWS App Runner

Serviço PaaS para aplicações web e APIs.

### Quando usar
- MVPs
- Aplicações web simples
- Deploy rápido sem infra

---

## AWS App2Container

Ferramenta para modernizar aplicações legadas.

### Uso
- Analisa apps existentes
- Gera Dockerfile e configura ECS

---

## AWS Lambda

Serviço serverless para execução de código.

### Características
- Event-driven
- Escala automática
- Sem gerenciamento de servidores

---

## Lambda Concurrency

Define execuções simultâneas.

### Tipos
- Unreserved
- Reserved
- Provisioned (evita cold start)

---

## Escolha Arquitetural

| Cenário | Serviço |
|------|--------|
| Containers simples | ECS |
| Kubernetes | EKS |
| Serverless | Lambda |
| Web App rápido | App Runner |
| Migrar legado | App2Container |

---

## Conclusão

- ECS: Containers nativos AWS
- EKS: Kubernetes gerenciado
- Lambda: Serverless puro
- App Runner: PaaS simplificado
