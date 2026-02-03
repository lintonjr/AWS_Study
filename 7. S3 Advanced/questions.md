## Questão 1 – Lifecycle Rules

A company wants to **automatically move objects** from S3 Standard to a cheaper storage class after 30 days and **delete them after 1 year**.  
Which S3 feature should be used?

A. S3 Replication  
B. S3 Batch Operations  
C. S3 Lifecycle Rules  
D. S3 Storage Lens  

<details>
  <summary><strong> Answer</strong></summary>

  **C. S3 Lifecycle Rules**

  Lifecycle Rules allow automatic **transition between storage classes** and **object expiration** based on time.

</details>

---

## Questão 2 – S3 Batch Operations

You need to **add a tag** to **millions of existing objects** in an S3 bucket.  
What is the MOST efficient solution?

A. Write a custom script using AWS SDK  
B. Use S3 Event Notifications  
C. Use S3 Batch Operations  
D. Enable S3 Storage Lens  

<details>
  <summary><strong> Answer</strong></summary>

  **C. S3 Batch Operations**

  Batch Operations are designed for **large-scale operations** across millions or billions of objects.

</details>

---

## Questão 3 – S3 Storage Lens

A solutions architect wants **visibility into S3 usage and cost trends** across multiple accounts.  
Which service should be used?

A. CloudWatch  
B. S3 Inventory  
C. S3 Storage Lens  
D. AWS Cost Explorer  

<details>
  <summary><strong> Answer</strong></summary>

  **C. S3 Storage Lens**

  Storage Lens provides **account-wide and organization-wide analytics** for S3 usage and cost optimization.

</details>

---

## Questão 4 – S3 Encryption

A company requires **encryption at rest with full auditability** and **fine-grained access control**.  
Which S3 encryption option should be used?

A. SSE-S3  
B. SSE-KMS  
C. SSE-C  
D. Client-side encryption only  

<details>
  <summary><strong> Answer</strong></summary>

  **B. SSE-KMS**

  SSE-KMS provides **audit logs**, **key rotation**, and **access control** via AWS KMS.

</details>

---

## Questão 5 – S3 CORS

A web application hosted on a different domain cannot access objects in an S3 bucket due to browser errors.  
What should be configured?

A. Bucket Policy  
B. IAM Role  
C. S3 CORS configuration  
D. VPC Endpoint  

<details>
  <summary><strong> Answer</strong></summary>

  **C. S3 CORS configuration**

  CORS allows **cross-origin browser access** to S3 objects.

</details>

---

## Questão 6 – S3 Pre-signed URL

You want to allow users to **upload files directly to S3** without giving them AWS credentials.  
What is the BEST solution?

A. Make the bucket public  
B. Use IAM users  
C. Use S3 Pre-signed URLs  
D. Use CloudFront signed URLs  

<details>
  <summary><strong> Answer</strong></summary>

  **C. S3 Pre-signed URLs**

  Pre-signed URLs provide **temporary, secure access** without exposing credentials.

</details>

---

## Questão 7 – S3 Object Lock

A company must store records that **cannot be modified or deleted for 7 years**, even by administrators.  
Which S3 feature should be used?

A. Versioning  
B. Bucket Policy  
C. Object Lock in Compliance Mode  
D. Lifecycle Rules  

<details>
  <summary><strong> Answer</strong></summary>

  **C. Object Lock in Compliance Mode**

  Compliance Mode enforces **WORM (Write Once, Read Many)** and prevents deletion by any user.

</details>

---

## Questão 8 – S3 Object Lambda

A company wants to **mask sensitive fields** in JSON files stored in S3 **at request time**, without modifying the original data.  
Which solution should be used?

A. S3 Batch Operations  
B. S3 Object Lambda  
C. AWS Glue  
D. Lambda triggered by S3 Event  

<details>
  <summary><strong> Answer</strong></summary>

  **B. S3 Object Lambda**

  Object Lambda allows **real-time transformation** of objects when they are accessed.

</details>

---

## Questão 9 – Encryption in Transit

A company wants to **enforce encryption in transit** for all S3 access.  
How can this be achieved?

A. Enable SSE-KMS  
B. Enable Versioning  
C. Configure a Bucket Policy requiring HTTPS  
D. Use S3 Storage Lens  

<details>
  <summary><strong> Answer</strong></summary>

  **C. Configure a Bucket Policy requiring HTTPS**

  Bucket Policies can enforce **TLS (HTTPS)** for all requests.

</details>

---

## Questão 10 – Cost Optimization

An S3 bucket stores data that is **rarely accessed**, but must be retrieved **within minutes** when needed.  
Which storage class is MOST appropriate?

A. S3 Standard  
B. S3 Glacier Deep Archive  
C. S3 Glacier Flexible Retrieval  
D. S3 One Zone-IA  

<details>
  <summary><strong> Answer</strong></summary>

  **C. S3 Glacier Flexible Retrieval**

  It offers **low storage cost** with **restore times in minutes**, suitable for infrequent access.

</details>

---

## Final Exam Tips

- Otimização automática de custo → **Lifecycle Rules**
- Operações em massa → **Batch Operations**
- Visibilidade e governança → **Storage Lens**
- Criptografia auditável → **SSE-KMS**
- Acesso temporário → **Pre-signed URLs**
- Dados imutáveis → **Object Lock**
- Transformação dinâmica → **Object Lambda**

---

