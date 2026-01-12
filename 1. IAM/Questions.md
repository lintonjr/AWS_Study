# Perguntas (Não estão no estilo da prova)

> Regras: 4 alternativas, apenas 1 correta.

## 1) Ordem de avaliação (Allow/Deny)
Um usuário tem uma policy **Allow** para `s3:*` em `*`. O bucket possui uma bucket policy com **Deny** para `s3:DeleteObject` para todos. O que acontece quando o usuário tenta deletar um objeto?  
A. Permite, porque o usuário tem Allow amplo  
B. Nega, porque Deny explícito sempre vence  
C. Permite, porque bucket policy não afeta IAM user  
D. Depende da região do bucket  

## 2) Acesso EC2 → S3 sem chaves
Você precisa permitir que uma instância EC2 leia objetos de um bucket S3 **sem armazenar access keys** no servidor. Qual é a melhor solução?  
A. Criar um IAM User e colocar as keys no `.env` da instância  
B. Criar um IAM Group com permissão e adicionar a instância ao group  
C. Criar uma IAM Role com permissão S3 e associar via Instance Profile  
D. Criar uma bucket policy Allow para o IP público da instância  

## 3) Root account
Qual prática é **mais recomendada** para proteger a conta root?  
A. Usar root diariamente e rotacionar senha semanalmente  
B. Habilitar MFA no root e usar root apenas quando necessário  
C. Criar access keys no root e usar no CI/CD  
D. Colocar root em um IAM Group com permissões restritas  

## 4) IAM Group
Sobre IAM Groups, qual afirmação é correta?  
A. Groups podem ser assumidos via STS como se fossem Roles  
B. Groups podem conter outros Groups (aninhamento)  
C. Você anexa policies a Groups para gerenciar permissões de usuários  
D. Groups podem ter credenciais (password/access keys) próprias  

## 5) Inline policy
Quando uma **inline policy** pode ser justificável?  
A. Quando você quer reutilizar a mesma policy em várias roles e users  
B. Quando a permissão deve existir somente ligada a uma identidade específica, sem reutilização  
C. Quando você quer que a AWS atualize a policy automaticamente  
D. Quando você precisa aplicar a policy em recursos (resource-based policy)  

## 6) CLI/SDK e melhores práticas
Qual afirmação está mais alinhada às best practices ao usar AWS SDK em produção dentro da AWS?  
A. Usar access key do root em variáveis de ambiente  
B. Usar access keys de um IAM user “service-account” no código  
C. Usar IAM Role para o serviço (credenciais temporárias via STS)  
D. Desativar CloudTrail para reduzir custo  

## 7) Trust policy vs permission policy
Uma IAM Role possui duas partes principais. Qual é a descrição correta?  
A. Permission policy define *quem* assume; trust policy define *o que* ela faz  
B. Trust policy define *quem* pode assumir; permission policy define *o que* ela pode fazer  
C. Ambas definem apenas recursos; ações ficam no Security Group  
D. Trust policy é usada somente para S3  

## 8) S3 ListBucket vs GetObject
Você quer permitir que um usuário liste o bucket e leia objetos. Qual combinação correta?  
A. `s3:ListBucket` no ARN `arn:aws:s3:::bucket/*` e `s3:GetObject` no ARN `arn:aws:s3:::bucket`  
B. `s3:ListBucket` no ARN `arn:aws:s3:::bucket` e `s3:GetObject` no ARN `arn:aws:s3:::bucket/*`  
C. Ambas ações sempre usam `arn:aws:s3:::bucket/*`  
D. Ambas ações sempre usam `arn:aws:s3:::bucket`  

## 9) Policy Simulator
Você está recebendo `AccessDenied` ao chamar uma API. Qual ferramenta IAM é mais indicada para simular e entender se a ação é permitida por policies?  
A. IAM Credential Report  
B. IAM Access Advisor  
C. IAM Policy Simulator  
D. AWS Budgets  

## 10) Credential Report
Qual é o principal uso do **IAM Credential Report**?  
A. Verificar custos de usuários por serviço  
B. Auditar status de credenciais (MFA, keys ativas, uso, rotação)  
C. Criar policies automaticamente por comportamento  
D. Substituir o CloudTrail para auditoria de API  

## 11) Access Advisor
Qual problema o **IAM Access Advisor** ajuda a resolver?  
A. Mostrar quais serviços uma entidade usou recentemente para reduzir permissões  
B. Detectar ataques DDoS automaticamente  
C. Configurar MFA em lote  
D. Gerar chaves KMS para criptografia  

## 12) Cross-account sem compartilhar chaves
Você precisa permitir que a Conta B acesse recursos na Conta A, sem criar usuários com keys compartilhadas. Qual abordagem correta?  
A. Criar IAM user na Conta A e enviar access keys para a Conta B  
B. Criar Role na Conta A com trust policy permitindo a Conta B assumir (STS AssumeRole)  
C. Colocar o CIDR da Conta B em uma IAM policy  
D. Habilitar acesso público e restringir por User-Agent  

## 13) MFA como condição
Você quer permitir `iam:ChangePassword` somente se o usuário estiver autenticado com MFA. O que usar?  
A. Apenas Password Policy  
B. Condition em policy exigindo MFA (ex.: `aws:MultiFactorAuthPresent`)  
C. Security Group no IAM User  
D. Bucket policy no IAM  

## 14) Resource-based policy
Qual exemplo é de **resource-based policy**?  
A. Policy anexada a IAM User  
B. Policy anexada a IAM Group  
C. Policy anexada a IAM Role  
D. Bucket policy do S3  

## 15) Policies gerenciadas pela AWS
Qual é uma característica de **AWS Managed Policies**?  
A. Você pode editá-las livremente  
B. Elas podem ser atualizadas pela AWS ao longo do tempo  
C. Elas só podem ser anexadas a recursos, não identidades  
D. Elas são sempre mais restritivas que as Customer Managed  

## 16) “Implicit Deny”
Se nenhuma policy permitir uma ação e não houver Deny explícito, o resultado é:  
A. Allow implícito  
B. Deny implícito (implicit deny)  
C. Allow se o usuário estiver em um Group  
D. Depende do horário (time-based access)  

## 17) Rotação e risco de access keys
Você suspeita que uma access key foi exposta. Qual é a resposta mais apropriada?  
A. Criar mais uma access key e manter as duas ativas  
B. Desativar/deletar a access key comprometida e rotacionar imediatamente  
C. Apenas mudar a senha do Console do usuário  
D. Desativar MFA para evitar bloqueios  

## 18) Role para Lambda
Para permitir que uma função Lambda escreva logs no CloudWatch Logs, o que é necessário?  
A. Um IAM User com access keys no código da Lambda  
B. Uma bucket policy no CloudWatch  
C. Uma execution role (IAM Role) associada à Lambda com permissões de logs  
D. Um Security Group com saída para `logs.amazonaws.com`  

## 19) Boas práticas: anexar policy
Qual prática é mais recomendada para gerenciamento de permissões de pessoas?  
A. Anexar policies diretamente a cada IAM User  
B. Usar Groups e anexar policies aos Groups  
C. Usar apenas inline policies  
D. Usar somente root para evitar complexidade  

## 20) Princípio do menor privilégio
Qual cenário melhor representa **least privilege**?  
A. Conceder `AdministratorAccess` e “depois ajustar” se alguém reclamar  
B. Conceder apenas ações e recursos necessários (com conditions quando fizer sentido)  
C. Conceder `*:*` mas restringir por região na aplicação  
D. Conceder permissões amplas e confiar no “bom uso”  

---

## Gabarito e explicações

1) **B** — Deny explícito sempre vence Allow.  
2) **C** — Role + Instance Profile fornece credenciais temporárias sem keys no host.  
3) **B** — MFA no root e uso mínimo do root.  
4) **C** — Group agrupa users e recebe policies.  
5) **B** — Inline é útil quando deve ficar presa a uma identidade específica.  
6) **C** — Use Role e credenciais temporárias (STS) para workloads AWS.  
7) **B** — Trust = quem assume; Permission = o que pode fazer.  
8) **B** — ListBucket no bucket ARN; GetObject nos objetos (`/*`).  
9) **C** — Policy Simulator simula permissões e ajuda em troubleshooting.  
10) **B** — Credential Report audita credenciais (MFA, keys, rotação etc.).  
11) **A** — Access Advisor mostra serviços acessados para reduzir permissões.  
12) **B** — Cross-account correto: AssumeRole com trust policy.  
13) **B** — Condition exigindo MFA (ex.: `aws:MultiFactorAuthPresent`).  
14) **D** — Bucket policy é resource-based policy.  
15) **B** — AWS Managed pode ser atualizada pela AWS.  
16) **B** — Se não há Allow, nega por padrão (implicit deny).  
17) **B** — Revogar/rotacionar imediatamente a key exposta.  
18) **C** — Lambda precisa de execution role com permissões de logs.  
19) **B** — Gerencie pessoas por Groups e policies gerenciadas.  
20) **B** — Menor privilégio: mínimo necessário + conditions quando útil.

---