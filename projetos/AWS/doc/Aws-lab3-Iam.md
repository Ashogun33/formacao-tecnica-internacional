
# Apostila Técnica – Lab 3: IAM (Controle de Acesso na AWS)

## 🎯 Objetivo do Laboratório
Este laboratório teve como foco aprender a configurar o serviço IAM da AWS para controle de acesso com segurança e organização. Foram criados grupos, usuários, políticas e perfis de acesso com base no princípio do menor privilégio.

---

## 🛠️ Etapas Práticas Realizadas

### 1. Criação de Grupos IAM
- **Admins**: com política `AdministratorAccess`
- **DevOps**: com política `PowerUserAccess`
- **Leitores**: com política `ReadOnlyAccess`
- **Estagiarios**: com política personalizada para leitura em um bucket específico

### 2. Criação de Usuários
- `admin-user`, `devops-user`, `leitor-user`, `estagiario-user`, `auditor-user`
- Usuários adicionados a seus respectivos grupos
- `auditor-user` criado **sem acesso ao console** e com **acesso programático**

### 3. Políticas Personalizadas Criadas

#### 🔸 Política: `S3ReadOnlyMeuBucketEstagio`
Permite ao usuário acessar apenas o bucket `meu-bucket-estagio` com ações de leitura:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:GetObject", "s3:ListBucket"],
      "Resource": [
        "arn:aws:s3:::meu-bucket-estagio",
        "arn:aws:s3:::meu-bucket-estagio/*"
      ]
    }
  ]
}
```

#### 🔸 Política: `S3ListAllBucketsOnly`
Permite listar todos os buckets no Console Web:

```
{
  "Effect": "Allow",
  "Action": "s3:ListAllMyBuckets",
  "Resource": "*"
}
```

#### 🔸 Política: `AuditorPolicy`
Permite apenas leitura nos serviços EC2, S3 e IAM:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeInstances",
        "ec2:DescribeVolumes",
        "ec2:DescribeSnapshots",
        "s3:ListAllMyBuckets",
        "s3:ListBucket",
        "s3:GetObject",
        "iam:ListUsers",
        "iam:ListGroups",
        "iam:ListRoles",
        "iam:ListPolicies"
      ],
      "Resource": "*"
    }
  ]
}
```

---

## ⚠️ Pontos de Atenção Importantes

- ❗ Não usar **IAM Identity Center** para este laboratório (pode gerar custos e complicações desnecessárias)
- ❗ Sempre configurar **Bucket Policy** quando estiver usando **Object Ownership: Bucket owner enforced**
- ❗ Usuários com apenas `s3:GetObject` e `s3:ListBucket` não conseguem usar o console S3 sem também ter `s3:ListAllMyBuckets`
- ❗ As `Access Keys` só aparecem uma vez – **salve imediatamente**
- ❗ Região padrão precisa estar correta (ex: `us-east-2`). Nunca use `"global"` no `aws configure`

---

## 💻 AWS CLI – Testes Realizados

Após configurar o perfil `auditor` com `aws configure --profile auditor`, foram realizados testes com os seguintes comandos:

```bash
aws s3 ls --profile auditor
aws ec2 describe-instances --profile auditor
aws iam list-users --profile auditor
```

Todos retornaram resultados com sucesso, confirmando que a política de leitura estava funcionando corretamente.

---

## 📘 Conhecimentos Consolidadores

- IAM: Usuários, Grupos, Políticas, Privilégios
- IAM Policy em JSON
- Bucket Policy vs IAM Policy
- Princípio do Menor Privilégio
- Configuração de perfis com AWS CLI
- Testes práticos com `describe-instances`, `list-users`, `s3 ls`

---

📁 *Este conteúdo integra o projeto “Formação Técnica AWS Cloud Foundations”. Pode ser consultado como referência futura para projetos com segurança na AWS.*
