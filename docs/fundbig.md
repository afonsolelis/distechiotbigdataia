# Fundamentos e Ferramentas de Big Data

## Revisão de Banco de Dados Rápida!

## 1. Introdução e Objetivos

A importância da integridade e confiabilidade dos dados é reconhecida firmemente pela indústria da tecnologia da informação. Os conceitos ACID são fundamentais para garantir que os sistemas de banco de dados mantenham a consistência dos dados em meio a operações complexas e concorrentes. Além disso, a escolha da ferramenta de banco de dados adequada pode influenciar significativamente o desempenho e a escalabilidade das aplicações.

## 2. Conceitos ACID

Os conceitos ACID são fundamentais para garantir a confiabilidade e a integridade dos dados em um sistema de banco de dados. ACID é um acrônimo que representa:

1. **Atomicidade (Atomicity)**: Refere-se à propriedade de que uma transação deve ser tratada como uma unidade indivisível. Ou seja, todas as operações dentro de uma transação devem ser concluídas com sucesso; caso contrário, a transação é revertida. Isso garante que o banco de dados não fique em um estado inconsistente.

2. **Consistência (Consistency)**: Garante que uma transação leva o banco de dados de um estado válido para outro estado válido. Qualquer dado escrito no banco de dados deve ser válido de acordo com todas as regras definidas, incluindo restrições, gatilhos, cascatas, etc.

3. **Isolamento (Isolation)**: Garante que as operações de transações concorrentes não interfiram umas nas outras. O nível de isolamento determina como e quando as mudanças feitas em uma transação se tornam visíveis para outras transações.

4. **Durabilidade (Durability)**: Garante que, uma vez que uma transação foi confirmada, ela permanecerá assim mesmo em caso de falha do sistema. Isso é alcançado através do uso de logs de transação e backups.

## 3. Principais Ferramentas de Banco de Dados

### 3.1 PostgreSQL

O PostgreSQL é um dos sistemas de gerenciamento de banco de dados relacionais mais avançados e populares disponíveis hoje. Ele é conhecido por sua robustez, flexibilidade e conformidade com os padrões SQL. Algumas características incluem:

- **Suporte ACID completo**
- **Suporte a JSON e JSONB para dados não estruturados**
- **Extensibilidade com funções, operadores e tipos de dados personalizados**
- **Comunidade ativa e grande quantidade de recursos e documentação**

### 3.2 MySQL

O MySQL é outro sistema de gerenciamento de banco de dados relacional muito popular, especialmente no desenvolvimento web. Ele é conhecido por sua velocidade e facilidade de uso. Algumas características incluem:

- **Suporte ACID com o mecanismo de armazenamento InnoDB**
- **Ampla adoção e suporte pela comunidade**
- **Compatibilidade com diversas linguagens de programação**

## 4. Comparação com Hadoop

O Hadoop é uma plataforma de software de código aberto usada para computação distribuída e armazenamento de grandes volumes de dados. Ele é composto por vários módulos, incluindo o Hadoop Distributed File System (HDFS) e o MapReduce. Comparado com bancos de dados relacionais como PostgreSQL e MySQL:

- **Hadoop** é ideal para processamento de grandes volumes de dados não estruturados e semi-estruturados.
- **Bancos de dados relacionais** são ideais para transações ACID e consultas complexas em dados estruturados.

## 5. Comparação com ClickHouse

O ClickHouse é um sistema de gerenciamento de banco de dados de coluna projetado para consultas analíticas em tempo real. Comparado com bancos de dados relacionais tradicionais:

- **ClickHouse** é otimizado para leitura e consultas analíticas, com alta performance em consultas complexas em grandes volumes de dados.
- **Bancos de dados relacionais** são mais adequados para operações transacionais e consultas que exigem conformidade ACID.

### 5.1 ClickHouse e MergeTree

O ClickHouse utiliza uma estrutura de dados chamada **MergeTree** para armazenar dados de forma eficiente. O MergeTree permite:

- **Particionamento**: Divisão dos dados em segmentos menores para facilitar a consulta.
- **Indexação**: Criação de índices para acelerar as consultas.
- **Merge**: Combinação de partes menores dos dados em partes maiores para otimizar o armazenamento e a performance.

## Adendo: O que é OLAP?

OLAP (Online Analytical Processing) é uma tecnologia que permite a análise rápida de grandes volumes de dados armazenados em um banco de dados multidimensional. OLAP é amplamente utilizado em aplicações de Business Intelligence (BI) para realizar consultas complexas e análises de dados.

### Características do OLAP

- **Multidimensionalidade**: OLAP permite organizar dados em múltiplas dimensões, facilitando a visualização e análise de informações de diferentes perspectivas.
- **Velocidade**: OLAP é otimizado para consultas rápidas e análises interativas, permitindo que os usuários obtenham insights em tempo real.
- **Agregação**: OLAP suporta a agregação de dados, permitindo cálculos como somas, médias e contagens em diferentes níveis de granularidade.
- **Hierarquias**: OLAP permite a definição de hierarquias dentro das dimensões, facilitando a navegação e análise de dados em diferentes níveis de detalhe.

### Tipos de OLAP

1. **ROLAP (Relational OLAP)**: Utiliza bancos de dados relacionais para armazenar e gerenciar dados. As consultas OLAP são traduzidas em consultas SQL complexas.
2. **MOLAP (Multidimensional OLAP)**: Utiliza bancos de dados multidimensionais (cubos OLAP) para armazenar dados. Oferece desempenho superior para consultas complexas.
3. **HOLAP (Hybrid OLAP)**: Combina as abordagens ROLAP e MOLAP, aproveitando os pontos fortes de ambos os tipos.

### Aplicações de OLAP

OLAP é amplamente utilizado em várias áreas, incluindo:

- **Análise de Vendas**: Para analisar tendências de vendas, desempenho de produtos e comportamento de clientes.
- **Finanças**: Para análise de lucros, despesas e previsões financeiras.
- **Marketing**: Para avaliar a eficácia das campanhas de marketing e segmentar mercados.
- **Operações**: Para monitorar e otimizar processos operacionais e logísticos.

OLAP é uma ferramenta poderosa para transformar dados brutos em insights acionáveis, permitindo que as organizações tomem decisões informadas e baseadas em dados.

---

<div class="container m-1">
    <div class="row">
        <div class="col-12">
            <div class="embed-responsive embed-responsive-16by9">
                <iframe src="https://slides.com/afonsobrandao/fundbigdata/embed?style=light" title="Fundamentos de Engenharia de Dados e BigData" scrolling="no" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
            </div>
        </div>
    </div>
</div>

## Autoestudos

<div class="container m-1">
    <div class="row">
        <div class="col-12">
            <div class="embed-responsive embed-responsive-16by9">
                <iframe width="560" height="315" src="https://www.youtube.com/embed/pQXr-xXhKNs?si=6a-ZY8l-4_WpXOLN" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
            </div>
        </div>
    </div>
</div>

<div class="container m-1">
    <div class="row">
        <div class="col-12">
            <a href="https://www.oracle.com/br/big-data/what-is-big-data/#:~:text=A%20defini%C3%A7%C3%A3o%20de%20big%20data,de%20novas%20fontes%20de%20dados." class="btn btn-primary w-100" style="color: white;" role="button">BigData sem Mistério</a>
        </div>
    </div>
</div>

<div class="container m-1">
    <div class="row">
        <div class="col-12">
            <a href="https://www.researchgate.net/publication/366380179_BIG_DATA_FUNDAMENTOS_E_APLICACAO_NAS_EMPRESAS" class="btn btn-primary w-100" style="color: white;" role="button">Fundamentos e Aplicação de BigData em Empresas</a>
        </div>
    </div>
</div>

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>

 <style>
    .embed-responsive-16by9 {
        padding-bottom: 56.25%; /* Proporção 16:9 */
        position: relative;
        height: 0;
        overflow: hidden;
        max-width: 100%;
    }
    .embed-responsive-16by9 iframe {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
    }
</style>