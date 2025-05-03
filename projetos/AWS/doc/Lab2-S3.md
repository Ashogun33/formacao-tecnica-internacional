🧾 README.md – Projeto AWS S3: Site Estático
🌐 Sobre este projeto

Este é um exercício prático realizado como parte da Formação Técnica AWS Cloud Foundations, com o objetivo de aprender a utilizar o Amazon S3 para publicação de um site estático gratuito usando a camada Free Tier da AWS.

O site foi inteiramente hospedado no S3 e conta com:

    Página inicial estilizada com HTML + CSS.

    Exibição de imagem.

    Página de erro personalizada (404).

    Segurança ajustada por políticas específicas (sem expor o bucket inteiro).

📌 O que foi feito

    Criação de bucket no S3

        Nome: meu-lab2-s3-aws

        Região: eu-north-1 (Estocolmo)

        Configurado para aceitar acesso público apenas a arquivos específicos.

    Criação do index.html

        Arquivo HTML simples com CSS embutido.

        Mostra uma imagem enviada junto ao bucket.

    Criação do error.html

        Exibe uma mensagem amigável quando o usuário acessa uma página inexistente.

    Configuração do Static Website Hosting

        O bucket foi configurado como servidor estático.

        O index.html foi definido como página inicial.

        O error.html foi configurado como página de erro.

    Definição de política de acesso (Bucket Policy)

        Apenas os arquivos index.html, error.html e a imagem foram tornados públicos.

        Todos os demais arquivos são privados por padrão.

✅ Resultado final

Você pode acessar o site publicado aqui:

🔗 http://meu-lab2-s3-aws.s3-website.eu-north-1.amazonaws.com
📂 Estrutura dos arquivos no bucket

meu-lab2-s3-aws/
├── index.html
├── error.html
└── vivi-2-wallpaper.jpg

💡 O que aprendi com este lab

    Como usar o Amazon S3 para hospedar sites estáticos.

    Diferença entre ACL e Bucket Policy.

    Importância do controle de acesso para manter a segurança.

    Como personalizar a experiência do usuário com páginas de erro.

    Como usar HTML e CSS básico para montar um mini-site funcional.

🚧 Próximos passos

    [ ] Criar mais páginas HTML e adicionar navegação interna.
    [ ] Separar o CSS em um arquivo próprio.
    [ ] Iniciar o Lab 3 – IAM: controle de usuários e permissões na AWS.

🧠 Dica para quem está começando

Mesmo sem servidores, sem backend e sem banco de dados, você já pode publicar seu site profissional na AWS usando apenas o S3. E o melhor: grátis na camada Free Tier.
