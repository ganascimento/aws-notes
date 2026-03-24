# ⚡ Lambda

O AWS Lambda é um serviço de computação serverless, ou seja, você executa código sem precisar gerenciar servidores.

- Você paga apenas pelo tempo que o código é executado e pela quantidade de invocações.
- Ele é ideal para microserviços, automações, processamento de eventos e integração de sistemas.

Em resumo: Lambda é um computador virtual que só liga quando você precisa, e desliga automaticamente após executar o código.

## 🧩 Conceitos principais

### 📝 Função Lambda

- A unidade de execução do Lambda é a função Lambda.
- Cada função contém:
  - Código (Python, C#, Node.js, Java, Go, Ruby…)
  - Configurações (memória, timeout, variáveis de ambiente, IAM role)

### ⏩ Triggers (gatilhos)

Lambda não fica “rodando” constantemente, mas é invocado por eventos, por exemplo:

- **S3** → quando um arquivo é enviado
- **DynamoDB** → quando há uma mudança na tabela
- **API Gateway** → quando uma requisição HTTP chega
- **CloudWatch** → para agendar tarefas (cron)
- **SNS/SQS** → quando uma mensagem chega

### 🛡️ Execution Role (IAM)

- Cada Lambda precisa de uma Role IAM que define permissões para acessar outros serviços AWS.
- **Exemplo:** permitir que a Lambda grave logs no CloudWatch ou leia arquivos no S3.

### ☁️ Conceito de Serverless

- Lambda não tem servidor dedicado.
- Escala automaticamente conforme a demanda, criando múltiplas instâncias da função se necessário.
- Tempo máximo de execução por invocação: 15 minutos.

## ⚙️ Como funciona

- Um evento dispara a função Lambda.
- Lambda aloca automaticamente recursos (CPU, memória).
- Código é executado em isolamento.
- Resultado é retornado ao invocador ou enviado para outro serviço (SNS, S3, DynamoDB…).

Ciclo de vida da execução:
- **Cold start:** primeira execução da função ou após um período sem uso. Pode demorar alguns segundos.
- **Warm start:** execuções subsequentes usam a mesma instância “quente”, mais rápidas.

## 🔄 Tipos de invocação

| Tipo                | Como funciona                                          | Uso típico                         |
| ------------------- | ------------------------------------------------------ | ---------------------------------- |
| **Síncrona**        | Lambda executa e retorna a resposta imediatamente      | API Gateway, chamadas diretas      |
| **Assíncrona**      | Lambda executa em background, sem bloquear o invocador | SNS, S3, processamento de arquivos |
| **Eventos em lote** | Lambda processa vários registros de uma vez            | SQS, DynamoDB Streams              |

## 📚 Casos de uso comuns

- **API Serverless:** criar APIs usando Lambda + API Gateway.
- **Processamento de arquivos:** resize de imagens, conversão de vídeos quando enviados para S3.
- **ETL (Extração/Transformação/Carregamento):** processar dados de DynamoDB ou S3 e salvar em outro banco.
- **Automação e cron jobs:** usando CloudWatch Events para tarefas periódicas.
- **Integração entre serviços:** por exemplo, SNS envia evento e Lambda processa.

## ✅ Vantagens do Lambda

- **Serverless:** não precisa provisionar nem gerenciar servidores.
- **Escalabilidade automática:** cresce conforme o volume de eventos.
- **Custo sob demanda:** paga apenas pelo tempo de execução.
- **Integração nativa:** funciona com quase todos os serviços AWS.
- **Isolamento e segurança:** cada execução é isolada em containers.

## 🚧 Limitações

- **Tempo máximo por execução:** 15 minutos
- **Memória máxima:** 10 GB
- **Tamanho máximo do pacote de implantação:** 250 MB (zip) / 10 GB (container image)
- Não indicado para workloads longos ou de execução contínua

## 🏅 Boas práticas

- **Funções pequenas e focadas:** cada Lambda deve ter uma responsabilidade única.
- **Evitar dependências pesadas:** reduzir tempo de cold start.
- Usar variáveis de ambiente para configuração e segredos (não codificar no código).
- **Monitoração:** sempre habilitar logs no CloudWatch.
- **IAM mínimo necessário:** aplicar princípio do menor privilégio.
- **Integração com outras filas/serviços:** SNS, SQS, DynamoDB Streams, EventBridge.