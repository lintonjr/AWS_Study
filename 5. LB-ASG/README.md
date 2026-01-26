# Aula Completa – Elastic Load Balancing & Auto Scaling
## AWS Certified Solutions Architect – Associate

Esta aula aborda **Elastic Load Balancing (ELB)** e **Auto Scaling**, dois dos pilares mais importantes da certificação **AWS Certified Solutions Architect – Associate**.

O objetivo aqui não é decorar nomes de serviços, mas **entender o raciocínio arquitetural que a AWS cobra na prova**.

---

## Objetivos da Aula

Ao final desta aula, você será capaz de:

- Entender por que Load Balancers são necessários
- Diferenciar corretamente ALB, NLB, CLB e GWLB
- Explicar Cross-Zone Load Balancing
- Entender profundamente Auto Scaling Groups (ASG)
- Escolher corretamente ASG Scaling Policies
- Entender SSL/TLS em Load Balancers
- Resolver questões de prova com confiança

---

## O Problema Real

Uma aplicação rodando em uma única EC2 sofre com:
- Ponto único de falha
- Falta de escalabilidade
- Downtime em deploys

A AWS resolve isso com:
- Elastic Load Balancing
- Auto Scaling

---

## Elastic Load Balancer (ELB)

Serviço totalmente gerenciado que:
- Distribui tráfego automaticamente
- Executa health checks
- Integra com Auto Scaling
- Suporta SSL/TLS

Na prova, ELB sempre significa **alta disponibilidade**.

---

## Tipos de Load Balancer

### Classic Load Balancer (CLB) – Legado
Usado apenas para aplicações antigas. Evite se não for explicitamente citado.

### Application Load Balancer (ALB)
- Camada 7 (HTTP/HTTPS)
- Roteamento por path, host e headers
- Ideal para aplicações web, APIs e microservices

### Network Load Balancer (NLB)
- Camada 4 (TCP/UDP/TLS)
- Altíssima performance
- IP fixo por AZ

### Gateway Load Balancer (GWLB)
- Inspeção de tráfego
- Firewalls e IDS/IPS
- Camadas 3 e 4

---

## Cross-Zone Load Balancing

Distribui tráfego igualmente entre instâncias em diferentes AZs.

- ALB: sempre ativo
- NLB: opcional
- CLB: opcional

---

## Auto Scaling Group (ASG)

Garante:
- Escalabilidade automática
- Auto-healing
- Alta disponibilidade

Componentes:
- Launch Template
- Min / Max / Desired Capacity

---

## ASG Scaling Policies

### Target Tracking
Mantém uma métrica alvo automaticamente.

### Step Scaling
Escala por faixas de métricas.

### Simple Scaling
Baseado em um único alarme.

### Scheduled Scaling
Escala por horário.

---

## ALB + ASG

Combinação clássica para:
- Alta disponibilidade
- Escalabilidade automática

---

## SSL / TLS e ACM

- SSL termination no Load Balancer
- Certificados gerenciados pelo AWS Certificate Manager
- Renovação automática

Na prova: **sempre escolha ACM**.

---

## Resumo Mental

- Web / API → ALB
- TCP / UDP → NLB
- Segurança → GWLB
- Escalar EC2 → ASG
- SSL → ACM

---

## Conclusão

Dominar Load Balancers e Auto Scaling garante alto desempenho na prova AWS SAA.

---

Material de estudo – AWS Certified Solutions Architect – Associate

