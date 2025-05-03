# 💻 Lab 1 – EC2 (Início)

## 🎯 Objetivo

Criar uma instância EC2 Linux gratuita utilizando o Free Tier da AWS, acessá-la com segurança via SSH e realizar exploração básica do ambiente de servidor.

## 📦 Etapas Realizadas

* Criação da instância t2.micro com Amazon Linux 2023
* Geração de chave SSH (.pem) e configuração de permissões com `chmod 400`
* Configuração de rede padrão e liberação da porta SSH (22) apenas para o IP local
* Conexão bem-sucedida via SSH com `ec2-user`
* Exploração do sistema com comandos básicos: `uname`, `df`, `htop`, `cat /etc/os-release`
* Atualização do sistema com `dnf update`
* Instalação do `htop` para monitoramento em tempo real

## ⚠️ Cuidados Importantes

* Salve a chave `.pem` com segurança — não há como baixá-la novamente!
* IP retornado por `hostname -I` é privado; use o painel AWS ou metadata para consultar o IP público.
* Verifique se o firewall local (ex: UFW) permite conexões de saída pela porta 22.

## 📘 Apostila Completa

Consulte a apostila técnica detalhada deste laboratório com todos os comandos e pontos de atenção:

👉 `Lab1_EC2_Inicio.md`

---

**Parte da Formação Técnica – AWS Cloud Foundations**
