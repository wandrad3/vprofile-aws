📘 Tutorial de Aprovisionamento de Aplicação Java com AWS CloudFormation


ℹ️ Arquitetura da Aplicação:

A aplicação Java vprofile é agora provisionada inteiramente na AWS utilizando um template CloudFormation, substituindo a abordagem anterior com Vagrant e Ruby.

🔗 Repositório anterior com Vagrant e Ruby
https://github.com/wandrad3/automated-provisioning-java-application

🔗 Repositório da Aplicação:
https://github.com/devopshydclub/vprofile-project.git

🧩 Componentes Provisionados na AWS
EC2 Auto Scaling com Apache Tomcat para hospedagem da aplicação Java.
Application Load Balancer (ALB) para distribuição de tráfego.
Aurora MySQL Cluster como banco de dados principal.
ElastiCache Memcached para cache distribuído.
Amazon Route 53 para resolução DNS (simulado).
CloudFormation Template para infraestrutura como código.


🚀 Provisionamento com CloudFormation
Prepare o Ambiente:

Suba o stack via AWS CloudFormation (via Console ou CLI). Forneça sua KeyPair para acesso SSH às instâncias.

## Aplicação Java:

O script embutido no LaunchTemplate instala o Java, Tomcat e realiza o deploy do WAR compilado. O application.properties é gerado dinamicamente com os endpoints de Aurora e ElastiCache.

## Serviços AWS Envolvidos:

EC2, VPC, Subnets, Security Groups, Load Balancer, Auto Scaling, RDS Aurora, ElastiCache.

📈 Diagrama da Arquitetura

```mermaid
---
config:
  layout: fixed
---

flowchart TD
 subgraph subGraph0["Public Subnet"]
        ALB["⚖️ Application Load Balancer"]
        Internet["🌐 Internet"]
        APP01["🖥️ App01 - EC2"]
        APP02["🖥️ App02 - EC2"]
  end
 subgraph subGraph1["Private Subnet"]
        ElastiCache["⚡ ElasticCache - Memcached"]
        AuroraDB["💾 AuroraDB Cluster"]
  end
    Internet --> ALB
    ALB --> APP01 & APP02
    APP01 --> ElastiCache & AuroraDB
    APP02 --> ElastiCache & AuroraDB


📈 Desenho da Arquitetura


![vagrant-file-arc](https://github.com/user-attachments/assets/a7ce31e6-3661-4c4a-a01c-acd3cec8f828)

  
