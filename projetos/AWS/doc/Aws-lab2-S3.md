📘 Lab 2: Publicação de Site Estático com Amazon S3
🎯 Objetivo

Aprender a utilizar o serviço Amazon S3 para hospedar um site estático completo, incluindo:

    Criação e configuração de bucket.

    Políticas de acesso público.

    Upload de arquivos HTML, imagens e página de erro.

    Ativação do modo Static Website Hosting.

✅ Etapas Realizadas
1. Criar um bucket S3

    Acessar o console da AWS → Serviço S3.

    Criar um bucket com nome único (ex: meu-lab2-s3-aws).

    Região utilizada: eu-north-1 (Estocolmo).

    Desmarcar opção “Block all public access”.

🔎 Ponto de atenção:
A região eu-north-1 não permite o uso de ACLs para liberar objetos manualmente, exigindo uso de Bucket Policies.
2. Upload de arquivos no bucket

    Upload da imagem vivi-1-wallpaper.jpg e, posteriormente, vivi-2-wallpaper.jpg.

    Upload de index.html.

📌 A imagem inicialmente estava na pasta public/, mas foi movida para a raiz do bucket.
3. Criação e configuração de Bucket Policy

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowPublicReadOnlyToWebsiteFiles",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": [
        "arn:aws:s3:::meu-lab2-s3-aws/index.html",
        "arn:aws:s3:::meu-lab2-s3-aws/vivi-2-wallpaper.jpg",
        "arn:aws:s3:::meu-lab2-s3-aws/error.html"
      ]
    }
  ]
}

🔎 Ponto de atenção:
Cada objeto que se deseja tornar público deve estar listado na política, caso o bucket use a configuração "Bucket owner enforced".
4. Criação do index.html

    HTML com CSS interno.

    Inclusão da imagem vivi-2-wallpaper.jpg.

<img src="vivi-2-wallpaper.jpg" alt="Imagem Vivi">

5. Ativação do Static Website Hosting

    Acesso ao bucket → aba Properties.

    Ativação do modo Static Website Hosting.

    Definição do index.html como documento principal.

6. Criação do error.html

    Página de erro personalizada com mensagem 404.

    Upload na raiz do bucket.

    Adição do error.html à Bucket Policy.

    Configuração no campo Error document do hosting.

🔗 Resultado Final

Site acessível publicamente via endpoint gerado pelo S3:

http://meu-lab2-s3-aws.s3-website.eu-north-1.amazonaws.com

📌 Boas práticas reforçadas neste Lab

    Organização de arquivos na raiz.

    Uso correto de políticas públicas com controle específico.

    Configuração mínima e segura (sem liberar o bucket inteiro).

    Personalização de erro 404.

    Publicação real usando AWS Free Tier.

📁 Estrutura final do bucket

meu-lab2-s3-aws/
├── index.html
├── error.html
└── vivi-2-wallpaper.jpg
