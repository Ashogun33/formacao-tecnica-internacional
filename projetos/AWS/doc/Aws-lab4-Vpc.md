# Lab 4 – AWS VPC Personalizada com Bastion e Backend

## 🌐 Sobre este projeto

Este é um exercício prático realizado como parte da Formação Técnica AWS Cloud Foundations. O objetivo deste laboratório é aprender a criar uma VPC personalizada na AWS com isolamento de rede, sub-redes públicas e privadas, e controle de acesso seguro via Bastion Host.

Ao final, foi montada a seguinte estrutura de rede:

```
VPC: 10.0.0.0/16
|
|-- Sub-rede Pública (10.0.1.0/24) – Bastion EC2 + Internet Gateway (IGW)
|-- Sub-rede Privada (10.0.2.0/24) – Backend EC2 + NAT Gateway
```

---

## 📌 O que foi feito (Resumo)

### 🔷 VPC e Sub-redes

* Criada VPC `lab-vpc` com faixa 10.0.0.0/16, DNS Resolution e Hostnames habilitados.
* Criadas duas sub-redes:

  * `lab-subnet-publica` – 10.0.1.0/24
  * `lab-subnet-privada` – 10.0.2.0/24

### 🔷 Roteamento e Acesso à Internet

* Internet Gateway `lab-igw` criado e associado à VPC
* Rota pública com destino 0.0.0.0/0 → IGW
* NAT Gateway `lab-nat-gateway` criado na sub-rede pública
* Rota privada com destino 0.0.0.0/0 → NAT Gateway

### 🔷 Segurança com Security Groups

* `lab-sg-bastion`: permite SSH (porta 22) **somente do IP pessoal**
* `lab-sg-backend`: permite SSH **somente do Bastion**

### 🔷 Instâncias EC2

* `lab-ec2-bastion`:

  * Sub-rede pública
  * IP público habilitado
  * Acesso via `.pem` do computador local
* `lab-ec2-backend`:

  * Sub-rede privada
  * Sem IP público
  * Acesso somente via Bastion usando SSH interno

### 🔷 Acesso Seguro

* A chave `.pem` foi copiada para a Bastion via SCP:

  ```bash
  scp -i lab-key-bastion.pem lab-key-bastion.pem ec2-user@<IP-BASTION>:/tmp/
  ```
* Dentro da Bastion:

  ```bash
  mv /tmp/lab-key-bastion.pem ~/ && chmod 400 ~/lab-key-bastion.pem
  ssh -i ~/lab-key-bastion.pem ec2-user@<IP-PRIVADO-BACKEND>
  ```

---

## ⚠️ Pontos de Atenção e Cuidados

### 💸 Sobre cobranças

* **NAT Gateway cobra por hora ativa**, mesmo sem tráfego.
* **Elastic IP cobra** se estiver **alocado e não vinculado**.
* EC2s fora do Free Tier ou ligadas o tempo todo também geram custos.

### 🧯 Sobre erros comuns

* Sub-rede pública sem rota para o IGW → sem acesso externo.
* Backend com IP público ativado → expõe indevidamente o servidor.
* DNS Hostnames desabilitados na VPC → impede resolução e acesso.
* SG configurado com `0.0.0.0/0` em ambiente privado → risco de segurança.
* Faltou copiar a chave `.pem` para a Bastion → sem acesso à Backend.

---

## ✅ Testes realizados com sucesso

* [x] Acesso externo via SSH à Bastion EC2
* [x] Acesso interno via SSH à Backend EC2
* [x] Chave copiada com segurança via SCP
* [x] Segurança validada entre Security Groups
* [x] Comunicação de saída da sub-rede privada via NAT Gateway

---

## 📚 Conclusão

Este laboratório representa um modelo prático e didático de infraestrutura segura em nuvem. A criação manual de cada recurso ajudou a compreender as dependências e relações entre VPC, sub-redes, roteamento, segurança e conectividade.

Essa base é essencial para ambientes de produção, certificações (como AWS CCP ou SAA) e futuros projetos com automação via Terraform ou AWS CLI.

---
