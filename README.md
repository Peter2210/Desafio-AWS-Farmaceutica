# Projeto AWS: Otimização e Redução de Custos em Infraestrutura Cloud

## Descrição do Projeto

Neste projeto será apresentado estratégia de migração e otimização na AWS para uma empresa do setor farmacêutico. A empresa nesta situação atua como um hub de distribuição, conectando diversas outras empresas do setor, o que exige um sistema robusto, escalável e com alto controle financeiro.

O objetivo da solução é sair de um modelo on-premise, aplicando as melhores práticas de **Cloud Computing** para reduzir drásticamente os custos operacionais de TI, além de garantir alta disponibilidade e segurança dos dados.

---

## Contexto da Empresa

* **Empresa:** Abstergo Industries
* **Setor:** Distribuição Farmacêutica (Hub B2B)
* **Desafio:** Custos altos com infraestrutura local ociosa, quedas de sistema durante picos de pedidos e falta de visibilidade financeira sobre os gastos de TI.

## Objetivos da Arquitetura

1. **Redução de Custos (FinOps):** Implementar serviços sob demanda e rotinas de ciclo de vida de dados.
2. **Escalabilidade:** Suportar picos de acessos sem lentidão (ex: fechamento de mês ou campanhas).
3. **Segurança e Conformidade:** Proteger dados sensíveis e notas fiscais de acordo com as normas do setor.
4. **Alta Disponibilidade:** Garantir que o hub de distribuição opere 24/7 sem interrupções.

---

## Serviços AWS Utilizados e Proposta de Valor

### 1. Computação e Escalabilidade
* **Amazon EC2 + Auto Scaling:** Os servidores virtuais hospedam o portal da empresa. O Auto Scaling foi adicionado para criar novas instâncias automaticamente durante picos de tráfego e desligá-las à noite/finais de semana, cobrando apenas o que for utilizado.
* **Elastic Load Balancing (ELB):** Distribui o tráfego de entrada entre as instâncias EC2, evitando que um único servidor fique sobrecarregado.

### 2. Armazenamento Inteligente
* **Amazon S3 (Standard & Intelligent-Tiering):** Utilizado para guardar documentos recentes, imagens e relatórios diários com alta durabilidade.
* **Amazon S3 Glacier:** Implementação de políticas de ciclo de vida para arquivar notas fiscais e backups antigos, reduzindo o custo de armazenamento.

### 3. Banco de Dados Gerenciado
* **Amazon RDS (Relational Database Service):** Hospeda o banco de dados relacional com dados críticos de estoque e clientes, além de oferecer backups automáticos, atualizações de patch sem esforço e configuração Multi-AZ para contingência.

### 4. Mensageria e Desacoplamento
* **Amazon SQS (Simple Queue Service):** Utilizado para enfileirar os milhares de pedidos recebidos das farmacêuticas simultaneamente e garantir que nenhum pedido seja perdido caso o banco de dados esteja processando outras requisições.

### 5. Segurança e Governança
* **Amazon VPC (Virtual Private Cloud):** Isola a rede da empresa, com o banco de dados (RDS) em uma sub-rede privada, inacessível pela internet, comunicando-se apenas com o EC2.
* **AWS Cost Explorer & Budgets:** Ferramentas configuradas para o gestor financeiro monitorar os gastos em tempo real e receber alertas caso os custos ultrapassem o orçamento.

## Tecnologias Utilizadas

* AWS EC2
* AWS S3
* AWS Glacier
* AWS RDS
* AWS SQS
* AWS VPC
* Elastic Load Balancer
* AWS Auto Scaling
* AWS Cost Explorer

---

## Arquitetura da Solução

1. Os parceiros e clientes acessam a aplicação através da internet, passando primeiro pelo **Elastic Load Balancer (ELB)**.
2. O ELB direciona o tráfego para um grupo de instâncias **Amazon EC2** gerenciadas pelo Auto Scaling.
3. Pedidos complexos ou massivos são enviados para o **Amazon SQS** para processamento assíncrono.
4. O EC2 se comunica de forma segura via rede privada (VPC) com o **Amazon RDS** para gravar e ler dados de estoque e faturamento.
5. Arquivos, notas fiscais e comprovantes são salvos no **Amazon S3**. Após 90 dias, políticas automáticas movem esses arquivos para o **S3 Glacier** para redução de custos.
6. O **AWS Cost Explorer** gera dashboards mensais para a diretoria.

---

## Benefícios e Resultados Esperados

* **Economia Real:** Substituição de custos fixos de hardware por custos variáveis com o uso de Instâncias Reservadas/Savings Plans junto ao S3 Glacier.
* **Resiliência:** O sistema não cai mais em dias de pico graças ao Auto Scaling e ao SQS.
* **Segurança:** Dados críticos isolados em sub-redes privadas (VPC), mitigando riscos de vazamentos.
* **Foco no Negócio:** A equipe de TI deixa de focar em manutenção de hardware e passa a focar em melhorar a plataforma do hub.

---

## Autor

**Pedro Henrique Meller Silva** *Estudante de Cloud Computing | Desafio de Projeto DIO*
