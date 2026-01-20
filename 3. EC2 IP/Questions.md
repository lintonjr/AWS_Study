## Pergunta 1

You have launched an EC2 instance that will host a NodeJS application. After installing all the required software and configured your application, you noted down the EC2 instance public IPv4 so you can access it. Then, you stopped and then started your EC2 instance to complete the application configuration. After restart, you can't access the EC2 instance, and you found that the EC2 instance public IPv4 has been changed. What should you do to assign a fixed public IPv4 to your EC2 instance?

- [ ] Allocate an Elastic IP and assign it to your EC2 instance
- [ ] From inside your EC2 instance OS, change network configuration from DHCP to static and assign it a public IPv4
- [ ] Contact AWS Support and request a fixed public IPv4 to your EC2 instance
- [ ] This can't be done, you can only assign a fixed private IPv4 to your EC2 instance

<details>
  <summary><strong>Explicação</strong></summary>

  **Allocate an Elastic IP and assign it to your EC2 instance** ✅

When you stop and start an EC2 instance, the **public IPv4 can change**. To keep a **fixed public IPv4**, you should **allocate an Elastic IP (EIP)** and **associate it** with the instance (or with its network interface).
</details>

## Pergunta 2

You have an application performing big data analysis hosted on a fleet of EC2 instances. You want to ensure your EC2 instances have the highest networking performance while communicating with each other. Which EC2 Placement Group should you choose?

- [ ] Spread Placement Group  
- [ ] Cluster Placement Group
- [ ] Partition Placement Group  

<details>
  <summary><strong>Explicação</strong></summary>

  **Cluster Placement Group** ✅ *Correto*

For **the highest network performance between EC2 instances**, use a **Cluster Placement Group**.

- It places instances **physically close together** (typically in the **same Availability Zone**) to minimize latency.
- Provides **high throughput** and **low-latency networking**, ideal for **HPC**, **big data**, **distributed analytics**, and workloads that do lots of **east-west traffic** (instance-to-instance).

Quick comparison:
- **Spread**: maximizes availability by spreading instances across distinct hardware (best for critical small fleets).
- **Partition**: isolates groups of instances into partitions (useful for large distributed systems like HDFS/Cassandra).
- **Cluster**: packs instances together for **best performance** (best for big data/HPC).

</details>

## Pergunta 3

You have a critical application hosted on a fleet of EC2 instances in which you want to achieve maximum availability when there's an AZ failure. Which EC2 Placement Group should you choose?

- [ ] Cluster Placement Group  
- [ ] Partition Placement Group  
- [ ] Spread Placement Group

<details>
  <summary><strong>Explicação</strong></summary>

  **Spread Placement Group** ✅ *Correto*

To maximize **availability and fault tolerance**, choose a **Spread Placement Group**.

- It places instances on **distinct underlying hardware** (separate racks/hosts), reducing the chance that a single hardware failure impacts multiple instances.
- It can also spread instances across **multiple Availability Zones**, improving resilience against an **AZ-level failure**.

Quick comparison:
- **Cluster**: best network performance (low latency/high throughput), but less fault tolerant.
- **Partition**: isolates groups into partitions (good for large distributed systems), but not as strict as Spread for per-instance hardware isolation.
- **Spread**: best for **critical workloads** that need **maximum availability**.

</details>

## Pergunta 4

Elastic Network Interface (ENI) can be attached to EC2 instances in another AZ.

- [ ] True  
- [ ] False

<details>
  <summary><strong>Explicação</strong></summary>

  **False** ✅ *Correto*  

**ENIs (Elastic Network Interfaces) are tied to a specific Availability Zone (AZ).**  
That means you **cannot** attach an ENI created in **AZ A** to an EC2 instance that is running in **AZ B**.

If you need an interface in another AZ, you must **create a new ENI in that AZ** (or move/replace the instance within the same AZ as the ENI).

</details>

## Pergunta 5

The following are true regarding EC2 Hibernate, EXCEPT:

- [ ] EC2 Instance Root Volume must be an Instance Store volume
- [ ] Supports On-Demand and Reserved Instances  
- [ ] EC2 Instance RAM must be less than 150GB  
- [ ] EC2 Instance Root Volume type must be an EBS volume  

<details>
  <summary><strong>Explicação</strong></summary>

  **EC2 Instance Root Volume must be an Instance Store volume** ✅ *Correto (EXCEPT)*

The question asks for the statement that is **NOT true** about **EC2 Hibernate**.

✅ **To use Hibernate, the root volume must be an _EBS_ volume (not Instance Store)** and it must be **encrypted** to protect the RAM snapshot written to disk.

Other key rules (in general):
- Hibernate is supported for **On-Demand** and **Reserved Instances**.
- There is a memory limit (commonly referenced as **< 150 GB RAM**) for hibernation eligibility, depending on instance type.

So the incorrect statement (the **EXCEPT**) is:  
**"EC2 Instance Root Volume must be an Instance Store volume"**.

</details>



