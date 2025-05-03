# 📘 Apostila Técnica - Lab 1: EC2 (Início)

## 🎯 Objetivo

Criar uma instância EC2 Linux gratuita usando o Free Tier da AWS, acessar via SSH com segurança e explorar o ambiente de servidor como parte da formação técnica em AWS Cloud Foundations.

---

## 🧭 Etapas Realizadas

### 1. Acesso ao Console AWS

* URL: [https://aws.amazon.com/console/](https://aws.amazon.com/console/)
* Login realizado com conta Free Tier.

### 2. Navegação até EC2

* No Console AWS, clicar em **"EC2"** para gerenciar instâncias.

### 3. Criação da Instância

* **Nome da instância:** `MeuPrimeiroServidor`
* **AMI escolhida:** Amazon Linux 2023 (base Fedora)
* **Tipo de instância:** t2.micro (Free Tier)

### 4. Key Pair (Chave SSH)

* Criada nova chave:

  * Nome: `meu-primeiro-keypair`
  * Tipo: RSA
  * Formato: `.pem`
* Chave salva localmente e protegida com:

```bash
chmod 400 meu-primeiro-keypair.pem
```

### 5. Configuração de Rede

* VPC: default (`vpc-02bbcb855a153d832`)
* Subnet: default, sem preferência de zona de disponibilidade
* IP público: habilitado (Auto-assign Public IP: Enable)

### 6. Security Group (Firewall)

* Criado grupo liberando apenas:

  * **SSH (porta 22)** do IP local

### 7. Armazenamento (Disco)

* Volume padrão: 8 GB SSD (incluso no Free Tier)

### 8. Finalização e Lançamento

* Instância criada com sucesso
* Acompanhado o status até `running`

### 9. Conexão via SSH

Comando usado:

```bash
ssh -i meu-primeiro-keypair.pem ec2-user@<IP_PÚBLICO>
```

* Confirmado login como `ec2-user`

---

## 🔍 Exploração da Instância EC2

### Comandos executados:

```bash
uname -a                        # Ver informações do kernel
cat /etc/os-release             # Ver base do sistema (Amazon Linux baseado em Fedora)
df -h                           # Ver espaço em disco
free -h                         # Ver memória RAM
w                               # Ver usuários conectados e uptime
```

### Atualização do sistema:

```bash
sudo dnf update -y
```

### Instalação do monitor de processos:

```bash
sudo dnf install htop -y
htop                            # Rodando o monitor
```

### Verificação de rede e IP:

```bash
hostname -I                    # Mostra IP interno
curl http://169.254.169.254/latest/meta-data/public-ipv4  # Tenta obter IP público
ip a                           # Detalha interfaces de rede
```

---

## ⚠️ Pontos de Atenção

* Se não baixar a chave `.pem` na hora da criação da Key Pair, **não será possível acessá-la depois**.
* O IP retornado por `hostname -I` é **privado** (VPC). Para ver o público, use o painel da AWS ou `curl`.
* Se o firewall local do seu Linux bloquear porta 22, será necessário liberar (via `ufw`, `iptables`, etc).
* Toda instância EC2 **sem IP público** não é acessível via internet externa (exceto se usar NAT, Bastion ou Elastic IP).
* A desconexão automática por inatividade SSH é comum. Pode ser ajustada com KeepAlive.

---

## ✅ Resultados

* Instância EC2 criada com segurança.
* Acesso via SSH realizado.
* Comandos básicos de exploração executados.
* Ambiente pronto para uso em Labs futuros (como servidor web, banco de dados, etc).

---

## 📌 Recomendações Finais

* Sempre organize suas chaves em uma pasta protegida, ex: `~/.ssh/`
* Desligue instâncias não utilizadas para evitar cobranças fora do Free Tier
* Registre os passos de cada laboratório como esse documento para fins de estudo e portfólio técnico

---

**Fim da Apostila - Lab 1: EC2 (Início)**
