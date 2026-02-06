## AWS Certified Solutions Architect – Associate

O **Amazon VPC** é um dos temas mais críticos da prova.  
Grande parte das questões de arquitetura envolvem **rede, isolamento, conectividade e segurança**, mesmo quando o foco parece ser outro serviço.

---

## Objetivos da Aula

Ao final desta aula, você será capaz de:

- Entender o que é uma **VPC** e por que ela existe
- Trabalhar corretamente com **CIDR, IP público e privado**
- Projetar **subnets públicas e privadas**
- Entender **Internet Gateway e Route Tables**
- Diferenciar **NAT Instance e NAT Gateway**
- Aplicar corretamente **Security Groups e NACLs**
- Entender **VPC Peering**
- Usar **VPC Endpoints**
- Saber quando usar **AWS Direct Connect**
- Resolver questões de prova com segurança

---

## Estrutura da Aula

- Introdução à VPC
- CIDR e Endereçamento IP
- Subnets
- Internet Gateway e Route Tables
- NAT Instance vs NAT Gateway
- Segurança: NACL vs Security Groups
- VPC Peering
- VPC Endpoints
- Direct Connect
- Revisão e mentalidade de prova

---

## Amazon VPC – Conceito Fundamental

Uma **VPC (Virtual Private Cloud)** é uma **rede virtual isolada**, totalmente controlada pelo cliente dentro da AWS.

Ela permite:
- Definir intervalos de IP
- Criar subnets
- Controlar roteamento
- Controlar acesso de rede

 **Na prova**  
> Sempre que o enunciado falar em **isolamento de rede**, pense em **VPC**.

---

## CIDR, IP Público e IP Privado

### CIDR (Classless Inter-Domain Routing)

O CIDR define o **intervalo de IPs** da VPC.

Exemplo conceitual:
- `10.0.0.0/16` → rede grande
- `10.0.1.0/24` → subnet menor

 Regras importantes:
- CIDR não pode ser alterado facilmente depois
- Planejamento correto é essencial

---

### IP Privado
- Usado para comunicação **interna**
- Não acessível pela Internet
- Padrão para EC2 dentro da VPC

### IP Público
- Usado para comunicação com a Internet
- Pode mudar quando a instância reinicia

 **Na prova**  
> Comunicação interna → IP privado  
> Acesso pela Internet → IP público ou Elastic IP

---

## Subnets

Uma **Subnet** é uma subdivisão do CIDR da VPC e sempre pertence a **uma única Availability Zone**.

### Tipos principais:

#### Subnet Pública
- Possui rota para a Internet
- Associada a um **Internet Gateway**
- Usada para:
  - Load Balancers
  - Bastion Hosts
  - EC2 públicas

#### Subnet Privada
- **Não possui acesso direto à Internet**
- Usada para:
  - Application servers
  - Databases
  - Backends

 **Regra de prova**
> Database nunca deve estar em subnet pública.

---

## Internet Gateway & Route Tables

### Internet Gateway (IGW)

É o componente que permite comunicação entre a VPC e a Internet.

Características:
- Um por VPC
- Escalável
- Altamente disponível

---

### Route Tables

Definem **para onde o tráfego vai**.

Exemplos conceituais:
- Tráfego local → dentro da VPC
- Tráfego externo → Internet Gateway
- Tráfego privado → NAT

 **Na prova**
> Sem rota, não há comunicação — mesmo com IP público.

---

## NAT Instance vs NAT Gateway

Ambos permitem que **instâncias em subnet privada acessem a Internet**, sem permitir acesso de entrada.

---

### NAT Instance (Legado)

- EC2 configurada manualmente
- Requer:
  - Disable source/destination check
  - Alta manutenção
- Escalabilidade manual

 Cai pouco, mas pode aparecer.

---

### NAT Gateway (Recomendado)

- Serviço gerenciado
- Escala automaticamente
- Alta disponibilidade
- Menor risco operacional

 **Regra de prova**
> Acesso à Internet a partir de subnet privada → **NAT Gateway**

---

## Segurança: NACL vs Security Groups

### Security Groups

- Stateful (retorno automático permitido)
- Associado à **instância**
- Controla tráfego **permitido**

Usado como:
> Firewall da instância

---

### Network ACL (NACL)

- Stateless (regras de entrada e saída explícitas)
- Associado à **subnet**
- Avaliado por ordem de regra

Usado como:
> Firewall da subnet

---

### Comparação Importante

| Característica | Security Group | NACL |
|--------------|---------------|------|
| Stateful | Sim | Não |
| Nível | Instância | Subnet |
| Regras de deny | Não | Sim |

 **Na prova**
> Controle fino por instância → Security Group  
> Controle de subnet inteira → NACL

---

## VPC Peering

### O que é?

Permite comunicação **privada** entre duas VPCs.

### Características:
- Tráfego não passa pela Internet
- Usa IPs privados
- Não é transitivo

 **Limitação importante**
> VPC A ↔ VPC B  
> VPC B ↔ VPC C  
> **VPC A não fala com VPC C**

 **Na prova**
> Comunicação simples entre VPCs → VPC Peering

---

## VPC Endpoints

Permitem acessar **serviços AWS** sem sair da rede da AWS.

### Tipos:

#### Gateway Endpoint
- S3
- DynamoDB

#### Interface Endpoint
- ENI privado
- A maioria dos serviços AWS

### Benefícios:
- Mais segurança
- Menor latência
- Sem NAT ou Internet Gateway

 **Na prova**
> Acessar S3 sem Internet → **VPC Endpoint**

---

## AWS Direct Connect

### O que é?

Conexão **dedicada e privada** entre o data center on-premises e a AWS.

### Casos de uso:
- Latência previsível
- Alta largura de banda
- Compliance
- Grandes volumes de dados

 **Na prova**
> Conexão privada e estável → **Direct Connect**

---

## Como a AWS cobra VPC na prova

| Cenário | Escolha |
|------|--------|
| Isolamento de rede | VPC |
| Comunicação interna | IP privado |
| Subnet sem Internet | Subnet privada |
| Acesso Internet privado | NAT Gateway |
| Firewall da instância | Security Group |
| Firewall da subnet | NACL |
| Comunicação entre VPCs | VPC Peering |
| Acesso AWS sem Internet | VPC Endpoint |
| Conexão on-prem privada | Direct Connect |

---

## Conclusão

Se você dominar:
- Subnets
- Roteamento
- NAT
- Segurança
- Conectividade

Você resolve **a maioria das questões de rede da prova AWS SAA**.

---

