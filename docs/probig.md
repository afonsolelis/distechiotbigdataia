# Aula de Projeto Prático de BigData

## Antes de Tudo

1. Vamos criar o github do seu projeto individual. Entre no seu github (ou crie se não tiver) e crie um repositório novo com o nome de: `{nome}{sobrenome}bigdatafecaf`;
2. Conecte-se com o seu github via replit;

# Vamos Iniciar a Aula

1. Baixe o dataset daqui: [link](https://www.kaggle.com/datasets/atulanandjha/temperature-readings-iot-devices/data);
2. Faça o upload para o replit;
3. Rode o seguinte comando no shell:

```shell
poetry add streamlit pandas sqlalchemy psycopg2-binary plotly python-dotenv
```

4. Crie um `.env`:

```text
DATABASE_URL=xxxxxx
```

5. Desenvolva o script em `main.py`:

```python
import streamlit as st
import pandas as pd
from sqlalchemy import create_engine
import plotly.express as px


# Função para criar conexão com o banco de dados
def get_db_connection():
	return create_engine("string de conexão")


# Função para criar tabela no PostgreSQL
def create_table(engine, df):
	df.to_sql('temperature_logs', engine, if_exists='replace', index=False)


# Upload do arquivo CSV
st.title("Upload de Arquivo CSV")
uploaded_file = st.file_uploader("Escolha um arquivo CSV", type="csv")

if uploaded_file is not None:
	# Leitura do arquivo CSV
	df = pd.read_csv(uploaded_file)
	st.write("Estrutura do Dataset:")
	st.write(df.head())

	# Conectar ao banco de dados
	engine = get_db_connection()

	# Criar tabela no PostgreSQL
	create_table(engine, df)
	st.success("Dados enviados para o banco de dados.")

	# Ler dados do banco de dados
	query = "SELECT * FROM temperature_logs"
	data = pd.read_sql(query, engine)

	# Visualização dos dados com Plotly
	st.title("Visualização dos Dados")
	fig = px.line(data,
	              x='noted_date',
	              y='temp',
	              title='Série Temporal de Temperaturas')
	st.plotly_chart(fig)
```

6. Execute o Streamlit e veja o gráfico.

7. Faça git push e depois o deploy em render.com.

## Vamos para o Recreio!

### Agora é a sua vez, inicie o projeto, e mande a url para o formulário [link](https://docs.google.com/forms/d/e/1FAIpQLSd2BXsZJz8C-4PQsLUO9XzAzj1Us2djMD0OJLuYj1-wfYxOuw/viewform?usp=sf_link)

