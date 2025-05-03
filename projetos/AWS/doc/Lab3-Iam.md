
# Lab 3 – IAM: Controle de Acesso na AWS

## 🎯 Objetivo
Aprender e praticar a criação de usuários IAM, grupos, políticas personalizadas e aplicar o Princípio do Menor Privilégio.

## ✅ Etapas Realizadas

### 1. Criação de Grupos IAM
- **Admins**: com política `AdministratorAccess`
- **DevOps**: com política `PowerUserAccess`
- **Leitores**: com política `ReadOnlyAccess`
- **Estagiarios**: com política personalizada de leitura S3

### 2. Criação de Usuários IAM
- `admin-user`
- `devops-user`
- `leitor-user`
- `estagiario-user`
- `auditor-user` (acesso programático)

### 3. Políticas Criadas
#### 🔸 Política: `S3ReadOnlyMeuBucketEstagio`
Permite apenas leitura e listagem no bucket `meu-bucket-estagio`.

#### 🔸 Política: `S3ListAllBucketsOnly`
Permite listar todos os buckets no painel AWS (usado por `estagiario-user`).

#### 🔸 Política: `AuditorPolicy`
Permite leitura nos serviços EC2, S3 e IAM.

### 4. Acesso Programático
- Criado usuário `auditor-user` sem acesso ao Console.
- Geradas credenciais via Access Key + Secret Key.
- Configurado perfil CLI com `aws configure --profile auditor`.

### 5. Testes Realizados via AWS CLI
```bash
aws s3 ls --profile auditor
aws ec2 describe-instances --profile auditor
aws iam list-users --profile auditor
```

## 🧪 Resultados Esperados
- Usuários com permissões restritas e organizadas por grupos.
- `estagiario-user` acessa somente um bucket.
- `auditor-user` executa leitura por CLI sem acesso ao console.
- Nenhum usuário fora dos grupos pode modificar recursos indevidamente.

## 🧱 Conhecimentos Desenvolvidos
- IAM: usuários, grupos e políticas
- Políticas JSON personalizadas
- Access Key vs Console Access
- Princípio do Menor Privilégio
- AWS CLI: perfis, comandos e autenticação

---

📁 *Este laboratório integra o projeto Formação Técnica AWS Cloud Foundations.*
