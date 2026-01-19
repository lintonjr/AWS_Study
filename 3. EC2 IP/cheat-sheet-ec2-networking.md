# AWS SAA – EC2 Networking & Advanced Concepts  
## Cheat Sheet

Material de revisão rápida para **AWS Certified Solutions Architect – Associate**, focado em tópicos recorrentes de **EC2 Networking e comportamento avançado de instâncias**.

---

## 🌐 Private IP vs Public IP vs Elastic IP

### 🔹 Private IP
- Comunicação **interna na VPC**
- Único **dentro da VPC**
- Pode ser reutilizado em **VPCs diferentes**
- **Não acessível pela Internet**
- Padrão para arquiteturas seguras

👉 Usar para:
- Backends
- Bancos de dados
- Microservices

---

### 🔹 Public IP
- Comunicação com a **Internet (WWW)**
- **Único globalmente**
- Pode ser **geolocalizado**
- ⚠️ **Muda** após `stop/start` da EC2

👉 Usar para:
- Acesso externo simples
- SSH, testes, demos

---

### 🔹 Elastic IP (EIP)
- IP **público fixo (IPv4)**
- **Não muda** após stop/start
- Pode ser **reatribuído rapidamente** (failover)
- Limite padrão: **5 EIPs por região**
- 💸 Custo se não estiver associado

❗ **Pegadinha de prova**
> Elastic IP **não é boa prática** para alta disponibilidade

✅ Prefira:
- **Load Balancer**
- **Route 53 (DNS)**

---

## 🧱 EC2 Placement Groups

Controlam **onde as instâncias EC2 ficam fisicamente**.

### 🔹 Cluster
- Mesma Availability Zone
- Instâncias **muito próximas**
- 🔥 Altíssima performance
- Baixa latência / alta largura de banda (10–25+ Gbps)

👉 Usar para:
- HPC
- Big Data
- Machine Learning

❌ Risco:
- Falha da AZ afeta todas as instâncias

---

### 🔹 Spread
- Instâncias em **hardwares diferentes**
- Pode abranger **múltiplas AZs**
- Máx: **7 instâncias por AZ**

👉 Usar para:
- Aplicações críticas
- Alta disponibilidade

---

### 🔹 Partition
- Instâncias separadas em **partições**
- Cada partição usa racks diferentes
- Escala para **centenas de instâncias**
- Metadados informam a partição

👉 Usar para:
- Hadoop
- Cassandra
- Kafka
- HBase

---

### 📌 Resumo rápido

| Tipo | Use quando precisar de |
|------|------------------------|
| Cluster | Performance |
| Spread | Alta disponibilidade |
| Partition | Big Data escalável |

---

## 🔌 Elastic Network Interface (ENI)

### O que é?
- **Placa de rede virtual** dentro da VPC
- Recurso **independente da EC2**
- Associada a **uma AZ específica**

### Pode ter:
- Private IPv4 (primário e secundários)
- Elastic IP
- Security Groups
- MAC Address

### Destaques
- Pode ser **movida entre EC2s**
- Excelente para **failover**
- Muito cobrada em prova

📌 Pegadinha:
> ENI **não é global**, é por AZ

---

## 💤 EC2 Hibernate

### Estados da EC2

| Ação | O que acontece |
|------|---------------|
| Stop | EBS preservado |
| Terminate | EBS pode ser destruído |
| Hibernate | **RAM salva em disco** |

---

### O que é Hibernate?
- Salva a **memória RAM** no EBS
- Retomada extremamente rápida
- Aplicação continua do ponto exato

### Quando usar
- Startup lento
- Aplicação stateful
- Ambientes de dev e analytics

### Limitações
- Apenas instâncias suportadas
- Root volume deve ser **EBS**
- Limite de RAM

📌 Cai em prova:
> Stop ≠ Hibernate  
> Hibernate preserva RAM, Stop não

---

## ⚠️ Pegadinhas Clássicas de Prova

- ❌ Elastic IP ≠ Alta disponibilidade  
- ❌ Public IP é confiável a longo prazo  
- ❌ Spread Group não escala  
- ❌ ENI não é global  
- ✅ Load Balancer > Elastic IP  
- ✅ Private IP é padrão  
- ✅ Partition escala  
- ✅ Hibernate preserva RAM  

---

## ✅ Resumo Ultra-Rápido

- **Private IP** → comunicação interna  
- **Public IP** → acesso externo  
- **Elastic IP** → IP fixo (evitar)  
- **Cluster** → performance  
- **Spread** → alta disponibilidade  
- **Partition** → Big Data  
- **ENI** → failover de rede  
- **Hibernate** → startup rápido  

---
