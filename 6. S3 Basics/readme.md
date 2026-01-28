## AWS Certified Solutions Architect – Associate

O Amazon S3 é um dos **serviços mais cobrados da prova**.  
Esta aula aborda **S3 do básico ao avançado**, com foco em **arquitetura, custo, segurança e automação**.

---

## Objetivos da Aula

Ao final desta aula, você será capaz de:

- Entender profundamente o **Amazon S3**
- Aplicar **Bucket Policies**
- Usar **Versioning** corretamente
- Explicar **S3 Replication**
- Escolher a **Storage Class correta**
- Entender o **S3 Express One Zone**
- Configurar **Lifecycle Rules**
- Entender **Requester Pays**
- Usar **S3 Event Notifications**
- Resolver questões de prova com segurança

---

## Estrutura da Aula

- Introdução ao S3
- Segurança e Bucket Policies
- Versioning e Replication
- Storage Classes
- S3 Express One Zone
- Lifecycle Rules
- Requester Pays
- S3 Event Notifications
- Mentalidade de prova e revisão

---

## Amazon S3 – Conceito Fundamental

O **Amazon S3 (Simple Storage Service)** é um serviço de **armazenamento de objetos**, altamente escalável e durável.

### Características principais:
- Armazena **objetos** (não blocos, não arquivos tradicionais)
- Cada objeto = **dados + metadata + key**
- Escala praticamente de forma ilimitada
- **Durabilidade de 99.999999999% (11 9s)**

 **Na prova**
> S3 = armazenamento durável, escalável e global (regional, mas acessível globalmente)

---

## 2️⃣ Buckets e Organização

### Buckets
- São **globais em nome**
- Criados em **uma região específica**
- Contêm objetos organizados por **prefixos**

 Importante:
> Não existem “pastas reais” no S3, apenas **prefixos no nome do objeto**

---

## Bucket Policy (Controle de Acesso)

### O que é uma Bucket Policy?
É uma **política baseada em recurso**, escrita em JSON, que controla **quem pode acessar o bucket ou objetos**.

### O que pode controlar:
- Quem pode **ler, escrever ou deletar**
- Acesso por:
  - Conta AWS
  - IAM Role
  - IP
  - VPC Endpoint
  - HTTPS obrigatório

 **Na prova**
> Acesso público controlado → **Bucket Policy**  
> Permissões para usuários → **IAM Policy**

---

## S3 Versioning

### O que é Versioning?
Permite manter **múltiplas versões** do mesmo objeto.

### Benefícios:
- Proteção contra deleção acidental
- Recuperação de versões antigas
- Base para:
  - Replication
  - MFA Delete

 Regras importantes:
- Uma vez ativado, **não pode ser desativado**
- Apenas suspenso
- Objetos deletados geram **delete markers**

 **Na prova**
> Proteção contra exclusão → **Versioning**

---

## S3 Replication

### O que é Replication?
Cópia automática e assíncrona de objetos entre buckets.

### Tipos:
- **CRR (Cross-Region Replication)**
- **SRR (Same-Region Replication)**

### Requisitos:
- Versioning habilitado nos dois buckets
- Permissões IAM adequadas

### Casos de uso:
- Disaster Recovery
- Compliance
- Redução de latência
- Replicação entre contas

 **Na prova**
> DR entre regiões → **CRR**

---

## S3 Storage Classes

Escolher a storage class correta é **fundamental para custo e prova**.

### S3 Standard
- Alta disponibilidade
- Acesso frequente
- Websites, apps, conteúdo ativo

---

### S3 Intelligent-Tiering
- Move objetos automaticamente entre tiers
- Ideal quando **padrão de acesso é desconhecido**

 Custo extra de monitoramento

---

### S3 Standard-IA
- Acesso infrequente
- Alta durabilidade
- Custo menor, **custo de acesso**

---

### S3 One Zone-IA
- Dados em **uma única AZ**
- Menor custo
- Não indicado para dados críticos

---

### S3 Glacier Instant Retrieval
- Dados raramente acessados
- Acesso em milissegundos

---

### S3 Glacier Flexible Retrieval
- Restore em minutos ou horas
- Backups e DR

---

### S3 Glacier Deep Archive
- Restore em horas
- **Menor custo**
- Arquivamento de longo prazo

 **Na prova**
> Arquivo longo prazo e barato → **Glacier Deep Archive**

---

## S3 Express One Zone

### O que é?
Uma storage class **de altíssima performance**, focada em **latência de milissegundos**.

### Características:
- Uma única AZ
- Performance extrema
- Casos específicos

### Casos de uso:
- Machine Learning
- Analytics
- Data-intensive workloads

 **Na prova**
> Performance extrema em S3 → **Express One Zone**

---

## S3 Lifecycle Rules

### O que são Lifecycle Rules?
Regras automáticas para:
- Transição de objetos entre storage classes
- Exclusão automática de objetos

### Casos comuns:
- Standard → IA → Glacier
- Exclusão após X dias
- Gerenciamento de versões antigas

 **Na prova**
> Otimização automática de custo → **Lifecycle**

---

## S3 Requester Pays

### O que é?
Modelo onde **quem faz o download paga pelo custo de transferência**.

### Casos de uso:
- Dados públicos
- Compartilhamento de grandes datasets
- Open data

 **Na prova**
> Dono do bucket não quer pagar transferência → **Requester Pays**

---

## S3 Event Notifications

### O que são?
Permitem reagir a eventos no S3, como:
- Upload de objeto
- Delete
- Restore

### Destinos:
- AWS Lambda
- Amazon SQS
- Amazon SNS
- EventBridge

### Casos de uso:
- Processamento automático
- Gatilhos de workflow
- Data pipelines

📌 **Na prova**
> Processar arquivo após upload → **S3 Event Notification + Lambda**

---

## Como a AWS cobra S3 na prova

| Cenário | Serviço |
|------|--------|
| Armazenar objetos | S3 |
| Controle de acesso público | Bucket Policy |
| Recuperar versões | Versioning |
| DR entre regiões | CRR |
| Otimizar custo | Lifecycle |
| Dados públicos grandes | Requester Pays |
| Processamento automático | Event Notifications |
| Performance extrema | Express One Zone |

---

## Conclusão

Se você dominar:
- Storage Classes
- Versioning
- Replication
- Lifecycle
- Segurança com Bucket Policy

Você resolve **a maioria das questões de S3 da prova**.

---

Material criado para estudo da  
**AWS Certified Solutions Architect – Associate**
