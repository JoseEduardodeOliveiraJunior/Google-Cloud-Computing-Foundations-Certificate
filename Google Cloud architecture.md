# Google Cloud Foundations — Infraestrutura, Compute, Storage, Big Data e Regiões

Esse conteúdo apresenta uma **visão geral da arquitetura da Google Cloud**.

A principal ideia é enxergar a infraestrutura da Google Cloud em **camadas** e entender onde entram seus principais serviços.

---

# 1. As 3 camadas da infraestrutura Google Cloud

Podemos imaginar a infraestrutura da Google Cloud da seguinte maneira:

```text
┌─────────────────────────────────────────────┐
│  3. BIG DATA + MACHINE LEARNING             │
│  BigQuery, Dataflow, Pub/Sub, Vertex AI...  │
├─────────────────────────────────────────────┤
│  2. COMPUTE + STORAGE                       │
│  Compute Engine, Cloud Run, Cloud Storage   │
│  Cloud SQL, Spanner, Bigtable...            │
├─────────────────────────────────────────────┤
│  1. NETWORKING + SECURITY                   │
│  Rede, VPC, Firewall, IAM, segurança etc.   │
└─────────────────────────────────────────────┘
```

As três grandes camadas são:

1. **Networking + Security**
2. **Compute + Storage**
3. **Big Data + Machine Learning**

---

# 2. Networking e Security

A camada de **Networking e Security** é a fundação da infraestrutura.

Antes de pensar em:

- Máquinas virtuais
- Bancos de dados
- Containers
- BigQuery
- Aplicações

é necessário possuir uma estrutura de rede e segurança.

Essa camada envolve conceitos como:

- Redes
- Comunicação
- Segurança
- Controle de acesso
- Conectividade
- Firewalls
- IAM
- Proteção dos recursos

Por exemplo:

```text
Usuário
   ↓
Internet
   ↓
Rede Google
   ↓
Firewall / Segurança
   ↓
Aplicação
```

Se uma empresa possui uma aplicação no Google Cloud, toda a comunicação precisa passar pela infraestrutura de rede.

Podemos comparar essa camada com a fundação de uma casa:

```text
Fundação da casa
      ↓
Networking + Security
```

Sem uma boa fundação, o restante da estrutura não funciona adequadamente.

---

# 3. Compute e Storage

Na segunda camada temos duas coisas fundamentais:

- **Compute**
- **Storage**

## Compute

**Compute significa processamento.**

São os recursos responsáveis por executar:

- Aplicações
- APIs
- Containers
- Algoritmos
- Processamentos
- Jobs
- Serviços

Exemplo:

```text
Compute Engine
      ↓
Executa uma aplicação
```

---

## Storage

**Storage significa armazenamento.**

É onde ficam:

- Arquivos
- Dados
- Imagens
- Vídeos
- Backups
- Bancos de dados
- Datasets

Exemplo:

```text
Cloud Storage
      ↓
Armazena arquivos
```

Portanto:

> **Compute = processa**

> **Storage = armazena**

---

# 4. Decoupling Compute and Storage

Um conceito importante apresentado pela Google Cloud é:

> **Decoupling Compute and Storage**

Em português:

> **Desacoplamento entre processamento e armazenamento.**

Isso significa que a capacidade de processamento e armazenamento podem crescer de maneira independente.

---

## Exemplo

Imagine que inicialmente uma empresa possui:

```text
100 GB de dados
+
2 CPUs
```

Depois de algum tempo, ela passa a possuir:

```text
10 TB de dados
+
2 CPUs
```

O armazenamento aumentou muito, porém a necessidade de processamento permaneceu praticamente igual.

Nesse caso, não seria necessário aumentar CPU apenas porque o armazenamento cresceu.

---

Também pode acontecer o contrário:

```text
1 TB de dados
+
100 CPUs
```

A empresa pode possuir poucos dados, mas precisar de muita capacidade computacional para realizar um processamento complexo.

---

A arquitetura pode ser visualizada assim:

```text
         Aplicação
             │
       ┌─────┴─────┐
       ↓           ↓
    Compute     Storage
       ↑           ↑
    aumenta      aumenta
se necessário  se necessário
```

### Para memorizar

> **Compute = processa**

> **Storage = guarda**

> **Decoupled = Compute e Storage podem crescer independentemente.**

---

# 5. Serviços de Compute da Google Cloud

A Google oferece diferentes serviços de computação.

Entre os principais estão:

```text
Compute
│
├── Compute Engine
├── Google Kubernetes Engine
├── App Engine
├── Cloud Run
└── Cloud Run functions
```

Cada serviço atende necessidades diferentes.

---

# 6. Compute Engine

O **Compute Engine** é o serviço de **máquinas virtuais** da Google Cloud.

Com ele é possível criar uma máquina virtual dentro da infraestrutura do Google.

```text
Google Cloud
      ↓
Compute Engine
      ↓
VM
      ↓
Linux
      ↓
Sua aplicação
```

Você possui bastante controle sobre a máquina.

Pode definir:

- Sistema operacional
- CPU
- Memória RAM
- Disco
- Rede
- Software instalado
- Configurações da máquina

---

## Exemplo com Spring Boot

Imagine que você possui uma API Java utilizando Spring Boot.

Poderíamos ter:

```text
Compute Engine
      ↓
Ubuntu
      ↓
Java
      ↓
Spring Boot
      ↓
API
```

Você criaria uma VM, instalaria Java e executaria sua aplicação nela.

### Para memorizar

> **Compute Engine = Máquina Virtual da Google Cloud.**

---

# 7. Google Kubernetes Engine — GKE

O **Google Kubernetes Engine**, conhecido como **GKE**, é o serviço Kubernetes gerenciado da Google.

Ele é utilizado principalmente para executar e gerenciar **containers**.

Imagine possuir vários containers:

```text
Docker Container
Docker Container
Docker Container
Docker Container
Docker Container
```

Gerenciar centenas ou milhares de containers manualmente seria muito complicado.

O Kubernetes ajuda a organizar essa infraestrutura.

```text
                    GKE
                     │
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
    Container     Container     Container
```

O Kubernetes pode ajudar com:

- Escalabilidade
- Balanceamento
- Disponibilidade
- Distribuição dos containers
- Reinicialização automática
- Orquestração
- Gerenciamento de workloads

### Para memorizar

> **GKE = Kubernetes gerenciado pelo Google.**

---

# 8. App Engine

O **App Engine** é uma plataforma para executar aplicações sem precisar administrar diretamente toda a infraestrutura.

Você pode pensar assim:

```text
Seu código
    ↓
App Engine
    ↓
Google gerencia infraestrutura
```

Você se preocupa principalmente com:

```text
Código
```

Enquanto o Google gerencia boa parte de:

```text
Servidor
Sistema operacional
Infraestrutura
Escalabilidade
```

O App Engine é um exemplo clássico de:

> **PaaS — Platform as a Service**

### Para memorizar

> **App Engine = plataforma gerenciada para executar aplicações.**

---

# 9. Cloud Run

O **Cloud Run** permite executar **containers de maneira serverless**.

Imagine uma aplicação Python:

```text
Aplicação Python
      ↓
Docker
      ↓
Container
      ↓
Cloud Run
```

Você cria a aplicação e empacota utilizando um container.

Depois, o Cloud Run executa esse container.

```text
Você
 ↓
Container
 ↓
Cloud Run
 ↓
Google gerencia infraestrutura
```

Uma das grandes vantagens é não precisar administrar diretamente servidores.

Além disso, o Cloud Run pode escalar automaticamente de acordo com a demanda.

### Para memorizar

> **Cloud Run = Container Serverless.**

---

# 10. Cloud Run Functions

O **Cloud Run functions** é utilizado para executar funções ou pequenos códigos em resposta a eventos.

Por exemplo:

```text
Arquivo enviado ao Cloud Storage
              ↓
            Evento
              ↓
      Cloud Run function
              ↓
       Processa arquivo
```

Imagine uma função Python:

```python
def processar_arquivo(event):
    print("Arquivo recebido")
```

Você não precisa criar uma VM inteira apenas para executar essa função.

A infraestrutura necessária é gerenciada pela Google.

### Para memorizar

> **Cloud Run functions = funções executadas em resposta a eventos.**

---

# 11. Comparação dos serviços de Compute

Uma maneira simples de memorizar:

| Serviço | Principal conceito |
|---|---|
| Compute Engine | Máquina Virtual |
| Google Kubernetes Engine | Kubernetes |
| App Engine | Plataforma para aplicações |
| Cloud Run | Container Serverless |
| Cloud Run functions | Funções e eventos |

Podemos imaginar aproximadamente:

```text
MAIS CONTROLE SOBRE INFRAESTRUTURA
              ↑

       Compute Engine
              │
             GKE
              │
          Cloud Run
              │
 App Engine / Functions

              ↓
MENOS INFRAESTRUTURA PARA GERENCIAR
```

Essa não é uma classificação absoluta, mas ajuda a criar um modelo mental inicial.

---

# 12. Serviços de Storage

A Google Cloud oferece diferentes opções de armazenamento e bancos de dados.

Entre elas estão:

```text
Storage
│
├── Cloud Storage
├── Cloud SQL
├── Spanner
├── Bigtable
└── Firestore
```

É importante entender que nem todos possuem a mesma finalidade.

---

# 13. Cloud Storage

O **Cloud Storage** é o serviço de armazenamento de **objetos** da Google Cloud.

Pode armazenar:

- Imagens
- Vídeos
- PDFs
- Arquivos CSV
- JSON
- Backups
- Logs
- Datasets
- Arquivos em geral

Os arquivos são armazenados dentro de estruturas chamadas **Buckets**.

Por exemplo:

```text
Cloud Storage

bucket-dados
│
├── clientes.csv
├── vendas.csv
├── produtos.json
├── relatorio.pdf
└── imagem.png
```

Cloud Storage também é muito utilizado para construção de:

- Data Lakes
- Backup
- Arquivamento
- Pipelines de dados

### Para memorizar

> **Cloud Storage = armazenamento de objetos/arquivos.**

---

# 14. Cloud SQL

O **Cloud SQL** é um serviço de banco de dados relacional gerenciado.

Ele suporta bancos como:

- PostgreSQL
- MySQL
- SQL Server

Uma arquitetura poderia ser:

```text
Aplicação
    ↓
Cloud SQL
    ↓
PostgreSQL
```

Você continua utilizando conceitos tradicionais de banco relacional.

Por exemplo:

```sql
SELECT
INSERT
UPDATE
DELETE
JOIN
```

A principal diferença é que a Google gerencia boa parte da infraestrutura do banco.

### Para memorizar

> **Cloud SQL = banco SQL relacional gerenciado.**

---

# 15. Spanner

O **Spanner** também é um banco de dados **relacional**.

Porém, ele foi projetado para sistemas que precisam de:

- Grande escalabilidade
- Alta disponibilidade
- Distribuição geográfica
- Consistência
- Aplicações globais

Imagine:

```text
Brasil
   \
    \
   Spanner
    /
   /
Europa
   \
   EUA
```

Os dados podem estar distribuídos geograficamente.

### Para memorizar

> **Spanner = banco relacional distribuído e altamente escalável.**

---

# 16. Bigtable

O **Bigtable** é um banco de dados **NoSQL**.

É utilizado principalmente para:

- Grandes volumes de dados
- Baixa latência
- Alta performance
- IoT
- Telemetria
- Logs
- Métricas
- Dados de sensores

Imagine milhões de dispositivos enviando dados:

```text
Sensor
Sensor
Sensor
Sensor
Sensor
   ↓
Bigtable
```

### Para memorizar

> **Bigtable = banco NoSQL para grandes volumes e alta performance.**

---

# 17. Firestore

O **Firestore** também é um banco **NoSQL**.

É bastante utilizado em:

- Aplicações Web
- Aplicações Mobile
- Aplicações Serverless
- Sistemas que trabalham com documentos

Os dados possuem estrutura de documentos.

Exemplo:

```json
{
  "nome": "Eduardo",
  "idade": 25,
  "cidade": "São Paulo"
}
```

Em um banco relacional tradicional temos:

```text
Tabela
  ↓
Linha
  ↓
Coluna
```

No Firestore temos algo semelhante a:

```text
Collection
    ↓
Document
    ↓
Fields
```

### Para memorizar

> **Firestore = banco NoSQL orientado a documentos.**

---

# 18. Bancos relacionais vs NoSQL

Um ponto importante do curso é saber diferenciar os serviços.

## Bancos relacionais

Na Google Cloud:

```text
Relacionais
│
├── Cloud SQL
└── Spanner
```

São bancos que trabalham com estruturas como:

```text
Cliente
────────────────
id
nome
email
cpf
```

Também permitem relacionamentos.

```text
Cliente
   ↓
Pedido
   ↓
Produto
```

---

## Bancos NoSQL

Na Google Cloud:

```text
NoSQL
│
├── Bigtable
└── Firestore
```

Eles possuem modelos diferentes do banco relacional tradicional.

---

## Para memorizar

```text
RELACIONAL
├── Cloud SQL
└── Spanner

NoSQL
├── Bigtable
└── Firestore
```

---

# 19. Big Data e Machine Learning

Na terceira camada da infraestrutura temos os serviços relacionados a:

- Big Data
- Analytics
- Machine Learning
- Inteligência Artificial

Alguns serviços apresentados são:

```text
Big Data / Analytics
│
├── Cloud Storage
├── Managed Service for Apache Spark
├── Bigtable
├── BigQuery
├── Dataflow
├── Firestore
├── Pub/Sub
├── Looker
└── Spanner
```

Também existem serviços de Inteligência Artificial e Machine Learning dentro do ecossistema Google Cloud.

---

# 20. Pipeline de dados

Esses serviços podem ser utilizados em conjunto para construir um **Data Pipeline**.

Um exemplo simples:

```text
Sistemas
   ↓
Pub/Sub
   ↓
Dataflow
   ↓
BigQuery
   ↓
Looker
```

Cada serviço possui uma função.

---

## Pub/Sub

Pode receber e distribuir eventos e mensagens.

```text
Sistema
   ↓
Evento
   ↓
Pub/Sub
```

---

## Dataflow

Pode processar e transformar os dados.

```text
Pub/Sub
   ↓
Dataflow
   ↓
Transformação
```

---

## BigQuery

Armazena e permite analisar grandes volumes de dados.

```text
Dataflow
   ↓
BigQuery
```

---

## Looker

Pode utilizar os dados para criar análises, relatórios e dashboards.

```text
BigQuery
   ↓
Looker
   ↓
Dashboard
```

---

# 21. Exemplo de Data Engineering

Imagine uma grande plataforma de e-commerce.

Milhares ou milhões de eventos acontecem todos os dias:

```text
Cliente abriu produto

Cliente adicionou produto ao carrinho

Cliente realizou compra

Cliente cancelou pedido

Cliente pesquisou produto
```

Esses eventos poderiam ser enviados para:

```text
Pub/Sub
```

Depois processados:

```text
Dataflow
```

Armazenados e analisados:

```text
BigQuery
```

E exibidos:

```text
Looker
```

A arquitetura seria:

```text
Aplicação
    ↓
Pub/Sub
    ↓
Dataflow
    ↓
BigQuery
    ↓
Looker
    ↓
Dashboard
```

Esse é um exemplo clássico de **Data Pipeline**.

---

# 22. Managed Services

Outro conceito importante apresentado é o de **Managed Services**, ou serviços gerenciados.

Quando utilizamos serviços gerenciados, o provedor de nuvem assume parte significativa da administração da infraestrutura.

Por exemplo, utilizando o BigQuery, você não precisa se preocupar diretamente com:

```text
Quantos servidores existem?

Quanto de RAM é necessária?

Quantos discos existem?

Como distribuir o cluster?

Como atualizar os servidores?

Como substituir hardware com defeito?
```

Você pode focar principalmente em:

```text
Dados
+
Consultas
+
Análises
```

Por exemplo:

```sql
SELECT
    cliente,
    SUM(valor)
FROM vendas
GROUP BY cliente;
```

A Google administra grande parte da infraestrutura necessária para executar a consulta.

### Para memorizar

> **Managed Service = Google administra grande parte da infraestrutura para você.**

---

# 23. Rede global da Google

Toda a infraestrutura da Google Cloud utiliza a rede global construída pelo Google.

Podemos imaginar:

```text
Brasil ───────── EUA
   │              │
   │              │
Europa ───────── Ásia
```

A infraestrutura global permite aproximar aplicações e conteúdos dos usuários.

Isso pode melhorar:

- Latência
- Performance
- Disponibilidade
- Experiência dos usuários

---

# 24. Content Caching

A Google possui diversos pontos de cache distribuídos geograficamente.

O objetivo é armazenar conteúdo frequentemente utilizado mais próximo do usuário.

Imagine:

```text
Servidor original
       ↓
Cache próximo ao usuário
       ↓
Usuário
```

Em vez de buscar todas as informações em um servidor muito distante, determinado conteúdo pode ser entregue por um local mais próximo.

Isso pode diminuir a latência.

---

# 25. O que é Latência?

**Latência** é o tempo necessário para uma informação viajar de sua origem até seu destino.

Imagine:

```text
Seu computador
      ↓
    Internet
      ↓
   Servidor
      ↓
    Resposta
```

Se a comunicação demora:

```text
20 ms
```

temos uma latência relativamente baixa.

Se demora:

```text
500 ms
```

temos uma latência maior.

### Para memorizar

> **Latência = tempo/atraso da comunicação entre dois pontos.**

Normalmente:

> **Menor latência = melhor experiência para o usuário.**

---

# 26. Estrutura geográfica da Google Cloud

A infraestrutura da Google Cloud é distribuída geograficamente.

Um conceito fundamental é:

```text
Google Cloud
    ↓
Region
    ↓
Zone
```

É extremamente importante entender a diferença entre **Region** e **Zone**.

---

# 27. O que é uma Region?

Uma **Region** representa uma área geográfica independente onde existem recursos da Google Cloud.

Exemplo apresentado no curso:

```text
London
=
europe-west2
```

Uma região contém várias zonas.

```text
Region
│
├── Zone A
├── Zone B
└── Zone C
```

### Para memorizar

> **Region = região geográfica.**

---

# 28. O que é uma Zone?

Uma **Zone** representa uma área de implantação dentro de uma região.

Por exemplo:

```text
Region: europe-west2
│
├── europe-west2-a
├── europe-west2-b
└── europe-west2-c
```

Quando você cria determinados recursos, pode escolher em qual zona eles serão executados.

Por exemplo:

```text
Compute Engine
      ↓
VM
      ↓
europe-west2-a
```

A VM estará associada àquela zona.

### Para memorizar

> **Zone = local dentro de uma Region onde determinados recursos são implantados.**

---

# 29. Region contém Zones

Essa relação precisa ficar muito clara:

```text
Área geográfica
      ↓
    REGION
      │
 ┌────┼────┐
 ↓    ↓    ↓
Zone A Zone B Zone C
```

### Regra para memorizar

> **Uma Region contém múltiplas Zones.**

---

# 30. Problema de utilizar apenas uma Zone

Imagine uma aplicação onde existe apenas uma VM:

```text
Region
│
├── Zone A
│      ↓
│     VM
│
├── Zone B
│
└── Zone C
```

Se a Zone A ficar indisponível:

```text
Zone A ❌
```

a VM também poderá ficar indisponível.

Isso acontece porque recursos **zonais** dependem daquela zona específica.

---

# 31. Recursos Zonais

Um recurso zonal opera dentro de uma única zona.

Exemplo:

```text
Region
   ↓
Zone A
   ↓
VM
```

Se a zona estiver indisponível:

```text
Zone A ❌
   ↓
VM indisponível
```

Por isso aplicações críticas normalmente precisam considerar mecanismos de redundância.

---

# 32. Redundância

**Redundância** significa possuir recursos adicionais para evitar que um único ponto de falha derrube todo o sistema.

Em vez de possuir:

```text
Zone A
  ↓
Servidor
```

poderíamos possuir:

```text
        Aplicação
            │
     ┌──────┴──────┐
     ↓             ↓
  Zone A         Zone B
     ↓             ↓
    VM 1          VM 2
```

Se acontecer:

```text
Zone A ❌
```

ainda temos:

```text
Zone B ✅
```

Dependendo da arquitetura, a aplicação pode continuar funcionando.

### Para memorizar

> **Redundância = possuir recursos duplicados/distribuídos para reduzir pontos únicos de falha.**

---

# 33. Alta disponibilidade

A utilização de múltiplas zonas pode ajudar na criação de sistemas com **High Availability**.

Em português:

> **Alta Disponibilidade**

Exemplo:

```text
                 Usuário
                    ↓
            Load Balancer
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
       Zone A              Zone B
          ↓                   ↓
         VM 1                VM 2
```

Se uma VM ou zona apresentar problemas, outra pode continuar atendendo os usuários.

---

# 34. Multi-region

Alguns serviços permitem utilizar configurações **multi-regionais**.

Podemos imaginar a hierarquia:

```text
Zone
  <
Region
  <
Multi-region
```

Uma arquitetura multi-regional pode distribuir dados ou serviços entre diferentes regiões geográficas.

Exemplo:

```text
           Aplicação
               │
      ┌────────┼────────┐
      ↓        ↓        ↓
   Brasil     EUA      Europa
   Region    Region    Region
```

Isso pode ajudar em cenários que precisam de:

- Alta disponibilidade
- Disaster Recovery
- Aplicações globais
- Baixa latência global
- Resiliência

---

# 35. Exemplo Multi-region com Spanner

O Spanner permite configurações multi-regionais.

Em vez de armazenar tudo apenas em:

```text
Spanner
   ↓
Region A
```

podemos possuir algo semelhante a:

```text
            Spanner
               │
       ┌───────┴───────┐
       ↓               ↓
    Region A         Region B
       │               │
   Zone 1/2/3       Zone 1/2/3
```

Os dados podem possuir réplicas distribuídas.

Essas réplicas ajudam a melhorar características como:

- Disponibilidade
- Resiliência
- Distribuição global
- Latência
- Recuperação de falhas

---

# 36. Por que escolher corretamente uma região?

A localização dos recursos influencia diversas características.

Entre elas:

- Latência
- Disponibilidade
- Durabilidade
- Resiliência
- Recuperação de desastres
- Requisitos regulatórios
- Proximidade dos usuários

Imagine uma empresa com usuários principalmente no Brasil.

Uma arquitetura poderia buscar:

```text
Usuários brasileiros
        ↓
Região próxima
        ↓
Aplicação
```

Quanto mais próximo geograficamente o serviço estiver dos usuários, potencialmente menor será a latência.

---

# 37. Problemas em uma região inteira

Também precisamos pensar em situações extremas.

Por exemplo:

- Falha generalizada
- Problema de infraestrutura
- Desastre natural
- Problemas elétricos
- Problemas de conectividade

Se toda a aplicação estiver em uma única região:

```text
Region A
   ↓
Aplicação
```

um problema regional pode impactar o serviço.

Dependendo dos requisitos, pode-se criar algo como:

```text
             Usuários
                │
        ┌───────┴────────┐
        ↓                ↓
 Region Brasil       Outra Region
```

Isso leva a conceitos como:

- Disaster Recovery
- High Availability
- Replicação
- Redundância
- Multi-region

---

# 38. Availability

**Availability significa Disponibilidade.**

A pergunta principal é:

> **O serviço está funcionando e acessível?**

Imagine:

```text
Usuário
   ↓
Aplicação ✅
```

Se o usuário consegue acessar o sistema, ele está disponível.

### Para memorizar

> **Availability = o serviço está disponível?**

---

# 39. Durability

**Durability significa Durabilidade.**

A pergunta principal é:

> **Qual a probabilidade de meus dados continuarem existindo?**

Imagine:

```text
Arquivo
   ↓
Armazenamento
   ↓
Réplicas
   ↓
Proteção contra perda
```

Um sistema com alta durabilidade possui uma probabilidade extremamente pequena de perda permanente dos dados.

### Para memorizar

> **Durability = meus dados continuam existindo?**

---

# 40. Latency

**Latency significa Latência.**

A pergunta é:

> **Quanto tempo demora para a informação chegar ou para receber uma resposta?**

Exemplo:

```text
Usuário
   ↓
20 ms
   ↓
Servidor
```

### Para memorizar

> **Latency = quanto tempo demora?**

---

# 41. Availability vs Durability vs Latency

Uma forma simples de memorizar:

```text
Availability
→ Está funcionando?

Durability
→ Meu dado continua existindo?

Latency
→ Quanto demora?
```

Ou:

| Conceito | Pergunta |
|---|---|
| Availability | O serviço está disponível? |
| Durability | Meus dados continuam protegidos? |
| Latency | Quanto tempo demora? |

---

# 42. Visão geral da arquitetura

Podemos resumir o conteúdo da aula desta maneira:

```text
                      GOOGLE CLOUD
                           │
        ┌──────────────────┴─────────────────┐
        │                                    │
   Global Network                       Security
        │
        ↓
      Region
        │
   ┌────┼────┐
   ↓    ↓    ↓
Zone A Zone B Zone C
        │
        ↓

────────────────────────────────────────────
              COMPUTE + STORAGE
────────────────────────────────────────────

Compute                       Storage
│                             │
├─ Compute Engine             ├─ Cloud Storage
├─ GKE                        ├─ Cloud SQL
├─ App Engine                 ├─ Spanner
├─ Cloud Run                  ├─ Bigtable
└─ Functions                  └─ Firestore

────────────────────────────────────────────
          DATA + ANALYTICS + ML
────────────────────────────────────────────

Pub/Sub
   ↓
Dataflow
   ↓
BigQuery
   ↓
Looker
   ↓
Insights
```

---

# 43. Resumo dos serviços

| Serviço | Categoria | Principal função |
|---|---|---|
| Compute Engine | Compute | Máquinas Virtuais |
| GKE | Compute | Kubernetes |
| App Engine | Compute | Plataforma gerenciada |
| Cloud Run | Compute | Containers Serverless |
| Cloud Run functions | Compute | Funções/eventos |
| Cloud Storage | Storage | Objetos e arquivos |
| Cloud SQL | Database | Banco relacional |
| Spanner | Database | Banco relacional distribuído |
| Bigtable | Database | Banco NoSQL de grande escala |
| Firestore | Database | Banco NoSQL de documentos |
| Pub/Sub | Data | Mensageria e eventos |
| Dataflow | Data | Processamento de dados |
| BigQuery | Data | Data Warehouse e Analytics |
| Looker | Analytics | Dashboards e BI |

---

# 44. O que memorizar desta aula

Não é necessário decorar todas as frases.

Os principais conceitos são:

1. Google Cloud possui uma infraestrutura global.

2. **Networking + Security** formam a base da infraestrutura.

3. **Compute = processamento.**

4. **Storage = armazenamento.**

5. Compute e Storage podem escalar separadamente.

6. Esse conceito é chamado de **Decoupling**.

7. **Compute Engine = Máquina Virtual.**

8. **GKE = Kubernetes gerenciado.**

9. **App Engine = plataforma gerenciada para aplicações.**

10. **Cloud Run = Container Serverless.**

11. **Cloud Run functions = funções executadas por eventos.**

12. **Cloud Storage = armazenamento de objetos/arquivos.**

13. **Cloud SQL = banco relacional gerenciado.**

14. **Spanner = banco relacional distribuído.**

15. **Bigtable = banco NoSQL de grande escala.**

16. **Firestore = banco NoSQL orientado a documentos.**

17. **Cloud SQL + Spanner = Relacionais.**

18. **Bigtable + Firestore = NoSQL.**

19. **Pub/Sub = mensagens e eventos.**

20. **Dataflow = processamento e transformação de dados.**

21. **BigQuery = Data Warehouse e Analytics.**

22. **Looker = BI, visualização e dashboards.**

23. **Region = área geográfica.**

24. Uma **Region contém várias Zones**.

25. **Zone = local onde determinados recursos são implantados.**

26. Recursos zonais podem ficar indisponíveis caso a zona fique indisponível.

27. **Redundância** reduz pontos únicos de falha.

28. **Multi-region** permite distribuir dados ou serviços geograficamente.

29. **Latency = tempo de comunicação.**

30. **Availability = disponibilidade do serviço.**

31. **Durability = proteção/permanência dos dados.**

---

# 45. Resumo visual para memorização

```text
GOOGLE CLOUD
│
├── NETWORKING + SECURITY
│
├── COMPUTE
│   ├── Compute Engine → VM
│   ├── GKE → Kubernetes
│   ├── App Engine → PaaS
│   ├── Cloud Run → Container Serverless
│   └── Functions → Eventos
│
├── STORAGE / DATABASE
│   ├── Cloud Storage → Objetos
│   ├── Cloud SQL → Relacional
│   ├── Spanner → Relacional distribuído
│   ├── Bigtable → NoSQL
│   └── Firestore → NoSQL documentos
│
├── DATA
│   ├── Pub/Sub → Eventos
│   ├── Dataflow → Processamento
│   ├── BigQuery → Analytics
│   └── Looker → BI
│
└── INFRAESTRUTURA GLOBAL
    ├── Region
    │   ├── Zone A
    │   ├── Zone B
    │   └── Zone C
    │
    └── Multi-region
```

---

# 46. Foco para Data Engineering

Para quem pretende avançar posteriormente para **Data Engineering na Google Cloud**, alguns serviços desse conteúdo serão especialmente importantes:

```text
Cloud Storage
      ↓
Pub/Sub
      ↓
Dataflow
      ↓
BigQuery
      ↓
Looker
```

Podemos pensar nas funções da seguinte maneira:

```text
Cloud Storage
→ Armazenar dados

Pub/Sub
→ Receber eventos/dados em tempo real

Dataflow
→ Processar e transformar dados

BigQuery
→ Armazenar e analisar grandes volumes de dados

Looker
→ Visualizar e transformar dados em insights
```

Um pipeline completo poderia ser:

```text
Aplicação / Sistema / IoT
           ↓
        Pub/Sub
           ↓
        Dataflow
           ↓
        BigQuery
           ↓
         Looker
           ↓
     Dashboard / Insights
```

Esses conceitos aparecem com muito mais profundidade conforme o estudo avança de **Google Cloud Foundations** para **Data Engineering**.

---

# 47. Mapa mental final

```text
GOOGLE CLOUD FOUNDATIONS

Google Cloud
│
├── Infraestrutura
│   │
│   ├── Networking
│   └── Security
│
├── Compute
│   │
│   ├── Compute Engine
│   ├── GKE
│   ├── App Engine
│   ├── Cloud Run
│   └── Cloud Run functions
│
├── Storage / Database
│   │
│   ├── Cloud Storage
│   ├── Cloud SQL
│   ├── Spanner
│   ├── Bigtable
│   └── Firestore
│
├── Data / Analytics
│   │
│   ├── Pub/Sub
│   ├── Dataflow
│   ├── BigQuery
│   └── Looker
│
└── Infraestrutura Global
    │
    ├── Region
    │   │
    │   ├── Zone A
    │   ├── Zone B
    │   └── Zone C
    │
    ├── Multi-region
    │
    ├── Availability
    ├── Durability
    └── Latency
```

---

# Conclusão

A Google Cloud possui uma infraestrutura construída em diferentes camadas.

A base é composta por:

```text
Networking + Security
```

Sobre essa base ficam os recursos de:

```text
Compute + Storage
```

E acima desses recursos existem diversos serviços de:

```text
Big Data + Analytics + Machine Learning
```

Além disso, a infraestrutura é distribuída globalmente através de:

```text
Regions
   ↓
Zones
```

Essa distribuição permite criar aplicações com maior:

- Disponibilidade
- Escalabilidade
- Resiliência
- Durabilidade
- Performance
- Baixa latência

Os conceitos apresentados aqui formam a base para compreender os serviços mais avançados da **Google Cloud Platform**.