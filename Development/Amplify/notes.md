# AWS Amplify

É um conjunto de ferramentas e serviços da AWS que ajuda desenvolvedores a criar, configurar e implantar aplicações web e mobile full-stack de forma simples e rápida.

## 🔑 O que ele faz

- Hospedagem e Deploy

  - Faz deploy automático de apps web (React, Angular, Vue, Next.js, etc.) conectando direto ao GitHub, GitLab ou CodeCommit.
  - Oferece CI/CD integrado para cada git push.

- Backend-as-a-Service

  - Permite criar backends sem precisar configurar manualmente todos os serviços AWS:

    - **Autenticação** → via Amazon Cognito.
    - **API REST/GraphQL** → via API Gateway ou AppSync.
    - **Banco de dados** → via DynamoDB ou Aurora Serverless.
    - **Storage de arquivos** → via Amazon S3.

- SDKs e Bibliotecas

  - Fornece bibliotecas para web e mobile que já sabem conversar com a AWS (login, upload de arquivos, requisições GraphQL/REST etc.).

- Interface Low-Code (Admin UI)

  - Permite configurar backends e gerenciar usuários, permissões, schemas de dados etc. sem precisar escrever CloudFormation ou Terraform.

## 🚀 Exemplo prático

- Você quer criar um app em React para cadastrar usuários e permitir upload de fotos.
- Com Amplify:
  - Cria o projeto no Amplify.
  - Adiciona auth (Cognito) e storage (S3).
  - Usa a lib do Amplify no React para login e upload.
  - Faz deploy com um clique → seu app fica disponível em uma URL do Amplify Hosting.

## 📌 Resumindo

O AWS Amplify é como um atalho para devs que não querem perder tempo montando toda a infraestrutura na mão. Ele junta vários serviços AWS (Cognito, AppSync, DynamoDB, S3, etc.) em um fluxo simples, com SDKs, CLIs e hospedagem pronta.
