## AWS Certified Solutions Architect – Associate

---

## 1. O que é AWS Lambda

AWS Lambda é um serviço **serverless** que permite executar código sem provisionar ou gerenciar servidores.

Você paga apenas por:
- Número de invocações
- Tempo de execução (em milissegundos)

É ideal para:
- Arquiteturas event-driven
- APIs serverless
- Processamento assíncrono
- Workloads intermitentes

---

## 2. Modelo de Execução do Lambda

### Tipos de Invocação

### Synchronous (Request / Response)
- API Gateway
- Application Load Balancer
- SDK direto

Fluxo:
Cliente → API Gateway / ALB → Lambda → Resposta

---

### Asynchronous
- Amazon S3
- Amazon SNS
- Amazon EventBridge

Fluxo:
Evento → Lambda → retry automático

---

### Poll-based (Event Source Mapping)
- Amazon SQS
- DynamoDB Streams
- Kinesis

Lambda faz polling automaticamente da origem.

---

## 3. Cold Start vs Warm Start

### Cold Start
Ocorre quando:
- Primeira execução
- Função ficou inativa
- Escala cria novo ambiente

Impacto:
- Aumento de latência
- Mais perceptível em VPC

---

### Warm Start
- Ambiente já inicializado
- Execução mais rápida

---

### Como reduzir Cold Start
- Evitar inicializações pesadas
- Usar runtimes rápidos
- Provisioned Concurrency
- Evitar VPC quando possível

---

## 4. Lambda e VPC

- Lambda não precisa estar em VPC por padrão
- VPC aumenta cold start
- Use VPC apenas para acessar recursos privados

### Acesso à Internet
Lambda em VPC precisa de:
- Subnet privada
- NAT Gateway
- Rota correta

---

## 5. Limites Importantes

| Item | Limite |
|---|---|
| Timeout | 15 minutos |
| Memória | 128 MB – 10 GB |
| /tmp | 512 MB (até 10 GB) |
| Payload sync | 6 MB |
| Payload async | 256 KB |

---

## 6. Lambda Concurrency

### Unreserved Concurrency
- Limite global da conta
- Compartilhado entre funções

---

### Reserved Concurrency
- Reserva capacidade para uma função
- Evita impacto entre Lambdas

---

### Provisioned Concurrency
- Elimina cold start
- Custo adicional
- Ideal para APIs críticas

---

## 7. Lambda Destinations

Permite enviar resultados automaticamente:

- On Success: SNS, SQS, EventBridge, Lambda
- On Failure: Auditoria e retry

---

## 8. Lambda + API Gateway vs ALB

### API Gateway
- APIs REST
- Auth e throttling
- Mais caro

### ALB
- HTTP simples
- Menor custo
- Alta performance

---

## 9. Lambda Layers

Usado para:
- Compartilhar bibliotecas
- Reduzir tamanho do pacote
- Padronizar dependências

---

## 10. Segurança

### IAM Execution Role
Define permissões de acesso da Lambda.

### Resource-based Policy
Define quem pode invocar a Lambda.

---

## 11. Monitoramento

- CloudWatch Logs
- CloudWatch Metrics
- AWS X-Ray

---

## 12. Quando NÃO usar Lambda

- Execuções longas (>15 min)
- Aplicações stateful
- Carga constante

Alternativas:
- ECS Fargate
- EC2
- Step Functions

---

## 13. Arquiteturas Comuns

- S3 → Lambda → S3
- API Gateway → Lambda → DynamoDB
- EventBridge → Lambda → SNS

---

## 14. Resumo para Prova

- Lambda é event-driven
- Cold start é relevante
- Concurrency é tema recorrente
- Provisioned Concurrency elimina cold start

---

Material de estudo – AWS Certified Solutions Architect – Associate
