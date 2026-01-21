# 🧪 Simulado – EBS, AMI, Instance Store e EFS  
## AWS Certified Solutions Architect – Associate

Este simulado cobre conceitos fundamentais de **armazenamento no EC2**, com foco nos temas mais cobrados na prova:
- EBS e seus tipos
- Snapshots
- AMI
- Instance Store
- EFS
- EBS Encryption e Multi-Attach

---

## ❓ Pergunta 1

You have just terminated an EC2 instance in **us-east-1a**, and its attached EBS volume is now available.  
Your teammate tries to attach it to an EC2 instance in **us-east-1b**, but he can't.  
What is a possible cause for this?

- [ ] He's missing IAM permissions  
- [ ] EBS volumes are locked to an AWS Region  
- [ ] EBS volumes are locked to an Availability  

<details>
<summary>📘 Explanation</summary>

**EBS volumes are locked to an Availability**

EBS volumes are created in a **specific Availability Zone (AZ)** and **cannot be attached to EC2 instances in a different AZ**.

To move an EBS volume across AZs:
1. Create an EBS snapshot  
2. Restore the snapshot in the target AZ  

</details>

---

## ❓ Pergunta 2

You launched an EC2 instance with:
- One **root EBS volume**
- One **additional EBS volume** for data

You plan to **terminate the instance**.  
What happens by default?

- [ ] Both volumes are deleted  
- [ ] Root volume is deleted, additional EBS volume is preserved  
- [ ] Root is preserved, data volume deleted  
- [ ] Both volumes are preserved  

<details>
<summary>📘 Explanation</summary>

**Root volume is deleted, additional EBS volume is preserved** ✅

By default:
- Root volume → `DeleteOnTermination = true`
- Additional EBS volumes → `DeleteOnTermination = false`

</details>

---

## ❓ Pergunta 3

You can use an AMI in **us-east-1** to launch an EC2 instance in any AWS Region.

- [ ] True  
- [ ] False

<details>
<summary>📘 Explanation</summary>

**False** ✅

AMIs are **region-specific**.  
To use it in another region, you must **copy the AMI** first.

</details>

---

## ❓ Pergunta 4

Which EBS volume types **can be used as boot volumes**?

- [ ] gp2, gp3, st1, sc1  
- [ ] gp2, gp3, io1, io2  
- [ ] io1, io2, st1, sc1  

<details>
<summary>📘 Explanation</summary>

**gp2, gp3, io1, io2** ✅

Only **SSD-based volumes** can be boot volumes:
- gp2
- gp3
- io1
- io2

HDD volumes (**st1**, **sc1**) cannot be boot volumes.

</details>

---

## ❓ Pergunta 5

What is **EBS Multi-Attach**?

- [ ] Same volume in multiple AZs  
- [ ] Multiple volumes in one EC2  
- [ ] Same EBS volume attached to multiple EC2 instances in the same AZ  
- [ ] Multiple volumes across AZs to one EC2  

<details>
<summary>📘 Explanation</summary>

**Same EBS volume attached to multiple EC2 instances in the same AZ** ✅

EBS Multi-Attach:
- Works only with **io1 / io2**
- Same AZ only
- Up to **16 EC2 instances**
- Requires **cluster-aware file systems**

</details>

---

## ❓ Pergunta 6

You want to encrypt an **unencrypted EBS volume**. What should you do?

- [ ] Snapshot → Copy snapshot with encryption → Create new volume  
- [ ] Edit volume and enable encryption  
- [ ] Ask AWS Support  
- [ ] Manually copy files to encrypted volume  

<details>
<summary>📘 Explanation</summary>

**Snapshot → Copy snapshot with encryption → Create new volume** ✅

You **cannot encrypt an existing EBS volume directly**.  
Encryption requires the **snapshot-copy process**.

</details>

---

## ❓ Pergunta 7

You want to share the same data as an **NFS drive** across EC2 instances in **multiple AZs**.

- [ ] EBS  
- [ ] EFS  
- [ ] Instance Store  

<details>
<summary>📘 Explanation</summary>

**EFS** ✅

Amazon EFS:
- Managed NFS
- Multi-AZ
- Scales automatically
- Ideal for shared storage

</details>

---

## ❓ Pergunta 8

You want a **high-performance local cache** and don’t care about data persistence.

- [ ] EBS  
- [ ] EFS  
- [ ] Instance Store  

<details>
<summary>📘 Explanation</summary>

**Instance Store** ✅

Instance Store:
- Best I/O performance
- Ephemeral storage
- Perfect for cache, buffers, temp data

</details>

---

## ❓ Pergunta 9

Your database requires **310,000 IOPS**.

What do you recommend?

- [ ] gp2  
- [ ] io1  
- [] EC2 Instance Store  
- [ ] io2 Block Express  

<details>
<summary>📘 Explanation</summary>

**EC2 Instance Store** ✅

For **extreme IOPS**, Instance Store offers the highest raw performance, but:
- Data is ephemeral
- Replication and backups are your responsibility

</details>

---

## 📌 Resumo para a Prova

| Serviço | Quando usar |
|------|------------|
| **EBS** | Disco persistente, 1 EC2 por AZ |
| **EBS Multi-Attach** | Clusters (io1/io2, mesmo AZ) |
| **EFS** | Compartilhamento de arquivos (multi-AZ) |
| **Instance Store** | Cache, buffers, I/O extremo |
| **AMI** | Padronização e boot rápido |

---

## 🎯 Dica de Prova

> **EBS = Block, AZ-bound**  
> **EFS = File, Multi-AZ**  
> **Instance Store = Fast & Ephemeral**

---
