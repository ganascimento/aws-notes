# 📬 SQS - Simple Queue Service

O AWS SQS é um serviço de filas de mensagens totalmente gerenciado. Ele permite que sistemas diferentes se comuniquem de forma assíncrona, desacoplando produtores e consumidores.

Basicamente, ele serve para armazenar mensagens temporariamente até que algum sistema esteja pronto para processá-las.

## 🧩 Conceitos principais

### 📦 Fila

- Uma fila SQS é como uma “caixa de mensagens”.
- Produtores colocam mensagens na fila.
- Consumidores retiram mensagens da fila para processá-las.
- Você pode ter uma ou várias filas dependendo do fluxo de trabalho.

### ✉️ Mensagens

- Podem conter até 256 KB de dados.
- Mensagens são armazenadas de forma temporária, padrão é até 4 dias (máximo configurable 14 dias).

### 🗂️ Tipos de fila

- Standard Queue
  - Entrega pelo menos uma vez (pode duplicar).
  - Entrega não garante ordem das mensagens.
  - Alta taxa de throughput (milhões/mensagens por segundo).

- FIFO Queue (First-In-First-Out)
  - Entrega exatamente uma vez (sem duplicatas).
  - Mantém ordem exata das mensagens.
  - Limite de throughput menor que Standard.

## ⚙️ Como funciona

- Um sistema (produtor) envia mensagens para a fila SQS.
- A fila armazenará essas mensagens até que sejam processadas.
- Outro sistema (consumidor) lê e processa as mensagens, podendo excluí-las após o processamento.
- O consumidor pode processar mensagens em paralelo, escalando conforme necessário.

Isso cria um modelo desacoplado e resiliente, porque se o consumidor ficar offline, a fila mantém as mensagens até ele voltar.

## 📚 Casos de uso comuns

- Processamento assíncrono de tarefas: uploads, relatórios, cálculos pesados.
- Desacoplamento de microserviços: sistemas diferentes podem enviar e receber dados sem depender do outro estar ativo.
- Controle de fluxo: evitar sobrecarga em sistemas de backend, processando mensagens de forma controlada.
- Garantia de entrega: especialmente usando FIFO, garantindo que nada se perca ou chegue duplicado.