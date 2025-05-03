# README – Lab 4: VPC Personalizada com Bastion e Backend

## 📘 Sobre este projeto

Este repositório documenta o Laboratório 4 da Formação Técnica AWS Cloud Foundations, onde foi construída uma arquitetura de rede com segurança segmentada utilizando VPC personalizada, Bastion Host e servidor Backend privado.

## 📐 Arquitetura final

```
VPC: 10.0.0.0/16
|
|-- Sub-rede Pública (10.0.1.0/24) – Bastion EC2 + Internet Gateway (IGW)
|-- Sub-rede Privada (10.0.2.0/24) – Backend EC2 + NAT Gateway
```

## 📌 Recursos criados

* VPC: `lab-vpc`
* Sub-redes: `lab-subnet-publica` e `lab-subnet-privada`
* IGW: `lab-igw` com rota 0.0.0.0/0
* NAT Gateway: `lab-nat-gateway` na sub-rede pública
* Route Tables:

  * `lab-rt-publica`: para sub-rede pública
  * `lab-rt-privada`: para sub-rede privada com saída via NAT
* Security Groups:

  * `lab-sg-bastion`: permite SSH apenas do IP pessoal
  * `lab-sg-backend`: permite SSH somente da Bastion
* EC2:

  * `lab-ec2-bastion` (pública)
  * `lab-ec2-backend` (privada)

## 🔐 Acesso e Segurança

* A Bastion foi acessada via SSH com chave `.pem`
* A chave foi copiada para a Bastion via SCP para acessar o Backend:

  ```bash
  scp -i lab-key-bastion.pem lab-key-bastion.pem ec2-user@<IP-BASTION>:/tmp/
  ssh -i ~/lab-key-bastion.pem ec2-user@<IP-PRIVADO-BACKEND>
  ```

## ⚠️ Pontos de Atenção

* O **NAT Gateway cobra por hora ativa**, mesmo sem tráfego
* Elastic IP **cobra se não estiver associado**
* Verificar se as rotas foram corretamente atribuídas às sub-redes
* EC2 sem chave ou com Security Group incorreto impede acesso

## ✅ Testes realizados

* [x] Acesso externo ao Bastion
* [x] Acesso interno da Bastion ao Backend
* [x] Isolamento de segurança validado por SGs
* [x] Comunicação de saída da sub-rede privada via NAT

## 🧭 Próximos passos

* Automatizar essa estrutura com Terraform ou AWS CLI
* Estender a VPC para múltiplas AZs e alta disponibilidade
* Implementar RDS, Load Balancer e Auto Scaling futuramente

---

Este README representa a documentação técnica mínima da entrega do Lab 4. Todos os recursos foram criados de forma manual para maximizar o aprendizado e domínio dos conceitos fundamentais de redes na AWS.
