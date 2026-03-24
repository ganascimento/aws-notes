# 📧 SES (Simple Email Service)

O AWS SES é um serviço de envio e recebimento de emails escalável e gerenciado. Ele permite que aplicações enviem emails de forma confiável sem precisar configurar servidores de email próprios.

Você pode usar para:
- Enviar notificações para usuários
- Enviar newsletters ou campanhas de marketing
- Receber emails de usuários e processá-los automaticamente

## 🧩 Conceitos principais

### 🆔 Identidades

- Antes de enviar emails, você deve verificar quem envia os emails.
- Tipos de identidades:
  - Domínios: ex. meusite.com
  - Endereços de email específicos: ex. contato@meusite.com
- A verificação garante que você é o dono do endereço ou domínio e evita problemas de spam.

### ✉️ Envio de emails

Pode ser feito de três formas:
- SMTP: conectando-se ao SES como um servidor SMTP
- API da AWS: usando SDKs (C#, Python, etc.)
- AWS CLI: via linha de comando

### 📥 Recebimento de emails

SES também permite receber emails, processá-los e armazená-los em:
- S3 (armazenamento)
- Lambda (processamento automático)
- SNS (notificação de chegada de email)

### 🏖️ Sandbox vs Produção

- Por padrão, ao criar uma conta SES você começa no modo sandbox, que tem limitações:
  - Só pode enviar emails para endereços verificados
  - Limite de envio diário e por segundo
- Para enviar emails para qualquer destinatário, você precisa solicitar saída da sandbox.

## ⚙️ Como funciona

- Verifique um domínio ou email remetente.
- Configure autenticação e políticas (DKIM, SPF, DMARC) para evitar que emails caiam em spam.
- Envie emails via API, SMTP ou CLI.
- Opcional: receba emails e processe automaticamente via S3, Lambda ou SNS.

SES garante alta taxa de entrega e escalabilidade sem precisar gerenciar servidores de email.

## 📚 Casos de uso comuns

- Notificações de aplicativos: reset de senha, confirmação de cadastro, alertas de sistema.
- Campanhas de marketing: newsletters para clientes.
- Processamento automático: receber emails de usuários e disparar workflows.
- Integração com outros serviços AWS: SNS, Lambda, S3, etc.