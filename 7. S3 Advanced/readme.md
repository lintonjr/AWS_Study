## AWS Certified Solutions Architect – Associate

Esta aula aprofunda recursos **avançados do Amazon S3**, muito comuns em **cenários de arquitetura, otimização de custo, segurança e automação**, e frequentemente explorados em **questões conceituais da prova**.

---

## Objetivos da Aula

Ao final desta aula, você será capaz de:

- Aplicar corretamente **S3 Lifecycle Rules**
- Entender e usar **S3 Batch Operations**
- Interpretar métricas do **S3 Storage Lens**
- Explicar **S3 Encryption** (em repouso e em trânsito)
- Entender e configurar **S3 CORS**
- Usar **S3 Pre-signed URLs**
- Aplicar **S3 Object Lock** (WORM)
- Explicar e identificar **S3 Object Lambda**
- Resolver questões de prova com confiança

---

## Estrutura da Aula

- Lifecycle Rules
- S3 Batch Operations
- S3 Storage Lens
- S3 Encryption
- S3 CORS
- S3 Pre-signed URL
- S3 Object Lock
- S3 Object Lambda
- Revisão e mentalidade de prova

---

## S3 Lifecycle Rules

### O que são Lifecycle Rules?

São **regras automáticas** que permitem:
- Mover objetos entre **Storage Classes**
- Excluir objetos automaticamente
- Gerenciar versões antigas

### Casos comuns:
- Dados ativos → Standard
- Dados menos acessados → IA
- Arquivamento → Glacier / Deep Archive
- Exclusão após X dias

 **Na prova**  
> Sempre que o enunciado mencionar **redução automática de custo ao longo do tempo**, pense em **Lifecycle Rules**.

---

## S3 Batch Operations

### O que são?

Permitem executar **operações em larga escala** em milhões ou bilhões de objetos S3.

### Exemplos de operações:
- Copiar objetos
- Alterar ACL ou metadata
- Aplicar tags
- Restaurar objetos do Glacier
- Invocar Lambda em massa

### Casos de uso:
- Migração de dados
- Correções em massa
- Reprocessamento de objetos

 **Na prova**  
> Operação em massa no S3 → **Batch Operations**

---

## S3 Storage Lens

### O que é?

Ferramenta de **visibilidade e análise** do uso do S3 em uma conta ou organização.

### Métricas fornecidas:
- Quantidade de dados armazenados
- Crescimento ao longo do tempo
- Distribuição por Storage Class
- Uso de Lifecycle Rules
- Padrões de acesso

### Casos de uso:
- Otimização de custos
- Governança
- Compliance
- Planejamento de capacidade

 **Na prova**  
> Análise e visibilidade do uso do S3 → **Storage Lens**

---

## S3 Encryption

### Tipos de criptografia em repouso

#### 🔹 SSE-S3
- Chaves gerenciadas pela AWS
- Mais simples
- Totalmente transparente

#### 🔹 SSE-KMS
- Chaves gerenciadas no AWS KMS
- Controle de acesso e auditoria
- Custo adicional por requisição

#### 🔹 SSE-C
- Chaves fornecidas pelo cliente
- AWS não armazena a chave
- Menos comum na prova

 **Regra de prova**  
> Precisa de auditoria e controle → **SSE-KMS**  
> Simples e automático → **SSE-S3**

---

### Criptografia em trânsito

- HTTPS (TLS)
- Pode ser **exigida via Bucket Policy**

 **Na prova**  
> Forçar HTTPS → **Bucket Policy**

---

## S3 CORS (Cross-Origin Resource Sharing)

### O que é?

Permite que aplicações web **em outro domínio** acessem objetos no S3 diretamente via navegador.

### Casos comuns:
- Frontend hospedado fora do S3
- Aplicações SPA
- Upload direto do browser para o S3

**Na prova**  
> Erro de CORS ao acessar S3 via browser → **Configurar CORS no bucket**

---

## S3 Pre-signed URL

### O que é?

URLs temporárias que concedem **acesso controlado** a objetos S3.

### Características:
- Tempo de expiração definido
- Pode permitir:
  - Download
  - Upload
- Não expõe credenciais AWS

### Casos de uso:
- Compartilhamento temporário
- Upload direto do cliente
- Downloads seguros
 
 **Na prova**  
> Acesso temporário a objeto privado → **Pre-signed URL**

---

## S3 Object Lock

### O que é?

Recurso que impede a exclusão ou alteração de objetos por um período definido.

### Conceito chave: **WORM**
Write Once, Read Many

### Modos:
- **Governance Mode**
- **Compliance Mode** (nem root pode apagar)

### Casos de uso:
- Compliance regulatório
- Auditorias
- Dados imutáveis

**Na prova**  
> Dados que não podem ser apagados → **Object Lock**

---

## S3 Object Lambda

### O que é?

Permite **transformar dados em tempo real** quando o objeto é acessado, sem alterar o objeto original.

### Como funciona:
- Cliente solicita o objeto
- Lambda processa o conteúdo
- Resultado transformado é retornado

### Casos de uso:
- Mascarar dados sensíveis
- Converter formatos
- Customizar respostas por usuário

 **Na prova**  
> Transformar dados no momento do acesso → **Object Lambda**

---

## Como a AWS cobra esses temas na prova

| Cenário | Serviço |
|------|--------|
| Otimizar custo automaticamente | Lifecycle Rules |
| Operação em massa | Batch Operations |
| Analisar uso do S3 | Storage Lens |
| Criptografia com auditoria | SSE-KMS |
| Acesso via browser | CORS |
| Acesso temporário | Pre-signed URL |
| Dados imutáveis | Object Lock |
| Transformação dinâmica | Object Lambda |

---

## Conclusão

Esses recursos representam o **nível avançado do S3** e costumam aparecer em:
- Questões de arquitetura
- Questões de segurança
- Questões de custo
- Questões de automação

Dominar esses tópicos aumenta **muito** sua taxa de acerto na prova.

---

