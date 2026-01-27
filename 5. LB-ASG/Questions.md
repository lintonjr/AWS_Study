A gaming application requires **ultra-low latency** and needs to process **millions of requests per second at Layer 4**.  
Which load balancer should be used?

- A. Application Load Balancer  
- B. Network Load Balancer  
- C. Classic Load Balancer  
- D. Gateway Load Balancer  

<details>
  <summary><strong>Answer</strong></summary>

  **B. Network Load Balancer (NLB)**

  NLB operates at **Layer 4 (TCP/UDP/TLS)**, provides **ultra-low latency**, and is designed to handle **millions of requests per second**, making it ideal for high-performance gaming applications.

</details>


An **Auto Scaling Group (ASG)** is **not launching new instances** despite **high CPU utilization**.  
What could be the issue?  
*(Choose TWO)*

- A. Security group is blocking traffic  
- B. Maximum capacity reached  
- C. Launch template is invalid  
- D. Insufficient IAM permissions for Auto Scaling  
- E. ELB health checks are failing  

<details>
  <summary><strong>Answer</strong></summary>

  **B. Maximum capacity reached**  
  **D. Insufficient IAM permissions for Auto Scaling**

  **Explanation:**

  - **B. Maximum capacity reached** – If the ASG has already reached its configured **Max Size**, it cannot launch additional instances, even if scaling conditions are met.
  - **D. Insufficient IAM permissions** – Auto Scaling requires proper IAM permissions to launch EC2 instances. Missing or incorrect permissions will prevent scaling actions.

   **Why the others are incorrect:**
  - **A. Security group is blocking traffic** – Does not prevent instance launch; it only affects network access.
  - **C. Launch template is invalid** – This *could* block launches, but it would typically cause explicit launch errors, not silent scaling failure.
  - **E. ELB health checks are failing** – This may cause instances to be replaced, but does not prevent new instances from being launched due to scaling.

</details>

An application experiences **variable traffic with sudden spikes**.  
What is the **MOST cost-effective compute solution**?

- A. Reserved Instances  
- B. On-Demand Instances with Auto Scaling  
- C. Dedicated Hosts  
- D. Spot Instances  

<details>
  <summary><strong>Answer</strong></summary>

  **B. On-Demand Instances with Auto Scaling**

  **Explanation:**

  - **On-Demand Instances with Auto Scaling** allow the application to scale **up and down automatically** based on demand.
  - You **only pay for instances while they are running**, making this option cost-effective for **unpredictable or spiky workloads**.

  **Why the others are not ideal:**
  - **A. Reserved Instances** – Best for steady, predictable workloads, not variable traffic.
  - **C. Dedicated Hosts** – High cost, used mainly for compliance or licensing requirements.
  - **D. Spot Instances** – Very cheap, but can be interrupted, making them risky as the *primary* solution for sudden spikes.

  **Exam tip:**  
  Variable or unpredictable traffic → **On-Demand + Auto Scaling**

</details>