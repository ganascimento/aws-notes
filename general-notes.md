# ☁️ Tipos de cloud computing

### Publico

Quando está usando um provedor cloud, exemplo:

- Aws
- Azure

### Privado

Quando mantem o data center próprio, ex:

- Bancos
- Instituições financeiras

### Hibrida

- Quando você tem os dois, parte cloud parte no próprio data center

<br>

# 🌎 Zones

### AZ (Availability Zone)

- **Analogia:** Imagine um supermercado gigante. Cada um tem energia própria, estoque próprio, e se um quebrar, o outro continua funcionando.

- **Definição:** São datacenters independentes dentro de uma mesma Região AWS. Cada região (ex: São Paulo, Virgínia) tem 2 a 6 AZs.

- **Uso:** Alta disponibilidade e tolerância a falhas (colocar servidores em múltiplas AZs garante redundância).

### PoP (Point of Presence)

- **Analogia:** Como se fossem lojinhas menores espalhadas pelo mundo, que ficam perto do cliente, só para entrega rápida de alguns produtos.

- **Definição:** São locais de borda (edge locations) usados para CloudFront (CDN) e Route 53 (DNS).

- **Uso:** Reduz a latência, cache de conteúdo perto do usuário final.

### Local Zones

- **Analogia:** É como se a AWS colocasse um mini-supermercado em cidades menores, para reduzir o tempo de entrega.

- **Definição:** Extensão da Região AWS em locais metropolitanos, trazendo serviços de computação, armazenamento e rede mais perto do usuário.

- **Uso:** Latência ultrabaixa (ex: jogos online, renderização 3D, mídia).

### Wavelength

- **Analogia:** Como se a AWS colocasse uma prateleira de produtos dentro da loja de uma operadora de celular 5G.

- **Definição:** Infraestrutura AWS embutida na rede 5G das teles (ex: Verizon, Vodafone, Claro).

- **Uso:** Aplicações que precisam de latência de 10 ms ou menos, como carros autônomos, AR/VR, IoT crítico.

### Outposts

- **Analogia:** Como se você tivesse uma filial do supermercado AWS dentro da sua própria fábrica.

- **Definição:** Hardware e racks físicos da AWS instalados no datacenter do cliente, mas totalmente gerenciados pela AWS.

- **Uso:** Atender requisitos de regulação, compliance ou latência local (ex: bancos, governo, hospitais).

---

# Comparativo: On-Premises x IaaS x PaaS x SaaS (AWS)

| Característica           | On-Premises (On-Site)                                      | IaaS (Infrastructure as a Service)                     | PaaS (Platform as a Service)                                               | SaaS (Software as a Service)                                                           |
| ------------------------ | ---------------------------------------------------------- | ------------------------------------------------------ | -------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| **Responsabilidade**     | Empresa cuida de tudo                                      | Infraestrutura gerenciada pela AWS, resto pela empresa | Plataforma e infraestrutura pela AWS, empresa foca no app                  | Tudo é gerenciado pela AWS                                                             |
| **Exemplo de Controle**  | Servidores, rede, storage, sistema operacional, aplicações | Configuração de VMs, rede, armazenamento               | Deploy de aplicações, banco de dados, runtime                              | Apenas uso do software                                                                 |
| **Escalabilidade**       | Limitada pela infraestrutura física da empresa             | Alta, ajustável conforme necessidade                   | Alta, com foco em aplicações                                               | Alta, baseada no serviço contratado                                                    |
| **Custos**               | Alto investimento inicial (CAPEX)                          | Custo variável conforme uso (OPEX)                     | Custo variável, pago pelo uso da plataforma                                | Assinatura/licença recorrente                                                          |
| **Velocidade de Deploy** | Lento, depende de aquisição e configuração de hardware     | Rápido, criação de instâncias em minutos               | Muito rápido, deploy automático na plataforma                              | Imediato, basta acessar                                                                |
| **Exemplos AWS**         | Data center próprio, servidores locais                     | **Amazon EC2**, **Amazon S3**, **Amazon VPC**, **EBS** | **AWS Elastic Beanstalk**, **Amazon RDS**, **AWS Lambda**, **API Gateway** | **Amazon WorkSpaces**, **Amazon Chime**, **Amazon Connect**, **Office 365**, **Gmail** |
