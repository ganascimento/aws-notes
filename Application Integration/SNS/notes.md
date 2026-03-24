# 📣 SNS - Simple Notification Service

O AWS SNS é um serviço de mensagens que permite enviar notificações de forma pub/sub (publicação/assinatura) ou mensagens diretas para vários destinatários. Ele é serverless, ou seja, você não precisa se preocupar em gerenciar servidores.

Basicamente, ele serve para entregar mensagens rapidamente para múltiplos sistemas ou usuários, como:

- Enviar alertas para administradores (via email ou SMS)
- Notificar microserviços quando um evento acontece
- Acionar funções Lambda automaticamente
- Integrar sistemas internos e externos

## 🧩 Conceitos principais

### 📝 Tópicos

- Um tópico SNS é um canal de comunicação.
- Publicadores enviam mensagens para o tópico.
- Assinantes recebem as mensagens desse tópico.

### 🔔 Assinaturas

Você pode adicionar assinantes a um tópico. Exemplos:
- Email
- SMS
- AWS Lambda
- SQS (Simple Queue Service)
- HTTP/HTTPS endpoint

### ✉️ Mensagens

- Mensagens podem ser texto simples ou JSON estruturado.
- Cada assinatura recebe a mensagem enviada ao tópico.

## ⚙️ Como funciona

- Um serviço ou aplicativo publica uma mensagem em um tópico SNS.
- O SNS distribui essa mensagem para todos os assinantes.
- Cada assinante recebe a mensagem no seu canal (email, SMS, Lambda, etc.).

Isso cria um modelo pub/sub desacoplado, onde o produtor e consumidor não precisam se conhecer diretamente.

## 📚 Casos de uso comuns

- Notificações de aplicativos: alertar usuários sobre eventos (ex: entrega de pedido, atualização de status).
- Monitoramento e alertas: enviar mensagens quando métricas da AWS CloudWatch atingem limites críticos.
- Integração de microserviços: quando um serviço publica eventos que outros precisam processar.
- Trigger para Lambda: processar eventos automaticamente sem polling.