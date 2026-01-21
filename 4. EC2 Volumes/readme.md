# AWS Certified Solutions Architect – Associate  
## Aula: EC2 Storage & File Systems

Esta aula aborda **armazenamento no EC2**, um dos tópicos mais cobrados na certificação **AWS Certified Solutions Architect – Associate**.  
O foco está em **quando usar cada serviço**, **impacto em arquitetura**, **custos**, **performance** e **alta disponibilidade**.

---

## 📦 1. Amazon EBS (Elastic Block Store)

O **Amazon EBS** é um serviço de **block storage** usado principalmente com instâncias EC2.

### Conceitos Fundamentais

- É um **disco de rede** (não é físico)
- Comunicação via rede → pequena latência
- Pode ser **anexado e desanexado rapidamente**
- **Limitado a uma Availability Zone (AZ)**
- Para mover entre AZs → **Snapshot**

### Características Importantes

- Capacidade provisionada (GB + IOPS)
- Você paga por **toda capacidade provisionada**
- Tamanho e performance podem ser aumentados **on-the-fly**

---

## 📸 2. EBS Snapshots

Snapshots são **backups point-in-time** de volumes EBS.

### Principais Pontos

- Não é obrigatório desanexar o volume (mas é recomendado)
- Snapshots são armazenados no S3 (gerenciado pela AWS)
- Podem ser copiados entre **AZs e Regions**

### Casos de Uso

- Backup
- Migração entre AZs
- Criação de AMIs
- Disaster Recovery

---

## 🗄️ 3. Recursos Avançados de Snapshots

### Snapshot Archive
- Até **75% mais barato**
- Restore leva de **24 a 72 horas**
- Ideal para backups de longo prazo

### Recycle Bin
- Recupera snapshots deletados acidentalmente
- Retenção configurável: **1 dia a 1 ano**

### Fast Snapshot Restore (FSR)
- Elimina latência no primeiro acesso
- **Custo adicional**
- Usado em workloads críticos

---

## 🖼️ 4. AMI (Amazon Machine Image)

Uma **AMI** é um template para criar instâncias EC2.

AMI tem escopo Regional

### O que contém uma AMI?

- Sistema Operacional
- Aplicações instaladas
- Configurações
- EBS Snapshots

### Tipos de AMI

- **AMI pública** (AWS)
- **AMI customizada** (sua)
- **AMI do Marketplace**

### Processo de Criação

1. Criar e configurar uma EC2
2. Parar a instância (integridade)
3. Criar AMI (gera snapshots)
4. Lançar novas instâncias a partir da AMI

---

## ⚡ 5. EC2 Instance Store

O **Instance Store** é armazenamento **local físico** no host da EC2.

### Características

- Altíssima performance de I/O
- **Dados são perdidos ao parar a instância**
- Storage **ephemeral**
- Backup é responsabilidade do usuário

### Casos de Uso

- Cache
- Buffer
- Dados temporários
- Scratch space

---

## 💽 6. Tipos de Volumes EBS

### SSD (Boot permitido)

#### gp3 / gp2 – General Purpose SSD
- Uso geral
- Boot volume
- Ambientes de dev/test
- gp3 permite escalar IOPS e throughput independentemente

#### io1 / io2 – Provisioned IOPS SSD
- Bancos de dados
- Workloads críticos
- Latência consistente
- io2 Block Express → até **256.000 IOPS**

---

### HDD (Boot NÃO permitido)

#### st1 – Throughput Optimized HDD
- Big Data
- Data Warehouse
- Log processing
- Até **500 MiB/s**

#### sc1 – Cold HDD
- Dados raramente acessados
- Menor custo
- Até **250 MiB/s**

---

## 🔗 7. EBS Multi-Attach (io1 / io2)

Permite anexar **um mesmo volume EBS** a **múltiplas EC2** na **mesma AZ**.

### Regras Importantes

- Até **16 instâncias**
- Todas têm leitura e escrita
- Aplicação deve gerenciar concorrência
- Requer **file system cluster-aware**

### Caso Clássico
- Aplicações Linux clusterizadas (ex: Teradata)

---

## 🔐 8. EBS Encryption

Criptografia **nativa e transparente** usando **AWS KMS (AES-256)**.

### O que é criptografado?

- Dados em repouso
- Dados em trânsito
- Snapshots
- Volumes criados a partir do snapshot

### Criptografar Volume Existente

1. Criar snapshot
2. Copiar snapshot com encryption
3. Criar novo volume criptografado
4. Anexar à instância

---

## 📂 9. Amazon EFS (Elastic File System)

O **EFS** é um **file system NFS gerenciado**.

### Características

- Montado em **centenas de EC2**
- Funciona em **Multi-AZ**
- Totalmente gerenciado
- **Pay-per-use**
- Apenas **Linux (POSIX)**

### Casos de Uso

- WordPress
- Content management
- Compartilhamento de arquivos
- Web servers

---

## 🚀 10. Performance e Classes do EFS

### Performance Modes
- **General Purpose** (default)
- **Max I/O** (Big Data, media processing)

### Throughput Modes
- Bursting
- Provisioned
- Elastic (auto scaling)

### Storage Classes
- Standard
- EFS-IA
- Archive
- One Zone / One Zone-IA

---

## ⚖️ 11. EBS vs EFS vs Instance Store

| Serviço | Tipo | AZ | Multi-Attach | Persistência | Caso Ideal |
|------|-----|----|-------------|-------------|-----------|
| EBS | Block | Single AZ | Não* | Sim | EC2 + DB |
| EFS | File | Multi-AZ | Sim | Sim | WordPress |
| Instance Store | Local | Host | Não | Não | Cache |

\* Exceto io1/io2 Multi-Attach

---

## 🧠 Dicas de Prova (EXAME)

- Precisa compartilhar arquivos entre instâncias? → **EFS**
- Precisa de disco para banco de dados? → **EBS io2**
- Precisa de alta performance temporária? → **Instance Store**
- Migrar EBS entre AZ? → **Snapshot**
- Boot volume? → **SSD apenas**

---
