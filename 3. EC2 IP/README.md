# AWS Certified Solutions Architect – Associate  
## EC2 Networking & Advanced Concepts

Esta aula cobre tópicos **críticos e recorrentes na prova SAA**, com foco em **EC2 Networking e comportamento avançado de instâncias**.

---

## 🎯 Objetivos da Aula
Ao final desta aula, você será capaz de:
- Diferenciar **Private IP, Public IP e Elastic IP**
- Escolher corretamente **EC2 Placement Groups**
- Entender e aplicar **Elastic Network Interfaces (ENI)**
- Explicar quando e por que usar **EC2 Hibernate**
- Resolver questões de prova com segurança

---

## 1️⃣ Private IP vs Public IP vs Elastic IP

### 🔹 Public IP
- Identifica a instância **na Internet (WWW)**
- Deve ser **globalmente único**
- Pode ser **geolocalizado**
- **Muda** quando a instância é **stop/start**

✅ Usos comuns:
- SSH direto
- Ambientes simples ou temporários

⚠️ **Não recomendado** para arquiteturas críticas

---

### 🔹 Private IP
- Identifica a instância **apenas dentro da VPC**
- Deve ser único **dentro da rede privada**
- Redes privadas diferentes **podem reutilizar os mesmos IPs**
- Comunicação externa via:
  - Internet Gateway (IGW)
  - NAT Gateway / NAT Instance

✅ Usos comuns:
- Backends
- Bancos de dados
- Comunicação interna segura

---

### 🔹 Elastic IP (EIP)
- IP **público estático (IPv4)**
- **Não muda** após stop/start
- Pode ser **reatribuído rapidamente** (failover)
- Limite padrão: **5 EIPs por região**
- **Cobra** se não estiver associado a uma instância ativa

⚠️ **Cai em prova**
> Elastic IP geralmente indica **má arquitetura**

✅ Alternativas recomendadas:
- Route 53 (DNS)
- Load Balancer

---

## 2️⃣ EC2 Placement Groups

Controlam **como instâncias EC2 são posicionadas fisicamente**.

### 🔹 Cluster
- Mesma Availability Zone
- Instâncias fisicamente próximas
- **Baixa latência + alta largura de banda (10–25+ Gbps)**

✅ Ideal para:
- HPC
- Big Data
- Machine Learning

❌ Risco: falha da AZ

---

### 🔹 Spread
- Instâncias em **hardwares diferentes**
- Pode abranger **múltiplas AZs**
- Limite: **7 instâncias por AZ**

✅ Ideal para:
- Aplicações críticas
- Alta disponibilidade

---

### 🔹 Partition
- Instâncias divididas em **partições isoladas**
- Escala para **centenas de instâncias**
- Metadados informam a partição

✅ Ideal para:
- Hadoop
- Cassandra
- Kafka
- HBase

---

### 📌 Resumo rápido

| Tipo | Objetivo |
|------|----------|
| Cluster | Performance máxima |
| Spread | Alta disponibilidade |
| Partition | Big Data distribuído |

---

## 3️⃣ Elastic Network Interfaces (ENI)

### O que é?
- **Placa de rede virtual** dentro da VPC
- Recurso **independente da EC2**
- Associada a **uma AZ específica**

### Atributos
- Primary Private IPv4
- IPs privados secundários
- Elastic IP (opcional)
- Security Groups
- MAC Address

### Pontos importantes
- Pode ser criada separadamente
- Pode ser **movida entre instâncias**
- Muito usada para **failover**

📌 **Cai em prova**
> ENI permite mover IPs privados e regras de segurança entre EC2s

---

## 4️⃣ EC2 Hibernate

### Estados de uma EC2

| Ação | Comportamento |
|------|---------------|
| Stop | EBS preservado |
| Terminate | EBS pode ser destruído |
| Hibernate | RAM salva em disco |

---

### O que é Hibernate?
- Salva o **conteúdo da RAM** em EBS
- Retomada rápida
- Aplicação continua do ponto exato

### Inicialização
- Primeira inicialização:
  - SO boot
  - User Data executa
- Após Hibernate:
  - Memória restaurada
  - Caches já aquecidos

### Limitações
- Apenas instâncias suportadas
- Root volume deve ser EBS
- RAM ≤ limite suportado

✅ Use quando:
- Startup é lento
- Aplicação stateful
- Ambientes analíticos/dev

---

## 5️⃣ Pegadinhas Clássicas de Prova

- ❌ Elastic IP ≠ Alta disponibilidade
- ✅ Load Balancer > Elastic IP
- ❌ Public IP é confiável a longo prazo
- ✅ Private IP é padrão arquitetural
- ❌ Spread não escala
- ✅ Partition escala
- ❌ ENI não é global
- ✅ Hibernate preserva RAM

---

## 6️⃣ Revisão Rápida

- **Private IP** → comunicação interna
- **Public IP** → acesso externo
- **Elastic IP** → IP fixo (evitar)
- **Placement Groups** → controle físico
- **ENI** → failover de rede
- **Hibernate** → startup rápido

---

