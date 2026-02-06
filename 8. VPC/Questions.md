# Simulado – VPC, CIDR & Networking (AWS SAA)

---

## Pergunta 1

**What does this CIDR `10.0.4.0/28` correspond to?**

- [ ] `10.0.4.0` to `10.0.32.0`
- [ ] `10.0.4.0` to `10.0.4.28`
- [ ] `10.0.0.0` to `10.0.16.0`
- [ ] `10.0.4.0` to `10.0.4.15`

<details>
<summary><strong> Answer</strong></summary>

**10.0.4.0 to 10.0.4.15**

A `/28` CIDR provides **16 IP addresses**  
Formula: `2^(32 - 28) = 16`

</details>

---

## Pergunta 2

You have a corporate network `10.0.0.0/8` and a satellite office `192.168.0.0/16`.  
Which CIDR is acceptable for your AWS VPC if you plan to connect networks later?

- [ ] `172.16.0.0/12`
- [ ] `172.16.0.0/16`
- [ ] `10.0.16.0/16`
- [ ] `192.168.4.0/18`

<details>
<summary><strong> Answer</strong></summary>

**172.16.0.0/16**

VPC CIDRs **must not overlap** with existing networks.  
Also, the **maximum VPC CIDR size is /16**.

</details>

---

## Pergunta 3

You want to create a subnet with capacity for **at least 28 EC2 instances**.  
What is the **minimum subnet size**?

- [ ] `/28`
- [ ] `/27`
- [ ] `/26`
- [ ] `/25`

<details>
<summary><strong> Answer</strong></summary>

**/26**

`/26` provides **64 IPs** (AWS reserves 5 → 59 usable)

</details>

---

##  Pergunta 5

You attached an Internet Gateway to your VPC, but EC2 instances still have no internet access.  
What is **NOT** a possible issue?

- [ ] Route tables missing routes
- [ ] EC2 instances have no public IP
- [ ] Security Group does not allow inbound traffic
- [ ] NACL does not allow outbound traffic

<details>
<summary><strong> Answer</strong></summary>

**Security Group does not allow inbound traffic**

Security Groups are **stateful** — if traffic goes out, return traffic is automatically allowed.

</details>

---

## Pergunta 7

VPC Peering is enabled between VPC A and VPC B.  
Routes were updated in VPC A, but instances still can’t communicate. What is the issue?

- [ ] Check the NACL
- [ ] Check Route Tables in VPC B
- [ ] Check EC2 Security Groups
- [ ] Check DNS Resolution

<details>
<summary><strong> Answer</strong></summary>

**Route tables must be updated in both VPCs**

VPC Peering is **non-transitive** and requires routes on **both sides**.

</details>

---

## Pergunta 8

You have Direct Connect to VPC A and need access to VPC B in another region.  
What should you do?

- [ ] Enable VPC Peering
- [ ] Use a Customer Gateway
- [ ] Use a Direct Connect Gateway
- [ ] Set up a NAT Gateway

<details>
<summary><strong> Answer</strong></summary>

**Direct Connect Gateway**

This allows a single DX connection to access **multiple VPCs across regions**.

</details>

---

## Pergunta 9

When using VPC Endpoints, which AWS services support **Gateway Endpoints**?

- [ ] Amazon S3 & Amazon SQS
- [ ] Amazon SQS & DynamoDB
- [ ] Amazon S3 & DynamoDB

<details>
<summary><strong> Answer</strong></summary>

**Amazon S3 & DynamoDB**

These are the **only services** that support **Gateway Endpoints**.  
All others use **Interface Endpoints (AWS PrivateLink)**.

</details>

---

## Exam Tips

- VPC CIDR **max size: /16**
- Subnets reserve **5 IPs**
- Security Groups = **stateful**
- NACLs = **stateless**
- VPC Peering requires routes on **both sides**
- Gateway Endpoints → **S3 & DynamoDB only**
- Direct Connect Gateway = **multi-VPC, multi-region**

---
