## Pergunta 1

**Which EC2 Purchasing Option can provide you the biggest discount, but it is not suitable for critical jobs or databases?**

- [ ] Convertible Reserved Instances  
- [ ] Dedicated Hosts  
- [ ] Spot Instances

<details>
  <summary><strong>Explicação (spoiler)</strong></summary>

  **Spot Instances** ✅ *Correto*

  Spot Instances are good for short workloads and this is the cheapest EC2 Purchasing Option. But, they are less reliable because you can lose your EC2 instance.

</details>

## Pergunta 2

**What should you use to control traffic in and out of EC2 instances?**

- [ ] Network Access Control List (NACL)  
- [ ] Security Groups
- [ ] IAM Policies  

<details>
  <summary><strong>Explicação (spoiler)</strong></summary>

  **Security Groups** ✅ *Correto*

  Security Groups operate at the EC2 instance level and can control traffic.

</details>

## Pergunta 3

**How long can you reserve an EC2 Reserved Instance?**

- [ ] 1 or 3 years  
- [ ] 2 or 4 years  
- [ ] 6 months or 1 year  
- [ ] Anytime between 1 and 3 years  

<details>
  <summary><strong>Explicação (spoiler)</strong></summary>

  **1 or 3 years** ✅ *Correto* 

  EC2 Reserved Instances can be reserved for 1 or 3 years only.

</details>

## Pergunta 4

**You would like to deploy a High-Performance Computing (HPC) application on EC2 instances. Which EC2 instance type should you choose?**

- [ ] Storage Optimized  
- [ ] Compute Optimized  
- [ ] Memory Optimized  
- [ ] General Purpose  

<details>
  <summary><strong>Explicação (spoiler)</strong></summary>
  
  **Compute Optimized** ✅ *Correto*

  Compute Optimized EC2 instances are great for compute-intensive workloads requiring high-performance processors (e.g., batch processing, media transcoding, high-performance computing, scientific modeling & machine learning, and dedicated gaming servers).

</details>

## Pergunta 6

**You are preparing to launch an application that will be hosted on a set of EC2 instances. This application needs some software installation and some OS packages need to be updated during the first launch. What is the best way to achieve this when you launch the EC2 instances?**

- [ ] Connect to each EC2 instance using SSH, then install the required software and update your OS packages manually  
- [ ] Write a bash script that installs the required software and updates to your OS, then contact AWS Support and provide them with the script. They will run it on your EC2 instances at launch  
- [ ] Write a bash script that installs the required software and updates to your OS, then use this script in EC2 User Data when you launch your EC2 instances

<details>
  <summary><strong>Explicação (spoiler)</strong></summary>

  **Write a bash script that installs the required software and updates to your OS, then use this script in EC2 User Data when you launch your EC2 instances** ✅ *Correto*  

  EC2 User Data is used to bootstrap your EC2 instances using a bash script. This script can contain commands such as installing software/packages, download files from the Internet, or anything you want.

</details>

## Pergunta 12

**Spot Fleet is a set of Spot Instances and optionally ...............**

- [ ] Reserved Instances  
- [ ] On-Demand Instances  
- [ ] Dedicated Hosts  
- [ ] Dedicated Instances  

<details>
  <summary><strong>Explicação (spoiler)</strong></summary>

  **On-Demand Instances** ✅ *Correto* 

  Spot Fleet is a set of Spot Instances and optionally On-Demand Instances. It allows you to automatically request Spot Instances with the lowest price.

</details>
