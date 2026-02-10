## AWS Certified Solutions Architect – Associate

---

## Objetivo da Aula

Ao final desta aula, você será capaz de:
- Escolher o **banco correto para cada cenário**
- Entender **alta disponibilidade, escalabilidade e performance**
- Resolver questões de prova envolvendo **RDS, Aurora, DynamoDB e ElastiCache**
- Diferenciar **bancos relacionais, NoSQL, cache, grafos e séries temporais**


---

## Amazon RDS (Relational Database Service)

O **Amazon RDS** é um serviço gerenciado de bancos de dados **relacionais**.

### Engines suportadas
- MySQL
- PostgreSQL
- MariaDB
- Oracle
- SQL Server
- Amazon Aurora (caso especial)

### Características
- Gerenciamento de patches
- Backups automáticos
- Snapshots manuais
- Multi-AZ (alta disponibilidade)

 **Na prova**  
> Se a questão citar SQL tradicional → pense em **RDS**

---

## RDS Multi-AZ (Alta Disponibilidade)

O **Multi-AZ** cria uma réplica síncrona em outra AZ.

### Importante
- Usado para **failover**
- NÃO melhora performance de leitura
- Endpoint permanece o mesmo

 **Dica de prova**  
> Alta disponibilidade ≠ Read Replica

---

## RDS Read Replicas (Escalabilidade de Leitura)

As **Read Replicas** são réplicas **assíncronas**.

### Usadas para
- Escalar leitura
- Relatórios
- Workloads read-heavy

### Características
- Endpoint separado
- Pode existir em outra região
- Não serve para failover automático

 **Comparação-chave (PROVA)**

| Feature | Multi-AZ | Read Replica |
|------|---------|-------------|
| HA | V | X |
| Read Scaling | X | V |
| Sync | Síncrono | Assíncrono |

---

## RDS Proxy

O **RDS Proxy** gerencia **pool de conexões** para bancos RDS e Aurora.

### Quando usar
- Lambda + RDS
- Muitas conexões simultâneas
- Reduz overhead de conexão

### Benefícios
- Melhora performance
- Aumenta resiliência
- Reduz falhas por excesso de conexões

 **Na prova**  
> Lambda abrindo muitas conexões → **RDS Proxy**

---

## Amazon Aurora

O **Amazon Aurora** é um banco relacional **cloud-native** compatível com:
- MySQL
- PostgreSQL

### Diferenciais
- Storage distribuído em **6 cópias / 3 AZs**
- Failover rápido
- Muito mais performance que RDS tradicional

### Aurora Replicas
- Até **15 réplicas**
- Failover automático
- Leitura altamente escalável

 **Na prova**
> Precisa de alta performance + SQL → **Aurora**

---

## Amazon ElastiCache

Serviço de **cache em memória**.

### Engines
- Redis
- Memcached

### Usos comuns
- Cache de sessão
- Leaderboards
- Dados frequentemente acessados
- Reduz carga no banco principal

 **ElastiCache ≠ banco principal**  
É um **acelerador**, não storage definitivo.

---

## Amazon DynamoDB

Banco **NoSQL key-value / document** totalmente gerenciado.

### Características
- Serverless
- Escala automaticamente
- Latência de milissegundos
- Alta disponibilidade por padrão

### Casos de uso
- Mobile apps
- IoT
- Gaming
- Catálogos

### Recursos importantes
- On-Demand vs Provisioned
- Global Tables (multi-região)
- DAX (cache em memória)

 **Na prova**
> Alta escala + baixa latência + serverless → **DynamoDB**

---

## Amazon Neptune

Banco de dados de **grafos**.

### Usado para
- Redes sociais
- Recomendação
- Detecção de fraude
- Relacionamentos complexos

### Modelos
- Property Graph
- RDF (SPARQL)

 **Na prova**
> Relações complexas → **Neptune**

---

## Amazon Timestream

Banco de dados para **séries temporais**.

### Usado para
- Métricas
- IoT
- Monitoramento
- Eventos com timestamp

### Características
- Serverless
- Armazenamento automático por camadas
- Queries rápidas por tempo

 **Na prova**
> Dados baseados em tempo → **Timestream**

---

## Comparação Geral (PROVA)

| Serviço | Tipo | Caso de Uso |
|------|----|-----------|
| RDS | Relacional | Apps tradicionais |
| Aurora | Relacional | Alta performance |
| ElastiCache | Cache | Baixa latência |
| DynamoDB | NoSQL | Escala massiva |
| Neptune | Grafo | Relacionamentos |
| Timestream | Time-series | Métricas / IoT |

---

## Escolha Arquitetural (muito cobrado)

- Precisa de SQL? → **RDS / Aurora**
- Precisa de HA? → **Multi-AZ**
- Precisa de leitura escalável? → **Read Replicas**
- Lambda + RDS? → **RDS Proxy**
- Milhões de requests? → **DynamoDB**
- Cache? → **ElastiCache**
- Relacionamentos complexos? → **Neptune**
- Dados por tempo? → **Timestream**

---

## Resumo Final para a Prova

✔ Multi-AZ = Alta disponibilidade  
✔ Read Replica = Escala de leitura  
✔ Aurora = SQL cloud-native  
✔ DynamoDB = Serverless + escala  
✔ ElastiCache = Performance  
✔ Neptune = Grafos  
✔ Timestream = Séries temporais  

---

