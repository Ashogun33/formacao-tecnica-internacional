# Controle de Usuários, Grupos e Permissões — Prática Linux Essentials

## 📅 Data
Abril de 2025

## 🎯 Objetivos
- Criar usuários e grupos no sistema Linux.
- Configurar diretórios privados e compartilhados com controle de acesso.
- Gerenciar permissões usando `chmod` e `chown`.
- Diagnosticar e corrigir problemas de acesso.
- Executar rollback completo (remoção segura de usuários, grupos e pastas).
- Validar segurança do sistema após alterações.

## 🛠️ Ações Realizadas

1. **Criação de usuários**:  
   - `user01`
   - `user02`
   - `user03`

2. **Criação de grupos**:  
   - `grupo_dev`
   - `grupo_doc`

3. **Atribuições de grupo**:
   - `user01` e `user02` adicionados ao `grupo_dev`.
   - `user03` adicionado ao `grupo_doc`.

4. **Criação de diretórios**:
   - `caminho/diretorio/dev` para o grupo `grupo_dev`.
   - `caminho/diretorio/doc` para o grupo `grupo_doc`.

5. **Configuração de permissões**:
   - Dono: `root`
   - Grupo: `grupo_dev` ou `grupo_doc`
   - Permissões: `rwxrwx---` (`770`)

6. **Ajustes de travessia**:
   - Adicionado permissão de execução (`o+x`) temporariamente no `caminho/diretorio/` para permitir acesso aos diretórios internos.

7. **Testes de operação**:
   - Usuários testaram criação de arquivos em seus respectivos diretórios.
   - Confirmação de restrição correta em diretórios alheios.

8. **Rollback**:
   - Remoção de usuários e seus respectivos diretórios pessoais.
   - Remoção dos grupos criados.
   - Remoção dos diretórios `dev` e `doc`.
   - Restauração das permissões originais do diretório base para `700`.
   - Verificação final de segurança e limpeza.

## 📋 Comandos principais utilizados

```bash
useradd -m -s /bin/bash user01
groupadd grupo_dev
usermod -aG grupo_dev user01
mkdir caminho/diretorio/dev
chown root:grupo_dev caminho/diretorio/dev
chmod 770 caminho/diretorio/dev
chmod o+x caminho/diretorio
touch arquivo.txt
userdel -r user01
groupdel grupo_dev
rm -r caminho/diretorio/dev
chmod 700 caminho/diretorio
