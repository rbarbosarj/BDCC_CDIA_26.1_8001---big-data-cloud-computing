# AC3 – Modelos de Banco de Dados e Arquiteturas de Dados

**Aluno:** Renan Barbosa
**Curso:** Engenharia de Computação
**Disciplina:** Big Data & Cloud Computing
**Código:** BDCC_CDIA_26.1_8001
**Avaliação:** AC03
**Ano:** 2026

---

# Questões Objetivas

## Questão 1

### Resposta:

**c) Colunar**

### Justificativa:

Bancos de dados colunares são otimizados para workloads analíticos (OLAP), nos quais é necessário executar agregações e consultas complexas sobre grandes volumes de dados. Diferentemente dos bancos orientados a linhas, o armazenamento colunar permite leitura seletiva apenas das colunas necessárias, reduzindo operações de I/O e aumentando significativamente a performance.

Além disso, bancos colunares oferecem:

* Alta compressão de dados
* Melhor throughput analítico
* Redução de custo por consulta
* Excelente escalabilidade para Big Data

Considerando o cenário com aproximadamente 500 milhões de registros e consultas analíticas envolvendo região, categoria e período, o modelo colunar é o mais adequado arquiteturalmente.

---

## Questão 2

### Resposta:

**c) Orientado a documentos**

### Justificativa:

Aplicações modernas com requisitos dinâmicos necessitam de flexibilidade estrutural. Bancos orientados a documentos permitem *schema flexibility*, possibilitando que diferentes documentos possuam atributos distintos sem necessidade de migrations complexas.

Esse modelo oferece:

* Evolução rápida do schema
* Desenvolvimento ágil
* Escalabilidade horizontal
* Flexibilidade estrutural

No cenário apresentado, os perfis de usuários possuem atributos variáveis, tornando o modelo orientado a documentos a melhor escolha.

---

## Questão 3

### Resposta:

**c) Relacional (tabular)**

### Justificativa:

Sistemas financeiros exigem consistência forte e suporte completo às propriedades ACID (Atomicidade, Consistência, Isolamento e Durabilidade).

Bancos relacionais são os mais adequados porque oferecem:

* Integridade referencial
* Transações multi-tabela
* Controle transacional robusto
* Consistência absoluta dos dados

Operações bancárias como débito e crédito exigem atomicidade para evitar inconsistências financeiras, característica suportada nativamente por bancos relacionais.

---

## Questão 4

### Resposta:

**b) II, apenas**

### Justificativa:

* **I – Falsa:** bancos colunares armazenam dados por coluna, e não por linha.
* **II – Verdadeira:** bancos orientados a documentos utilizam esquema flexível.
* **III – Falsa:** bancos relacionais tradicionais são otimizados principalmente para workloads transacionais (OLTP), e não para analytics massivo (OLAP).

---

## Questão 5

### Resposta:

**c) Amazon Redshift**

### Justificativa:

O Amazon Redshift é um Data Warehouse colunar totalmente gerenciado pela AWS, projetado para consultas analíticas em larga escala.

Suas principais características incluem:

* Arquitetura colunar
* Processamento Massivamente Paralelo (MPP)
* Alta compressão
* Excelente performance analítica
* Integração com o ecossistema AWS

Para workloads analíticas envolvendo dezenas ou centenas de terabytes, o Redshift apresenta excelente relação entre custo e performance.

---

# Questões Discursivas

# Questão Discursiva 1 – Cenário Integrador

## Arquitetura de Dados – Cenário Integrador

```mermaid
flowchart LR

A[Sistema de Vendas OLTP] --> B[(Amazon RDS)]
C[Catálogo de Produtos] --> D[(Amazon DynamoDB)]
E[Data Warehouse OLAP] --> F[(Amazon Redshift)]

B --> G[Aplicações Transacionais]
D --> G
F --> H[Business Intelligence / Analytics]
```

---

## a) Modelo de banco de dados ideal para cada necessidade

| Necessidade              | Modelo de Banco        | Justificativa                                                |
| ------------------------ | ---------------------- | ------------------------------------------------------------ |
| Sistema de vendas (OLTP) | Relacional             | Necessita ACID, integridade referencial e consistência forte |
| Data Warehouse (OLAP)    | Colunar                | Otimizado para consultas analíticas e agregações massivas    |
| Catálogo de produtos     | Orientado a documentos | Permite flexibilidade estrutural e evolução dinâmica         |

---

## Sistema de vendas (OLTP)

O sistema transacional da empresa exige processamento consistente e confiável de milhares de operações simultâneas envolvendo estoque, vendas e clientes.

O modelo relacional é o mais adequado devido ao suporte a:

* Transações ACID
* Integridade referencial
* Controle transacional
* Consistência forte

Esse modelo é ideal para workloads OLTP, onde confiabilidade e precisão são prioritárias.

### Serviço AWS recomendado:

**Amazon RDS (PostgreSQL ou MySQL)**

O Amazon RDS fornece:

* Gerenciamento automatizado
* Backups automáticos
* Replicação Multi-AZ
* Alta disponibilidade
* Escalabilidade vertical simplificada

### Vantagens:

* Consistência forte
* Integridade transacional
* Segurança operacional

### Desvantagens:

* Escalabilidade horizontal mais limitada
* Menor flexibilidade estrutural

---

## Data Warehouse (OLAP)

O ambiente analítico precisa processar aproximadamente 5 PB de dados históricos para consultas complexas da diretoria.

Nesse cenário, o modelo colunar é o mais eficiente porque:

* Reduz leitura desnecessária de dados
* Aumenta compressão
* Melhora throughput analítico
* Otimiza agregações massivas

Bancos colunares são projetados especificamente para workloads analíticas.

### Serviço AWS recomendado:

**Amazon Redshift**

O Redshift utiliza arquitetura MPP (*Massively Parallel Processing*), permitindo execução distribuída de consultas analíticas.

### Vantagens:

* Alta performance analítica
* Excelente compressão
* Escalabilidade para Big Data

### Desvantagens:

* Não otimizado para workloads transacionais
* Maior latência para escrita frequente

---

## Catálogo de produtos

O catálogo apresenta alta variabilidade estrutural, pois diferentes categorias possuem atributos distintos.

O modelo orientado a documentos é ideal devido ao *schema flexibility*, permitindo:

* Estruturas diferentes por documento
* Evolução rápida da aplicação
* Redução de migrations
* Maior agilidade de desenvolvimento

### Serviço AWS recomendado:

**Amazon DynamoDB**

O DynamoDB fornece:

* Escalabilidade horizontal automática
* Baixa latência
* Alta disponibilidade
* Arquitetura serverless

### Vantagens:

* Flexibilidade estrutural
* Escalabilidade horizontal
* Alto desempenho

### Desvantagens:

* JOINs limitados
* Consultas relacionais mais complexas

---

# Questão Discursiva 2 – Persistência Poliglota e Arquitetura Distribuída

## Arquitetura de Persistência Poliglota

```mermaid
flowchart TD

A[Eventos de Rastreamento] --> B[(Amazon Redshift)]
C[Configuração de Caminhões] --> D[(Amazon DynamoDB)]
E[Cobrança e Faturamento] --> F[(Amazon RDS PostgreSQL)]

G[API Gateway / Microsserviços]
G --> B
G --> D
G --> F

H[AWS Glue / ETL]
H --> B
H --> D
H --> F
```

---

## a) Arquitetura proposta

A startup deve adotar uma arquitetura de persistência poliglota, utilizando diferentes modelos especializados conforme as características de cada workload.

| Desafio                 | Modelo                 | Serviço AWS           |
| ----------------------- | ---------------------- | --------------------- |
| Rastreamento de eventos | Colunar                | Amazon Redshift       |
| Configurações flexíveis | Orientado a documentos | Amazon DynamoDB       |
| Cobrança e faturamento  | Relacional             | Amazon RDS PostgreSQL |

---

## Desafio 1 – Rastreamento de entregas

O sistema gera aproximadamente 1 milhão de eventos por hora, caracterizando um workload analítico massivo.

O modelo colunar é o mais adequado porque:

* Otimiza consultas analíticas
* Processa bilhões de registros eficientemente
* Reduz custo computacional
* Melhora agregações e filtros

### Serviço AWS:

**Amazon Redshift**

O Redshift permite analytics distribuído em larga escala utilizando processamento paralelo massivo.

---

## Desafio 2 – Configurações flexíveis de caminhões

Cada caminhão possui atributos distintos, sensores específicos e estruturas variáveis.

O modelo orientado a documentos oferece:

* *Schema flexibility*
* Evolução dinâmica do modelo
* Redução de migrations
* Desenvolvimento mais ágil

### Serviço AWS:

**Amazon DynamoDB**

O DynamoDB suporta workloads altamente escaláveis com baixa latência e flexibilidade estrutural.

---

## Desafio 3 – Cobrança e faturamento

O sistema financeiro exige consistência absoluta e garantia de integridade transacional.

O modelo relacional continua sendo a melhor escolha devido ao suporte a:

* ACID
* Integridade referencial
* Controle transacional robusto
* Consistência forte

### Serviço AWS:

**Amazon RDS PostgreSQL**

O PostgreSQL oferece maturidade transacional e confiabilidade operacional para workloads financeiros.

---

## b) Estratégias para reduzir a complexidade operacional

### 1. Orquestração e Integração de Dados

Ferramentas de integração permitem sincronização entre múltiplos bancos de dados especializados.

Exemplos:

* AWS Glue
* Apache Airflow
* AWS Step Functions

Essas soluções automatizam pipelines ETL/ELT e reduzem inconsistências operacionais.

---

### 2. Camada Unificada de APIs

A utilização de API Gateway e microsserviços desacopla aplicações dos bancos específicos.

Benefícios:

* Redução do acoplamento
* Centralização do acesso
* Facilidade de manutenção
* Maior governança arquitetural

---

## c) Modelo inadequado para o Desafio 1

### Modelo inadequado:

**Relacional**

### Justificativa:

* Escalabilidade horizontal limitada
* Menor eficiência analítica
* Consultas lentas sobre bilhões de registros
* Alto custo operacional em workloads OLAP

Bancos relacionais são projetados prioritariamente para workloads transacionais (OLTP), enquanto o cenário apresentado exige processamento analítico massivo (OLAP), melhor atendido por arquiteturas colunares.
