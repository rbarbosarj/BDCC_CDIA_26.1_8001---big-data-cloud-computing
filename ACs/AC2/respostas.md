# AC2 – Computação em Nuvem

**Aluno:** Renan Barbosa
**Curso:** Engenharia de Computação
**Disciplina:** Computação em Nuvem
**Ano:** 2026

---

## 1. Questões Objetivas

### Questão 1

**Resposta:** a) IaaS

**Justificativa:**
A aplicação é legada e depende de Windows Server, IIS e configurações específicas. O modelo IaaS permite controle total sobre sistema operacional, rede e dependências, possibilitando replicar o ambiente original sem necessidade de reescrita.

---

### Questão 2

**Resposta:** b) AWS Elastic Beanstalk

**Justificativa:**
O Elastic Beanstalk automatiza provisionamento, deploy e escalabilidade, sendo ideal para MVPs com equipe reduzida e necessidade de rápida entrega.

---

### Questão 3

**Resposta:** c) I e II, apenas

**Justificativa:**
No IaaS, o provedor gerencia infraestrutura e virtualização, enquanto o cliente gerencia o sistema operacional e aplicações.
No PaaS, o provedor gerencia o sistema operacional e patches.
No SaaS, o cliente não controla o ambiente de execução.

---

### Questão 4

**Resposta:** c) SaaS

**Justificativa:**
O CRM é fornecido como serviço pronto, eliminando a necessidade de gerenciamento de infraestrutura, atualizações e backups.

---

### Questão 5

**Resposta:** d) AWS Elastic Beanstalk

**Justificativa:**
O desenvolvedor deseja apenas enviar o código, delegando à plataforma a gestão de infraestrutura, escalabilidade e balanceamento.

---

## 2. Questão Discursiva 1

O modelo mais adequado para a migração é o **IaaS (Infrastructure as a Service)**.

A empresa possui um sistema legado com dependências específicas de Java, banco Oracle e configurações de rede. O IaaS permite reproduzir esse ambiente na nuvem com alto nível de compatibilidade, sem necessidade de reescrever a aplicação.

A estratégia mais adequada é o modelo **lift-and-shift**, no qual a aplicação é migrada para a nuvem com mínimas alterações estruturais. Isso reduz riscos e tempo de migração.

No modelo IaaS, a empresa mantém controle sobre sistema operacional, banco de dados e configurações, enquanto o provedor gerencia infraestrutura física, rede e virtualização. Isso é vantajoso considerando a experiência da equipe de TI.

O PaaS exigiria adaptações significativas da aplicação, o que pode aumentar custo e complexidade. Já o SaaS não se aplica, pois o sistema é proprietário.

Na AWS, a solução pode utilizar:

* Amazon EC2 para execução das instâncias
* Amazon VPC para configuração de rede
* Amazon RDS ou EC2 para banco de dados

Além disso, arquiteturas Multi-AZ garantem alta disponibilidade e tolerância a falhas (fault tolerance), aumentando a resiliência do sistema.

Em termos de custos, há redução de CapEx e migração para OpEx, eliminando gastos com hardware físico, energia e manutenção.

---

## 3. Questão Discursiva 2

Para esse cenário, o modelo mais adequado é o **PaaS (Platform as a Service)**.

O IaaS oferece controle total, mas exige gerenciamento de infraestrutura, segurança, escalabilidade e monitoramento, o que pode sobrecarregar uma equipe pequena.

O PaaS permite foco no desenvolvimento da aplicação, automatizando provisionamento, balanceamento, escalabilidade e manutenção. Isso acelera o desenvolvimento e reduz o tempo de lançamento.

A escalabilidade horizontal permite atender ao crescimento de usuários sem intervenção manual, sendo essencial para suportar até 100 mil acessos simultâneos.

Na AWS, a arquitetura pode utilizar:

* AWS Elastic Beanstalk para deploy e escalabilidade
* Amazon RDS para banco de dados gerenciado
* Amazon S3 para armazenamento de arquivos
* Amazon CloudFront (CDN) para distribuição de conteúdo

Além disso, serviços como Auto Scaling e Application Load Balancer garantem alta disponibilidade e desempenho.

Dessa forma, o PaaS atende melhor aos requisitos de agilidade, escalabilidade e baixo custo inicial, reduzindo a complexidade operacional e permitindo foco no desenvolvimento da solução.
