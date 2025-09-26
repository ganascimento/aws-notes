# 💽 S3

É um serviço de armazenamento de arquivos.

Ele é pay-as-you-go (paga conforme o uso)

[Clique aqui para ver a calculadora](https://calculator.aws/#/createCalculator/S3)

## 🗄️ Bucket

### Modos

- **General Purpose:** Maioria dos casos, armazenar arquivos em várias regiões para propósitos gerais

- **Directory:** Usado para baixa latencia, por exemplo para jogos online

### Estrutura

- Bucket
- Objetos (arquivos)
- Key: caminho + nome do objeto
- Region: O local onde o bucket está hospedado fisicamente

<br>

# 🗂️ Classes de armazenamento

| Classe                        | Durabilidade  | Disponibilidade | Recuperação   | Uso recomendado                         | Cobrança por recuperação/eliminação | Custo por GB (USD, aprox.)      |
| ----------------------------- | ------------- | --------------- | ------------- | --------------------------------------- | ----------------------------------- | ------------------------------- |
| S3 Standard                   | 99,999999999% | 99,99%          | Imediata      | Dados acessados com frequência          | Não                                 | $0.025                          |
| S3 Intelligent-Tiering        | 99,999999999% | 99,9% - 99,99%  | Imediata      | Dados com padrões de acesso variáveis   | Não                                 | $0.025 (frequente), $0.015 (IA) |
| S3 Standard-IA                | 99,999999999% | 99,9%           | Imediata      | Dados acessados raramente               | Sim                                 | $0.014                          |
| S3 One Zone-IA                | 99,999999999% | 99,5%           | Imediata      | Dados raros, tolerantes a perda de zona | Sim                                 | $0.011                          |
| S3 Glacier Instant Retrieval  | 99,999999999% | 99,9%           | Imediata      | Arquivos raros, acesso rápido           | Sim                                 | $0.005                          |
| S3 Glacier Flexible Retrieval | 99,999999999% | 99,99%          | Minutos-horas | Arquivamento, acesso eventual           | Sim                                 | $0.004                          |
| S3 Glacier Deep Archive       | 99,999999999% | 99,99%          | Horas         | Arquivamento de longo prazo             | Sim                                 | $0.0015                         |

### S3 Standard

- **Quando usar?** Para arquivos usados com frequência.
- **Exemplo:** Um site de e-commerce que armazena imagens de produtos.

### S3 Intelligent-Tiering

- **Quando usar?** Quando você não sabe com que frequência os dados serão
  acessados.
- **Exemplo:** Um app de fotos onde algumas imagens são acessadas todos os dias e
  outras quase nunca.

### S3 Standard-IA

- **Quando usar?** Dados que você precisa guardar por segurança, mas acessa
  raramente.
- **Exemplo:** Backups de banco de dados feitos semanalmente.

### S3 One Zone-IA

- **Quando usar?** Quando você pode recriar os dados, se perdê-los.
- **Exemplo:** Arquivos temporários de exportações de relatórios que podem ser
  regenerados.

### S3 Glacier Instant Retrieval

- **Quando usar?** Arquivos antigos, mas que podem ser acessados instantaneamente.
- **Exemplo:** Relatórios de vendas antigos que podem ser consultados pelo time
  financeiro.

### S3 Glacier Flexible Retrieval

- **Quando usar?** Arquivos que quase nunca são acessados, mas precisam ser
  mantidos.
- **Exemplo:** Arquivos legais que precisam ser armazenados por anos.

### S3 Glacier Deep Archive

- **Quando usar?** Para arquivamento de longo prazo com baixo custo.
- **Exemplo:** Arquivos de auditorias anuais que devem ser guardados por 10 anos

### Observação

A transferência entre classes também é paga

<br>

# 🚨 Permissões

Para liberar um acesso publico não basta somente liberar o acesso através do **Block public access (bucket settings)**, também é necessário adicionar uma police, exemplo:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowAllReadWrite",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": ["arn:aws:s3:::NOME_DO_BUCKET/*"]
    }
  ]
}
```

<br>

# ✨ Versionamento

Permite manter várias versões do mesmo objeto (arquivo)

- Deletar: vai esconder o arquivo (marker)

Para habilitar depois de criada é em **Properties** > **Bucket Versioning**

Por exemplo ao deletar um arquivo, ele fica com a **Delete marker**, e ao habilitar **Show versions** é exibido todas versões do arquivo.

Se subir um arquivo com o mesmo nome, ele também versiona

Obs.: Por exemplo, se eu subir 3 versões diferentes de um mesmo arquivo, eu vou pagar triplicado por ele, pois ele vai consumir o espaço dos 3 arquivos somados

<br>

# ❤️‍🔥 Lifecycle configuration

Criar regras para os arquivos do bucket, por exemplo:

- É possível por exemplo remover arquivos depois de X dias
- Mover arquivos grandes para um bucket com uma classe mais barata

<br>

# ✉️ Event Notification

Possibilidade de chamar trigger quando certos eventos ocorrem dentro do bucket, eventos como:

- Chegar um arquivo
- Copiar um arquivo
- Deletar um arquivo

E os eventos que podem ser disparados são:

- Lambda
- SNS
- SQS

<br>

# 🗃️ Replicação (Replication)

Usado por exemplo para diminuir a latência, caso eu tenha um bucket q está em us-east-1 e tenho usuários de UK acessando, a latência é maior para esses usuários, então eu posso replicar este bucket, neste caso seria uma replicação CRR.

- CRR (Cross-Region Replication)
- SRR (Same-Region Replication)

Para configurar vá em **Management** > **Replication rules**

É possível criar regras de filtro para por exemplo não replicar arquivos .mp4

Quando replica entre regiões (CRR) ele cria um job para fazer este processo

<br>

# 🚫 Encryption

Todos objetos são encriptados

## Tipos de criptografia:

### Em repouso

Quando o objeto está na bucket

- **SSE-S3:** a chave de criptografia é gerenciada pela AWS
- **SSE-KMS:** a chave de criptografia é gerenciada pelo serviço da AWS (KMS)
- **DSSE-KMS**: a chave de criptografia é gerenciada pelo cliente

### Em trânsito

Quando o objeto está em processo de upload/download/read/write

- **HTTPS:** é habilitada por padrão da web

<br>

# 📼 Storage Gateway

É um serviço da AWS que permite integrar o armazenamento local (on-premises) da sua empresa com a nuvem da AWS de forma transparente. Ele age como uma ponte entre seu data center local e os serviços de armazenamento da AWS, como S3, Glacier e EBS.

Basicamente, ele facilita o uso da nuvem sem precisar mover imediatamente todos os dados ou mudar totalmente sua infraestrutura local. Ele pode ser usado para backup, arquivamento, migração de dados e disaster recovery.

Existem três tipos principais de Storage Gateway:

### File Gateway (NFS/SMB)

- Permite que você acesse o Amazon S3 como se fosse um compartilhamento de arquivos local.
- Arquivos salvos no gateway vão automaticamente para o S3, mantendo metadados locais.

### Volume Gateway (iSCSI)

- Fornece volumes de blocos que podem ser montados em servidores locais via iSCSI.
- Existem dois modos:
  - **Cached Volumes:** mantém uma cópia local em cache e todo o restante no S3.
  - **Stored Volumes:** mantém todos os dados localmente e faz backup incremental para o S3.

### Tape Gateway (Virtual Tape Library)

- Integração transparente com a nuvem.
- Redução de custos com armazenamento em fitas ou discos locais.
- Backup e recuperação mais rápidos e escaláveis.
- Suporte a aplicações existentes sem grandes mudanças.

<br>

# ❄️ SnowFamily

É uma família de dispositivos e serviços da AWS voltados para transferência e processamento de dados em larga escala, especialmente em ambientes onde a conectividade com a internet é limitada ou muito lenta. Ou seja, quando você tem grandes volumes de dados e não consegue enviá-los facilmente pela rede, a AWS oferece esses dispositivos físicos que você leva até o seu data center, carrega os dados e depois envia para a AWS.

### AWS Snowcone

- Menor dispositivo da família, portátil (menos de 5 kg).
- Armazenamento de até 8 TB.
- Pode executar computação local limitada, usando AWS IoT ou Lambda.
- Ideal para ambientes remotos, edge computing ou pequenas cargas de dados.

### AWS Snowball

- Dispositivo físico maior que o Snowcone.
- Armazenamento de 50 TB ou 80 TB por dispositivo.
- Usado para mover grandes volumes de dados para dentro ou fora da AWS.
- Suporta criptografia de ponta a ponta e integração com S3.
- Pode rodar alguma computação local, por exemplo, processamento prévio dos dados antes de enviar.

### AWS Snowmobile

- Um caminhão inteiro equipado para transferir dados em exabytes.
- Usado por empresas com quantidades massivas de dados, como data centers inteiros ou arquivos históricos gigantescos.
- Transporte físico seguro com criptografia e monitoramento da AWS.

<br>

# 💸 S3 Requester Pays

É uma configuração de bucket do Amazon S3 onde quem faz o download (o requester) paga pelos custos de requisição e transferência de dados, em vez do dono do bucket (o bucket owner).

Acesso através de **Properties** > **Requester Pays**

### Importante

- Não funciona para acesso anônimo → o requester precisa ter conta AWS e estar autenticado com IAM.
- Útil em cenários de open data → ex.: você publica um dataset de 10 TB, mas cada usuário que quiser baixar paga o tráfego.
- O bucket não pode ser configurado como website estático se tiver Requester Pays ativado.
- O requester deve usar a flag x-amz-request-payer nos requests.
