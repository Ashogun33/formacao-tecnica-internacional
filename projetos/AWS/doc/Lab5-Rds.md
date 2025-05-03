# 💾 Lab 5 – Amazon RDS (PostgreSQL)

Este laboratório tem como objetivo compreender o funcionamento e a arquitetura do Amazon RDS utilizando uma instância PostgreSQL **elegível ao Free Tier**, de forma segura e **sem gerar custos adicionais**.

> ⏱️ **Importante**: A instância foi criada apenas para fins didáticos e foi excluída **antes de completar 30 minutos**, evitando qualquer cobrança.

---

## 🎯 Objetivos do Lab

- Criar uma instância RDS usando PostgreSQL no Free Tier
- Entender conceitos como:
  - **DB Subnet Group**
  - **Engine**
  - **Endpoint**
  - **Parameter Group**
- Aplicar práticas seguras de provisionamento
- Remover a instância após análise de console

---

## ⚙️ Detalhes Técnicos

- **Engine**: PostgreSQL
- **Classe**: `db.t3.micro`
- **Armazenamento**: 20 GB (sem autoscaling)
- **Backup automático**: desativado
- **Acesso público**: desabilitado
- **Subnets**: privadas, distribuídas em 2 AZs
- **VPC**: personalizada (Lab 4)
- **DB Subnet Group**: configurado manualmente

---

## 🔐 Boas Práticas Aplicadas

- Isolamento em sub-redes privadas
- Sem exposição pública da instância
- Recursos mínimos para evitar desperdícios
- Nenhuma conexão ou carga de dados executada
- Exclusão manual após verificação de provisionamento

---

## 🧠 Aprendizado

Durante este laboratório, os seguintes conceitos foram explorados:

- Como funciona o isolamento de banco de dados em sub-redes privadas
- Como o RDS gera endpoints internos para conexão via VPC
- Como configurar uma instância segura sem custos extras
- Importância de manter o controle de tempo para evitar cobranças

---

## 🚨 Aviso de Custos

Este laboratório foi cuidadosamente monitorado:
- A instância foi removida **manualmente** antes de 30 minutos de uso
- Nenhum dado foi gravado
- Nenhuma funcionalidade além do console foi utilizada

---

## 📁 Projeto: Formação Técnica – AWS Cloud Foundations

> Repositório voltado à documentação dos laboratórios práticos em AWS com foco didático e arquitetural.
