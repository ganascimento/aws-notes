# 🔐 IAM (Identity and Access Management)

É o serviço que controla quem pode acessar os recursos da sua conta AWS e o que cada usuário pode fazer. Em outras palavras, ele gerencia identidade e permissões na nuvem da AWS. Vou detalhar de forma organizada:

## 📘 Principais conceitos do IAM

### Usuários (Users)

- Representam pessoas ou serviços que vão acessar sua conta AWS.
- Cada usuário pode ter login para o console da AWS, chaves de API ou ambos.

### Grupos (Groups)

- Coleções de usuários que compartilham as mesmas permissões.
- Permite gerenciar permissões de vários usuários de uma vez.

### Funções (Roles)

- Um conjunto de permissões que não está vinculado a um usuário específico, mas pode ser assumida por usuários, serviços ou instâncias EC2.
- Exemplo: uma instância EC2 que precisa acessar um bucket S3 sem usar chaves de acesso.

### Políticas (Policies)

- São regras que definem quem pode fazer o quê em quais recursos.
- Escrito em JSON, pode ser gerenciado pela AWS ou customizado.
- Exemplo de permissão: `"Allow": "s3:PutObject"` — permite enviar arquivos para um bucket S3.

### Identidade Federada

- Permite que usuários externos (ex: do Google, Active Directory corporativo) acessem a AWS sem criar usuários diretamente.

## ⚙️ Como o IAM funciona na prática

- Cada usuário ou serviço tem permissões explícitas definidas por políticas.
- Por padrão, nenhum usuário tem acesso a recursos até que você conceda.
- Você pode criar políticas muito específicas:
  - Permitir apenas leitura em um bucket S3.
  - Permitir iniciar EC2, mas não deletar instâncias.
- Roles permitem delegar temporariamente permissões para serviços ou contas externas.

## 🚀 Benefícios do IAM

- **Segurança:** você dá apenas o mínimo necessário para cada usuário ou serviço (princípio do menor privilégio).
- **Centralização:** todas as permissões ficam controladas em um só lugar.
- **Flexibilidade:** suporta múltiplos tipos de credenciais e acesso programático.
- **Escalabilidade:** fácil adicionar/remover usuários ou mudar permissões conforme o time cresce.

<br>

# 🛡️ Boas Práticas

- Não utilize o usuário Root
  - Crie uma conta separa para trabalhar com ela
- Crie contas IAM individuais
- Crie Grupos e associe as policies aos grupos
- Permita o mínimo possível
- Utilize primeiro as AWS Manager policies, caso tenha experiência utilize as custom policies
- Habilite o MFA
- Faça revisão do password policies

<br>

# 📌 Pontos importantes

## 📜 Tipos de Políticas

- **Identity-based policies** → ligadas a usuários, grupos ou roles.
- **Resource-based policies** → aplicadas diretamente em recursos (ex: bucket S3).
- Diferença: resource-based permitem acesso cross-account (contas diferentes da AWS).

## 🗂️ Inline vs Managed Policies

- Managed policies: criadas e gerenciadas pela AWS ou pela conta.
- Inline policies: ligadas a um único usuário/grupo/role, não reutilizáveis.

## ⚖️ Ordem de Avaliação

- Explicit Deny sempre vence.
- Permissões só acontecem quando há Allow explícito.

## 🔑 Autenticação

- IAM oferece 3 formas de autenticação:
  - Console (usuário/senha).
  - Programática (Access Key ID + Secret).
  - Federada (SSO, SAML, OIDC).

### Federation

**Federation no IAM significa:** permitir que usuários que não existem dentro do IAM façam login na AWS usando suas credenciais externas.

Ou seja, você não cria um usuário IAM para cada funcionário/usuário. Em vez disso, você confia em uma identidade externa (AD, Google, etc.) e dá acesso temporário via IAM Role + STS.

**📌 Tipos comuns de Federação**:

- AD (Active Directory da empresa)

  - Cenário: empresa já tem usuários no Active Directory (on-premises ou no Azure AD).
  - Em vez de criar usuário IAM para cada funcionário, integra o AD com a AWS.
  - O usuário usa o login corporativo e assume uma IAM Role que dá as permissões.
  - Feito via AWS Directory Service + SAML.

- SAML (Security Assertion Markup Language)

  - Padrão de federação usado em ambientes corporativos.
  - Exemplo: empresa usa Okta, ADFS, Ping Identity para autenticação.
  - Usuário se autentica no IdP → IdP emite um SAML Assertion → AWS confia e deixa o usuário assumir uma Role.

- OIDC (OpenID Connect)

  - Padrão moderno, baseado em OAuth 2.0.
  - Muito usado para aplicações e provedores como Google, Auth0, Cognito, GitHub.
  - Exemplo: um cluster EKS (Kubernetes na AWS) usa OIDC para pods assumirem Roles e acessarem recursos AWS (sem precisar de chaves estáticas).

## 🎭 IAM Role Assumption

- Usuário/serviço assume temporariamente uma role (gera credenciais temporárias do STS).
- Muito usado em:
  - EC2 acessar S3 sem credenciais.
  - Cross-account access.

## 🔍 IAM Access Analyzer

- Ferramenta para verificar se há recursos expostos publicamente ou acessíveis por outras contas.

## 🧪 IAM Policy Simulator

- Ferramenta para testar se uma política realmente concede ou nega a permissão.

## 👑 Root Account

- Só deve ser usado para tarefas críticas (ex: fechar a conta, mudar métodos de pagamento).

## 🔒 MFA

- **Tipos:** virtual MFA (Google Authenticator), hardware MFA, U2F security key.
- Pode ser exigido inclusive em roles (MFA condition).
