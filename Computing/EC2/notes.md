# EC2 (Elastic Comput Cloud)

É um serviço de aluguel de servidores virtuais

### Casos de uso

- Hospedagem de WebSite
- Hospedagem de WebAPI
- Servidor de banco de dados
- Criar instancia para testes
- IA - Machine Learning
- Jogos Online

### Escalabilidade

Capacidade de crescer ou reduzir os recursos conforme a demanda, tanto horizontalmente como verticalmente.

### Elasticidade

Ajusta o recurso conforme a demanda, ele usa a escalabilidade mas faz isto de forma automática, sem a necessidade de intervenção manual, ou seja, durante os picos do dia, o servidor criar instâncias ou aumenta os recursos (memória, disco, CPU) e também diminui caso a demanda diminua.

# Tipos de EC2

[Clique aqui para ver os tipos de instancia do EC2](https://aws.amazon.com/pt/ec2/instance-types/)

### General Propose

São aplicações comuns, websites, webapis, repositório de código

### Compute optimized

Quando é necessário um alto uso de cpu

### Optimized to memory

Que necessita de muita memória, que usa muita RAM

### Accelerated computing

Muito utilizada para machine learning, pois contém GPU

### Optimized for storage

Utilizada para banco de dados, pois tem um acesso a disco muito rapido

### Optimized for HPC

Com largura de banda muita alta

# Tipos de pagamento

[Clique aqui para ir para calculadora do EC2 por demanda](https://aws.amazon.com/pt/ec2/pricing/on-demand/)

### On-Demand

- Paga por hora ou segundo (dependendo do SO) sem compromisso.
- Mais caro, mas flexível.
- Bom para workloads imprevisíveis ou de teste/desenvolvimento.

### Savings Plans

- Você se compromete a gastar um valor fixo ($/hora) em EC2 por 1 ou 3 anos.
- Até 72% mais barato que On-Demand.
- Mais flexível que Reserved Instances porque se aplica a qualquer região, instância ou família compatível (dependendo do tipo de plano).
- Bom para workloads estáveis e de longo prazo.

### Spot Instances

- Usa capacidade ociosa da AWS com até 90% de desconto.
- Pode ser interrompida a qualquer momento pela AWS (com aviso de 2 minutos).
- Excelente para workloads flexíveis/fault-tolerant, como:
  - Big Data
  - Batch jobs
  - Treinamento de Machine Learning
  - Processamento paralelo

# Security Groups

É um fireall para as instâncias

É stateful sempre:

- Permite automaticamente as respostas

Se fosse um stateless (não tem opção de se tornar stateless):

- Teria que criar regras para saída
