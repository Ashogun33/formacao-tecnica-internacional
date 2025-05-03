# Lab 5 – Amazon RDS (Banco de Dados Relacional)

🎯 **Objetivo:**  
Compreender o funcionamento do Amazon RDS criando uma instância PostgreSQL para fins exclusivamente didáticos, **sem incorrer em custos adicionais**. A instância será observada e **removida em até 30 minutos**.

---

## ✅ Requisitos
- Instância elegível para o Free Tier (`db.t3.micro` ou `db.t2.micro`)
- Engine: PostgreSQL (preferencial) ou MySQL
- Sem conexão nem importação de dados
- Sem armazenamento extra ou autoscaling
- Backup desativado
- Acesso público desabilitado
- Exclusão imediata após visualização

---

## 🧭 Etapas do Lab

### 1. Acessar o Console RDS
- Acesse com seu **usuário IAM administrativo**.
- Vá para o serviço **Amazon RDS**.

---

### 2. Criar o DB Subnet Group
> Define as subnets privadas em AZs diferentes onde a instância RDS poderá ser implantada.

- Menu lateral: **Subnet groups > Create DB Subnet Group**
- **Name**: `rds-subnet-group`
- **VPC**: selecione a VPC criada no Lab 4
- **Availability Zones**: selecione duas diferentes (ex: `us-east-1a`, `us-east-1b`)
- **Subnets**: adicione duas subnets privadas (uma por AZ)

---

### 3. Criar a Instância PostgreSQL
- Clique em **Create database**
- **Engine**: PostgreSQL
- **Template**: **Free Tier**
- **DB Instance ID**: `lab5-db`
- **Username**: `admin`
- **Password**: `Lab5Test123` (exemplo)
- **Classe da instância**: `db.t3.micro`
- **Armazenamento**: 20 GB (desabilitar autoscaling)
- **Backup**: 0 dias
- **Public access**: **NO**
- **VPC Security Group**: use um grupo que permita acesso apenas via bastion host (se houver)
- **Subnet group**: `rds-subnet-group`
- **Monitoring e upgrades automáticos**: desabilitados

> ✅ Clique em **Create database**

---

### 4. Visualizar Informações da Instância
- Aguarde o status: `Available`
- Veja os dados:
  - **Endpoint**
  - **Porta (5432)**
  - **Parameter Group** e **Subnet Group**
- Não conectar, importar ou executar scripts SQL.

---

### 5. Excluir Instância
- Menu: **Actions > Delete**
- Confirmar sem snapshot.
- Tempo máximo de permanência: **30 minutos**

---

## 🧠 Conceitos aprendidos

| Item               | Descrição                                                                 |
|--------------------|---------------------------------------------------------------------------|
| **Engine**         | Tipo de banco (PostgreSQL, MySQL etc.)                                    |
| **Subnet Group**   | Define as subnets privadas para a instância                               |
| **Endpoint**       | Endereço privado de conexão dentro da VPC                                 |
| **Parameter Group**| Define configurações da engine (ex: timezone, max_connections)            |
| **Boas práticas**  | Acesso privado, backups desativados, instância mínima e remoção imediata  |

---

## 🚨 Observações de Custo
- **Instâncias RDS são cobradas por hora**, mesmo em poucos minutos.
- Free Tier cobre 750 horas por mês *somadas* entre instâncias RDS.
- **Nunca deixe instância ativa sem uso.**

---

📁 *Este laboratório faz parte do projeto: Formação Técnica – AWS Cloud Foundations*
