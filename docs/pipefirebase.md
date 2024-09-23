# Pipeline de Dados com Firebase
<iframe width="560" height="315" src="https://www.youtube.com/embed/pdOwJ29PoZk?si=pRqSprbfwGUjeR0W" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
---
![imagem](https://static.wixstatic.com/media/837d8d_962fd81cd2a24fde91e4a36f223cd549~mv2.png/v1/fill/w_838,h_439,al_c,lg_1,q_90,enc_auto/837d8d_962fd81cd2a24fde91e4a36f223cd549~mv2.png)

---

![imagem](https://static.wixstatic.com/media/837d8d_0111fb6cae764deebfefcbf97ba128a4~mv2.png/v1/fill/w_838,h_590,al_c,lg_1,q_90,enc_auto/837d8d_0111fb6cae764deebfefcbf97ba128a4~mv2.png)

---

![imagem](https://static.wixstatic.com/media/837d8d_f4802f3a971f4901bb2971a4bd2b00c7~mv2.png/v1/fill/w_837,h_365,al_c,lg_1,q_85,enc_auto/837d8d_f4802f3a971f4901bb2971a4bd2b00c7~mv2.png)

Aqui está o passo a passo adaptado para ser executado diretamente no Google Colab:

### Passo 1: Configurar o Firebase no Google Colab

1. **Instalar as dependências necessárias**:
   - Execute o seguinte comando no Colab para instalar o Firebase Admin SDK:

```bash
!pip install firebase-admin
```

2. **Subir as credenciais do Firebase**:
   - Baixe a chave de credenciais (arquivo JSON) do Firebase para o seu computador.
   - Em seguida, faça o upload do arquivo JSON para o Colab

### Passo 2: Inicializar o Firebase Admin SDK

1. **Inicializar o Firebase no Colab**:
   - Após o upload do arquivo JSON, inicialize o Firebase Admin SDK:

```python
import firebase_admin
from firebase_admin import credentials, firestore, storage
import datetime

# Especificar o caminho do arquivo JSON que já está no Colab
file_path = '/content/nome-do-arquivo-json.json'

# Carregar as credenciais a partir do arquivo JSON
cred = credentials.Certificate(file_path)
firebase_admin.initialize_app(cred, {
    'storageBucket': 'your-project-id.appspot.com'
})

# Referências ao Firestore e Storage
db = firestore.client()
bucket = storage.bucket()
```

### Passo 3: Leitura dos Arquivos no Firebase Storage

1. **Listar e baixar arquivos do Storage**:
   - Implemente a função para listar e baixar arquivos do Firebase Storage:

```python
def read_files_from_storage():
    blobs = bucket.list_blobs()  # Lista de todos os arquivos no bucket
    for blob in blobs:
        file_content = blob.download_as_text()
        process_file(file_content, blob.name)
```

### Passo 4: Processamento ETL

1. **Extrair e transformar os dados**:
   - Para cada arquivo lido, faça a transformação necessária para o formato especificado:

```python
def process_file(contents, file_name):
    linhas = contents.split('\n')
    for linha in linhas:
        data_transformada = {
            'projeto': 'projeto1',  # Nome do projeto
            'data_linha': {'linha': linha},  # Linha processada do arquivo
            'tag': 'tag1',  # Tag específica
            'data_ingestao': datetime.datetime.utcnow().isoformat()  # Data de ingestão
        }
        salvar_no_firestore(data_transformada)
```

### Passo 5: Carregar os Dados no Firestore

1. **Salvar os dados transformados no Firestore**:
   - Armazene os dados no Firestore:

```python
def salvar_no_firestore(data):
    try:
        db.collection('projetos').add(data)
        print('Documento salvo com sucesso:', data)
    except Exception as e:
        print('Erro ao salvar documento:', e)
```

### Passo 6: Executar o Pipeline

1. **Executar a função de leitura dos arquivos**:
   - Chame a função principal para executar o pipeline:

```python
if __name__ == "__main__":
    read_files_from_storage()
```

### Estrutura Final dos Documentos no Firestore

Os documentos no Firestore terão a seguinte estrutura:

```json
{
  "projeto": "projeto1",
  "data_linha": {
    "linha": "conteúdo da linha do arquivo"
  },
  "tag": "tag1",
  "data_ingestao": "2024-09-15T12:34:56.789Z"
}
```

### Dicas para o Google Colab

- **Automatização**: Para fins de automação, você pode criar funções que sejam disparadas manualmente no Colab ou usar Google Cloud Functions fora do Colab.
- **Exceções e Erros**: Lembre-se de adicionar tratamento de exceções adequados para garantir que erros sejam corretamente manipulados durante o processo de download e upload dos dados.

Esse pipeline completo permite ler arquivos do Firebase Storage, transformá-los e armazenar os dados no Firestore com a data de ingestão.