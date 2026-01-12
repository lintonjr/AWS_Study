# AWS SAA — IAM (Aula)

Material de estudo focado na certificação **AWS Certified Solutions Architect – Associate (SAA)** sobre **IAM (Identity and Access Management)**

---

## Sumário
- [Objetivos](#objetivos)
- [Pré-requisitos](#pré-requisitos)
- [Aula — IAM (Visão Geral)](#aula--iam-visão-geral)
  - [1) O que é IAM](#1-o-que-é-iam)
  - [2) Users, Groups e Policies](#2-users-groups-e-policies)
  - [3) MFA e Password Policy](#3-mfa-e-password-policy)
  - [4) Access Keys, CLI e SDK](#4-access-keys-cli-e-sdk)
  - [5) IAM Roles para Services e Cross-account](#5-iam-roles-para-services-e-cross-account)
  - [6) IAM Security Tools](#6-iam-security-tools)
  - [7) IAM Best Practices](#7-iam-best-practices)
  - [8) Perguntas estilo certificação (treino rápido)](#8-perguntas-estilo-certificação-treino-rápido)
  - [9) Mini-lab (30–40 min)](#9-mini-lab-3040-min)
  - [10) Resumo final (revisão)](#10-resumo-final-revisão)
- [Simulado — IAM (20 questões)](#simulado--iam-20-questões)
  - [Gabarito e explicações](#gabarito-e-explicações)

---

## Objetivos
Ao final deste material você deve conseguir:
- Explicar **quem** (Identity) acessa **o quê** (Permission) e **como** (AuthN/AuthZ) na AWS.
- Configurar **Users, Groups, Policies**, **MFA**, **Password Policy**, **Access Keys** e **Roles**.
- Usar ferramentas de auditoria do IAM e aplicar **best practices** cobradas em prova.

---

## Pré-requisitos
- Noções básicas de AWS (Console e serviços como S3 e EC2).
- Opcional para o mini-lab:
  - AWS CLI instalada
  - Credenciais configuradas (preferencialmente via IAM user de laboratório ou perfil de estudo)

---

# Aula — IAM (Visão Geral)

## 1) O que é IAM
**IAM (Identity and Access Management)** controla:
- **Autenticação (AuthN)**: provar quem você é (senha, MFA, chaves).
- **Autorização (AuthZ)**: definir o que você pode fazer (policies e permissões).

**Conceitos-chave**
- IAM é **global** (não é por região).
- Controle de acesso ocorre via:
  - **Identity-based policies** (anexadas a user/group/role)
  - **Resource-based policies** (anexadas ao recurso, ex.: S3 bucket policy, KMS key policy)
- Avaliação de permissão:
  - **Explicit Deny > Allow > Implicit Deny**

---

## 2) Users, Groups e Policies

### 2.1 IAM User
Representa uma identidade (pessoa ou aplicação *legada*).
- Pode ter **Console password**
- Pode ter **Access keys** (acesso programático)
- Pode ter policies anexadas diretamente (evitar como padrão)

> Dica de prova: a recomendação moderna é **federar** (IAM Identity Center/SSO) e usar **roles** para workloads.

### 2.2 IAM Group
Container de usuários para facilitar gerenciamento.
- Você anexa **policies ao Group** e adiciona users ao group.
- Group **não** pode conter outro group e **não** pode ser assumido como role.

### 2.3 IAM Policies
Documento JSON que define permissões.

**Estrutura típica**
- `Version`
- `Statement`:
  - `Effect`: Allow/Deny
  - `Action`: `s3:GetObject`
  - `Resource`: ARN do recurso
  - `Condition`: filtros (MFA, IP, tags, endpoint, etc.)

Exemplo didático — permitir ler objetos em um prefixo do S3:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ReadOnlyInPrefix",
      "Effect": "Allow",
      "Action": ["s3:GetObject"],
      "Resource": ["arn:aws:s3:::meu-bucket/relatorios/*"]
    }
  ]
}
```

**Tipos de policy**
- **AWS Managed**: prontas da AWS (rápidas, podem ser amplas).
- **Customer Managed**: você gerencia (melhor controle e reutilização).
- **Inline**: “presa” a uma identidade (evitar, salvo casos específicos).

**Pegadinhas comuns**
- `Resource: "*"` + ações sensíveis = risco alto.
- `s3:ListBucket` usa ARN do **bucket** (sem `/*`).
- `s3:GetObject` usa ARN do **objeto** (`/*`).
- Um `Deny` explícito sempre vence.

---

## 3) MFA e Password Policy

### 3.1 MFA
Recomendado para todos com acesso ao Console, principalmente para **root**.
- Virtual MFA (Authenticator)
- Hardware MFA

**Cai muito:** habilitar MFA no **root** e usar root apenas quando necessário.

### 3.2 Password Policy
Define regras para senha do Console:
- tamanho mínimo
- complexidade
- expiração
- impedir reutilização
- reset por admin

---

## 4) Access Keys, CLI e SDK

### 4.1 Access Keys
Credenciais programáticas:
- `AccessKeyId`
- `SecretAccessKey`

**Boas práticas**
- Nunca commitar keys em repo.
- Rotacionar periodicamente.
- Preferir **roles** ao invés de keys fixas em servidores.

### 4.2 AWS CLI
Configuração típica:
```bash
aws configure
# AWS Access Key ID:
# AWS Secret Access Key:
# Default region name:
# Default output format:
```

Verificar identidade atual:
```bash
aws sts get-caller-identity
```

### 4.3 AWS SDK
- Em EC2/Lambda/ECS: preferir **IAM Role** e **credenciais temporárias** via STS.
- Em dev local: usar perfis (`~/.aws/credentials`) é aceitável, mas em produção evite keys fixas.

---

## 5) IAM Roles para Services e Cross-account

### 5.1 O que é Role?
Role é uma identidade sem credenciais permanentes.
- Um principal (serviço, usuário, outra conta) **assume** a role e recebe credenciais temporárias via **STS**.

Exemplos:
- EC2 Role para acessar S3
- Lambda Execution Role para logs e acesso a DynamoDB
- ECS Task Role para acessar SQS, S3 etc.

### 5.2 Trust Policy vs Permission Policy
Uma Role tem:
1. **Trust policy**: *quem* pode assumir (quem)
2. **Permission policy**: *o que* pode fazer (o quê)

### 5.3 Cross-account access
Forma correta de permitir acesso entre contas sem compartilhar chaves:
- **AssumeRole + trust policy** permitindo outra conta (ou principal) assumir.

---

## 6) IAM Security Tools

### 6.1 IAM Credential Report
Relatório (CSV) com status de credenciais:
- MFA habilitado?
- Password last used
- Access keys: active/inactive, last used, rotação

### 6.2 IAM Access Advisor
Mostra quais serviços uma entidade realmente usou (último acesso).
- Ajuda a reduzir permissões e aplicar least privilege.

### 6.3 IAM Policy Simulator
Simula se uma ação seria permitida/negada para um user/role.
- Excelente para troubleshooting de `AccessDenied`.

> Extra importante: **CloudTrail** (auditoria de chamadas de API) e **Config** (compliance) são frequentemente usados junto ao IAM.

---

## 7) IAM Best Practices
1. **MFA no root** e root guardado com cuidado; uso mínimo.
2. **Least privilege** (mínimo necessário).
3. **Roles para workloads** (EC2/Lambda/ECS) — evite access keys.
4. **Groups** para pessoas + policies gerenciadas (Customer Managed) quando fizer sentido.
5. **Rotacione credenciais** e remova acesso não usado.
6. Use **Conditions** (MFA, IP, endpoint, tags) para reduzir risco.
7. Separe ambientes (dev/stage/prod) e reduza blast radius.
8. Audite com **Credential Report**, **Access Advisor**, **CloudTrail**.

---

## 8) Treino rápido
1. EC2 precisa ler S3 sem chaves → **IAM Role (Instance Profile)**  
2. Allow no user, Deny no bucket policy → **Deny vence**  
3. Reduzir permissões com segurança → **Access Advisor + Simulator**  
4. Acesso temporário a fornecedor → **STS / AssumeRole**  

---

## 9) Mini-lab (30–40 min)

### Parte A: identidade atual
```bash
aws sts get-caller-identity
```

### Parte B: policy gerenciada (S3 read-only em prefixo)
1. Crie uma **Customer Managed Policy** com o JSON do exemplo.
2. Anexe a um **Group** chamado `S3ReportsReaders`.
3. Adicione um usuário de teste ao group.

### Parte C: simular permissão
- Use **Policy Simulator**:
  - `s3:GetObject` no prefixo permitido → Allow
  - em outro prefixo → Implicit deny

### Parte D: habilitar MFA e checar relatório
- Habilite MFA no user.
- Gere **Credential Report** e valide os campos.

### Parte E: Role para Lambda (conceitual)
- Crie uma Role para **Lambda** com permissão de logs (ex.: policy gerenciada de logs).
- Entenda trust policy do serviço `lambda.amazonaws.com`.

---

## 10) Resumo final (revisão)
- **Users**: pessoas/aplicações; evite para workloads.
- **Groups**: organizam users; policies ficam aqui.
- **Policies**: JSON; Deny ganha; Condition é crucial.
- **MFA/Password Policy**: protegem Console; root com MFA sempre.
- **Access Keys**: programático; prefira roles.
- **Roles**: assumíveis via STS; ideal para serviços e cross-account.
- **Security Tools**: Credential Report, Access Advisor, Policy Simulator.
- **Best practices**: least privilege, rotação, auditoria, roles e federação.

---


