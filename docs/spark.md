# Processamento de Dados com Apache Spark

![spark](https://www.databricks.com/en-website-assets/static/5e953f5a26d3e6b7949bff788ef5a2af/largest-open-source-apache-spark1679038543.png)

#### Introdução ao Apache Spark

O Apache Spark é um mecanismo de processamento de dados de código aberto projetado para lidar com grandes volumes de dados de forma rápida e eficiente. Ele foi desenvolvido para superar as limitações do MapReduce, um modelo de programação utilizado no Hadoop, proporcionando maior desempenho ao realizar cálculos na memória em vez de no disco[1][3].

#### Componentes Principais do Spark

1. **Spark Core**: É o núcleo do Spark, responsável pelo processamento de dados paralelo. Ele lida com agendamento, otimização, e abstração de dados através de RDDs (Resilient Distributed Datasets), que são coleções imutáveis e distribuídas de objetos processáveis em paralelo[1][3].

2. **Spark SQL**: Permite consultas em dados estruturados usando DataFrames, que são uma abstração sobre RDDs. Ele suporta integração com armazenamentos de dados SQL, como Apache Hive[1].

3. **Spark Streaming**: Oferece processamento de dados em tempo real, ingerindo dados em minilotes e permitindo análises de streaming[2].

4. **MLlib**: Biblioteca de aprendizado de máquina que fornece algoritmos otimizados para processamento em larga escala[1].

5. **GraphX**: Framework para processamento de gráficos, permitindo ETL, análise exploratória e computação gráfica iterativa[2].

### Como Funciona

![como funciona](https://res.cloudinary.com/dyhjjms8y/image/upload/v1723481030/Captura_de_tela_2024-08-12_134337_f2dzwr.png)

![spark](https://arquivo.devmedia.com.br/artigos/Eduardo_Zambom/spark/image002.jpg)

#### Vantagens do Apache Spark

- **Processamento em Memória**: O Spark realiza cálculos na memória, o que reduz a latência e aumenta a velocidade do processamento em comparação com sistemas baseados em disco[1][3].
- **Suporte a Múltiplas Linguagens**: Oferece APIs em Java, Scala, Python e R, tornando-o acessível para diferentes perfis de desenvolvedores[5].
- **Escalabilidade**: Capaz de processar grandes volumes de dados distribuídos entre muitos computadores[5].

#### Introdução ao PySpark

PySpark é a interface do Apache Spark para a linguagem de programação Python. Ele permite que desenvolvedores usem o poder do Spark com a simplicidade e a popularidade do Python. PySpark é amplamente utilizado para tarefas de processamento de dados, aprendizado de máquina e análise de dados em larga escala.

#### Funcionalidades do PySpark

- **DataFrames e SQL**: Assim como no Spark SQL, PySpark suporta operações em DataFrames, permitindo consultas SQL diretamente em dados estruturados.
- **Machine Learning com MLlib**: PySpark oferece suporte à biblioteca MLlib, permitindo a implementação de algoritmos de aprendizado de máquina em grandes conjuntos de dados.
- **Streaming e Gráficos**: Com PySpark, é possível realizar processamento de dados em tempo real e trabalhar com gráficos usando as bibliotecas Spark Streaming e GraphX.

Citations:
[1] https://www.ibm.com/br-pt/topics/apache-spark
[2] https://aws.amazon.com/pt/what-is/apache-spark/
[3] https://www.activebi.com.br/post/apache-spark-ferramenta-poderosa-para-processamento-de-dados-em-big-data/71
[4] https://www.cnj.jus.br/formacao-e-capacitacao/curso-de-ciencia-de-dados-aplicada-ao-poder-judiciario/spark-distribuicao-e-processamento-de-dados/
[5] https://blog.dsacademy.com.br/vantagens-e-desvantagens-do-apache-spark/

# Prática - Vamos Rodar um Spark

1. Crie uma estrutura assim:
```
/csv
/parquet
/work
  └── notebook.ipynb
Dockerfile
docker-compose.yml
```

2. Crie um `docker-compose.yml`

```yml
version: '3.8'

services:
  jupyter:
    build: .
    ports:
      - "8888:8888"   # Porta para o Jupyter Notebook
      - "4040:4040"   # Porta para o Spark UI
    volumes:
      - ./csv:/home/jovyan/work/csv
      - ./parquet:/home/jovyan/work/parquet
      - ./work:/home/jovyan/work
```

3. Crie um `Dockerfile`

```yml
FROM jupyter/pyspark-notebook:spark-3.3.0

# Define o diretório de trabalho
WORKDIR /home/jovyan/work
```

4. Inicialize o docker:

```bash
docker-compose up
```

- Não se esqueça de pegar o token para entrar no `localhost:8888`

5. Copie o seguinte código:

```python
from pyspark.sql import SparkSession
import time

# Criação da SparkSession
spark = SparkSession.builder \
    .appName("CSV to Parquet") \
    .getOrCreate()

# Caminhos dos arquivos
csv_path = "csv/inventory_dataset.csv"
parquet_path = "parquet/inventory_dataset.parquet"

# Início do tempo de leitura
start_time = time.time()

# Leitura do arquivo CSV
df = spark.read.csv(csv_path, header=True, inferSchema=True)

# Fim do tempo de leitura
read_time = time.time() - start_time
print(f"Tempo de leitura do CSV: {read_time} segundos")

# Início do tempo de escrita
start_time = time.time()

# Escrita do DataFrame em formato Parquet
df.write.parquet(parquet_path)

# Fim do tempo de escrita
write_time = time.time() - start_time
print(f"Tempo de escrita em Parquet: {write_time} segundos")

# Parar a SparkSession
spark.stop()
```

6. Tem que ter o arquivo de 3.7gb `inventory_dataset.csv` na pasta `csv`.
7. Verificar o arquivo `parquet`.

# Agora teste sem o spark

```python
import pandas as pd
import time

# Caminhos dos arquivos
csv_path = "csv/inventory_dataset.csv"
parquet_path = "parquet/inventory_dataset_pandas.parquet"

# Início do tempo de leitura
start_time = time.time()

# Leitura do arquivo CSV usando Pandas
df = pd.read_csv(csv_path)

# Fim do tempo de leitura
read_time = time.time() - start_time
print(f"Tempo de leitura do CSV com Pandas: {read_time} segundos")

# Início do tempo de escrita
start_time = time.time()

# Escrita do DataFrame em formato Parquet usando Pandas
df.to_parquet(parquet_path, engine='pyarrow')

# Fim do tempo de escrita
write_time = time.time() - start_time
print(f"Tempo de escrita em Parquet com Pandas: {write_time} segundos")
```

# Discuta: O que é diferente?


