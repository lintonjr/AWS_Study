# AWS SAA — EC2 Fundamentals (Aula)

Material de estudo focado na certificação **AWS Certified Solutions Architect – Associate (SAA)** cobrindo os fundamentos de **Amazon EC2**, com foco em conceitos, práticas e pegadinhas típicas de prova.

---

## Sumário
- [Objetivos da aula](#objetivos-da-aula)
- [1) Introdução a EC2](#1-introdução-a-ec2)
- [2) EC2 User Data and Bootstrap](#2-ec2-user-data-and-bootstrap)
- [3) EC2 Instance Types Basics](#3-ec2-instance-types-basics)
- [4) Security Groups & Classic Ports Overview](#4-security-groups--classic-ports-overview)
- [5) EC2 SSH](#5-ec2-ssh)
- [6) EC2 Instance Connect](#6-ec2-instance-connect)
- [7) EC2 Instance Roles](#7-ec2-instance-roles)
- [8) EC2 Instance Purchasing Options](#8-ec2-instance-purchasing-options)
- [9) Spot Instances & Spot Fleet](#9-spot-instances--spot-fleet)
- [10) EC2 Instances Launch Types](#10-ec2-instances-launch-types)
- [Checklist de revisão](#checklist-de-revisão)
- [Mini-lab sugerido (20–30 min)](#mini-lab-sugerido-2030-min)

---

## Objetivos da aula
Ao final, você deve conseguir:
- Explicar o que é EC2 e como ela se encaixa em uma arquitetura AWS.
- Lançar instâncias com **User Data**, escolher **instance types**, configurar **Security Groups**, acessar via **SSH/Instance Connect**, usar **IAM Roles**, e comparar **opções de compra** (On-Demand, Reserved, Savings Plans, Spot).
- Reconhecer pegadinhas comuns de prova.

---

## 1) Introdução a EC2
**Amazon EC2 (Elastic Compute Cloud)** é o serviço de computação que fornece **máquinas virtuais** sob demanda na AWS.

### Conceitos essenciais
- **Instance**: a VM rodando (compute).
- **AMI (Amazon Machine Image)**: “imagem” do SO + configurações (ex.: Amazon Linux, Ubuntu).
- **EBS (Elastic Block Store)**: disco persistente (root volume e volumes adicionais).
- **ENI (Elastic Network Interface)**: interface de rede com IPs e security groups.
- **AZ (Availability Zone)**: instância roda em **uma AZ** dentro de uma região.
- **Elastic IP**: IP público fixo (atenção: pode ter custo se ocioso).
- **Auto Scaling / ELB**: escalar e balancear.

### Quando usar EC2?
- Workloads que precisam de controle do SO, pacotes, runtime e agentes.
- Aplicações stateful ou com dependências específicas (quando containers/serverless não atendem).

### Pegadinha de prova
- EC2 é por AZ. Resiliência em múltiplas AZ exige **mais de uma instância em AZs diferentes** + balanceamento.

---

## 2) EC2 User Data and Bootstrap
**User Data** é um script fornecido no lançamento para **bootstrap** (instalar dependências, baixar app, configurar serviços).

### Regras importantes
- User Data roda **na primeira inicialização** por padrão (dependendo do SO/cloud-init).
- Deve ser **idempotente** (se rodar mais de uma vez, não pode quebrar).
- Melhor prática: usar para setup inicial + **buscar configuração** de S3/SSM Parameter Store/Secrets Manager.

### Exemplo (Linux - cloud-init / bash)
```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl enable httpd
systemctl start httpd
echo "Hello from EC2 - $(hostname)" > /var/www/html/index.html
```

### Pegadinhas de prova
- “Preciso instalar software automaticamente ao lançar instância” → **User Data**.
- “Preciso garantir config central/segura” → preferir **SSM/Parameter Store/Secrets Manager** e/ou “bake” em AMI quando fizer sentido.

---

## 3) EC2 Instance Types Basics
Instance types definem **CPU, memória, rede e storage**.
- Cheque o link: https://instances.vantage.sh/

### Famílias comuns (para prova)
- **General purpose (t, m)**: equilíbrio (web/app). `t` = burstable.
- **Compute optimized (c)**: CPU intensa (batch, game servers).
- **Memory optimized (r, x)**: memória (cache, in-memory DB).
- **Storage optimized (i, d)**: IOPS/throughput local alto (DB, analytics).
- **Accelerated (p, g, inf)**: GPU/ML.

### Burstable (família T)
- Acumula **créditos de CPU** e “bursta” quando precisa.
- Bom para cargas com picos; ruim para CPU sustentada sem planejamento.

### Pegadinha de prova
- “Aplicação com CPU constante 80–90%” → evite `t*`, prefira `m/c/r` conforme o perfil.

---

## 4) Security Groups & Classic Ports Overview
**Security Group (SG)** é um firewall **stateful** no nível da instância/ENI:
- Se você permite inbound, o retorno é permitido automaticamente (**stateful**).
- Regras são **allow-only** (não existe deny explícito em SG).
- Regras podem referenciar **CIDR** ou **outros SGs** (muito usado entre camadas).

### Bom saber
- Security Groups podem ser usados em varias instâncias
- Tem escopo por região/VPC Combination
- SSH é bom ser mantido em um security group a parte
- Se você tem timeout, na maioria das vezes é um problema de SG
- Se você tem um connection refused, jamais será um problema de SG, pois se trata de application error, para application responder deve primeiramente ter funcionado o inbound do SG
- Todo inbound é bloqueado por padrão
- Todo outbound é liberado por padrão
- SG pode autorizar outros SG em inbound rule

### Portas clássicas (cai muito)
- **22**: SSH (Linux)
- **3389**: RDP (Windows)
- **80**: HTTP
- **443**: HTTPS
- **ICMP**: ping (se habilitado)

### Boas práticas de SG
- Abrir **22** apenas para seu IP (ou bastion/VPN), nunca `0.0.0.0/0` em produção.
- Para app em camadas:
  - SG do ALB permite 80/443 do mundo
  - SG da app permite porta do app **apenas do SG do ALB**
  - SG do banco permite 3306/5432 **apenas do SG da app**

### Pegadinhas de prova
- “Não consigo acessar via SSH” → verifique SG inbound 22 + rota/NACL/subnet + key pair + usuário correto.

---

## 5) EC2 SSH
### Pré-requisitos do SSH
- Instância Linux com **key pair** associado.
- Porta **22 inbound** liberada no SG para o seu IP.
- Conectividade: IP público (ou via bastion/VPN/SSM).

### Comandos comuns
```bash
chmod 400 minha-chave.pem
ssh -i minha-chave.pem ec2-user@<public-ip>
# ou ubuntu@<public-ip> para Ubuntu
```

### Erros comuns
- Permissão errada do arquivo PEM (`chmod 400`)
- Usuário errado (Amazon Linux = `ec2-user`, Ubuntu = `ubuntu`)
- SG não liberou 22 do seu IP
- Subnet privada sem rota/sem bastion/sem caminho de rede

---

## 6) EC2 Instance Connect
**EC2 Instance Connect (EIC)** facilita SSH sem distribuir PEM para todo mundo, enviando chave temporária (conforme setup).

### Quando usar
- Acesso operacional simplificado via Console/CLI.
- Útil em ambientes controlados com políticas restritas.

### Pontos de atenção
- Requer compatibilidade de AMI e configuração correta.
- Ainda depende de conectividade (IP público ou caminho via rede/bastion).

### Pegadinha de prova
- “Acessar instância sem distribuir PEM para a equipe” → EIC ou (muito comum em prova) **SSM Session Manager**.

---

## 7) EC2 Instance Roles
**Instance Role** = IAM Role anexada à EC2 via **Instance Profile**.

### Por que isso é essencial?
- Permite que a EC2 acesse serviços AWS (S3, DynamoDB, SSM etc.) **sem access keys fixas**.
- Credenciais temporárias via **STS** (mais seguro).

### Pegadinha de prova
- “Melhor forma de dar permissão para EC2 acessar S3?” → **IAM Role**, nunca access key em arquivo.

---

## 8) EC2 Instance Purchasing Options
### 8.1 On-Demand
- Paga por uso.
- Flexível, ideal para cargas imprevisíveis/curtas.

### 8.2 Reserved Instances (RI)
- Compromisso 1 ou 3 anos.
- Desconto vs On-Demand.
- Bom para workloads estáveis.
- **Standard** (mais desconto, menos flexível) ou **Convertible** (mais flexível, menos desconto).

### 8.3 Savings Plans
- Compromisso de **gasto por hora** (1–3 anos).
- **Compute Savings Plans** (mais flexível) e **EC2 Instance Savings Plans** (mais específico).
- Em prova, é comum aparecer como melhor custo com flexibilidade.

### 8.4 Dedicated Hosts / Dedicated Instances
- Isolamento físico/dedicado.
- Usado por compliance/licenciamento (ex.: BYOL).

### Pegadinhas de prova
- “Carga estável por anos” → **Reserved** ou **Savings Plans**.
- “Quer flexibilidade entre famílias/regions” → **Compute Savings Plans** costuma ser a resposta.
- “Licença presa a hardware físico” → **Dedicated Host**.

---

## 9) Spot Instances & Spot Fleet
### Spot Instances
- Grande desconto por usar capacidade ociosa.
- **Pode ser interrompida** pela AWS (aviso geralmente ~2 minutos).
- Ideal para cargas tolerantes à interrupção: batch, CI/CD runners, render, big data.

### Spot Fleet
- Frota que busca manter capacidade-alvo usando Spot (e opcionalmente On-Demand).
- Mistura instance types e AZs para aumentar chance de capacidade.

### Pegadinhas de prova
- “Precisa de baixo custo e tolera interrupção” → **Spot**.
- “Manter X capacidade com Spot com fallback/estratégia” → **Spot Fleet** (ou ASG com Mixed Instances).

---

## 10) EC2 Instances Launch Types
Aqui é comum confundir “forma de lançar” vs “opção de compra”.

### Padrões comuns (para prova)
- **Single instance** (manual): simples, pouca resiliência.
- **Auto Scaling Group (ASG)**: escala e substitui instâncias automaticamente.
- **Launch Template / Launch Configuration**:
  - **Launch Template** é o padrão moderno.
- **Placement Groups** (quando cai): cluster / spread / partition.
- **Conectividade**: public subnet (com public IP) vs private subnet.
- **Acesso**: SSH vs Instance Connect vs SSM.

### Pegadinhas de prova
- “Alta disponibilidade” → **ASG em múltiplas AZ + Load Balancer**.
- “Mudanças frequentes no padrão de lançamento” → **Launch Template**.

---

## Checklist de revisão
- ✅ EC2 conceitos: AMI, EBS, ENI, AZ  
- ✅ User Data: bootstrap e idempotência  
- ✅ Instance types: famílias e créditos de CPU (T)  
- ✅ Security Groups: stateful, allow-only, portas comuns  
- ✅ SSH: key, usuário, SG, rede  
- ✅ Instance Connect: acesso facilitado (lembrar do SSM)  
- ✅ Instance Roles: acesso seguro a AWS sem keys  
- ✅ Purchasing: On-Demand, RI, Savings Plans, Dedicated  
- ✅ Spot/Spot Fleet: barato + interrupção  
- ✅ Launch patterns: ASG/Launch Template + multi-AZ  

---

## Mini-lab sugerido (20–30 min)
1) Lance uma EC2 (Amazon Linux ou Ubuntu) em subnet pública  
2) Configure SG: 22 apenas seu IP e 80 aberto (para teste)  
3) Use User Data para instalar `httpd/nginx` e publicar uma página  
4) Acesse via SSH e valide `/var/www/html`  
5) Crie uma IAM Role com `AmazonS3ReadOnlyAccess` (ou policy mínima) e anexe à instância  
6) Dentro da EC2, rode `aws sts get-caller-identity` e faça um `aws s3 ls` (se tiver bucket)  

---
