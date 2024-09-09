# Redes Neurais Aplicadas

### Aula: Séries Temporais e Previsão com Redes Neurais Recorrentes (RNN)

#### 1. Introdução às Séries Temporais

**Definição:**  
Uma **série temporal** é um conjunto de observações ordenadas no tempo. Essas observações são feitas em intervalos regulares, como horas, dias, semanas ou meses, e são muito utilizadas para modelar fenômenos que mudam com o tempo.

![imagem](https://wagon-public-datasets.s3.amazonaws.com/data-science-images/lectures/deep-learning/04/example_1.png)

**Exemplos de Séries Temporais:**
- Preço de ações ao longo do tempo
- Vendas diárias de um produto
- Temperatura registrada a cada hora
- Demanda de energia elétrica

Séries temporais possuem uma característica importante: os dados anteriores influenciam os valores futuros. Esse padrão temporal é o que torna as séries temporais diferentes de outros tipos de dados.

#### 2. Componentes das Séries Temporais

![imagem](https://wagon-public-datasets.s3.amazonaws.com/data-science-images/lectures/deep-learning/04/data_description/standard_time_series.png)

As séries temporais são compostas por quatro componentes principais:

1. **Tendência (Trend):**  
   Movimento geral da série ao longo do tempo. Pode ser crescente, decrescente ou constante.

2. **Sazonalidade (Seasonality):**  
   Padrões que se repetem em intervalos de tempo regulares (diários, mensais, anuais, etc.). Exemplo: o aumento nas vendas durante o Natal.

3. **Ciclos (Cycles):**  
   Semelhante à sazonalidade, mas os ciclos não possuem intervalos de tempo fixos. Exemplo: ciclos econômicos.

4. **Ruído (Noise):**  
   Variações aleatórias nos dados, que não seguem nenhum padrão identificável.

#### 3. Análise de Séries Temporais

Para analisar séries temporais, usamos diversas técnicas que ajudam a entender as características dos dados, identificar padrões e realizar previsões.

##### a. Visualização
A primeira etapa para analisar uma série temporal é visualizá-la. Isso ajuda a identificar a tendência, a sazonalidade e possíveis outliers.

```python
import matplotlib.pyplot as plt
plt.plot(series)
plt.title('Série Temporal ao Longo do Tempo')
plt.xlabel('Tempo')
plt.ylabel('Valor')
plt.show()
```

##### b. Decomposição da Série Temporal
A decomposição de uma série temporal separa a série em seus componentes: tendência, sazonalidade e ruído. Isso é útil para entender o comportamento de cada um desses fatores.

![imagem](https://wagon-public-datasets.s3.amazonaws.com/data-science-images/lectures/deep-learning/04/data_description/comparison.png)

```python
from statsmodels.tsa.seasonal import seasonal_decompose
result = seasonal_decompose(series, model='additive', period=12)
result.plot()
plt.show()
```

##### c. Diferença (Differencing)
Aplicamos a técnica de diferenciação para remover a tendência da série temporal. Isso torna a série estacionária, o que facilita a previsão.

```python
series_diff = series.diff().dropna()
```

#### 4. Previsão de Séries Temporais

Existem diversas formas de realizar previsões em séries temporais. Algumas das mais tradicionais são:

- **ARIMA (AutoRegressive Integrated Moving Average):** Um dos métodos mais conhecidos e eficientes para dados lineares e estacionários.
- **Exponential Smoothing (Suavização Exponencial):** Técnica usada para prever séries com sazonalidade.

Contudo, quando as séries temporais são complexas e possuem muitos dados, redes neurais recorrentes (RNNs) são uma excelente opção.

#### 5. Redes Neurais Recorrentes (RNN) para Séries Temporais

As **Redes Neurais Recorrentes (RNNs)** são um tipo especial de rede neural projetada para lidar com dados sequenciais, como séries temporais. O poder das RNNs está em sua capacidade de "memorizar" informações anteriores, o que é essencial para entender e prever padrões temporais.

##### a. Como as RNNs Funcionam?

As RNNs possuem uma estrutura em que a saída de um neurônio é alimentada de volta como entrada para o próximo neurônio na sequência. Isso permite que a rede capture dependências temporais. O loop nas RNNs permite que elas “lembrem” informações de estados anteriores, o que é crucial para previsões baseadas em séries temporais.

##### b. Limitações das RNNs
Embora poderosas, as RNNs têm limitações, especialmente quando se trata de longas dependências temporais. A medida que a sequência se torna muito longa, as informações passadas podem "se perder". Para resolver isso, variantes como LSTM (Long Short-Term Memory) e GRU (Gated Recurrent Unit) foram criadas.

#### 6. Construindo uma RNN para Previsão de Séries Temporais

Agora vamos construir um modelo de RNN para prever a demanda de um produto ao longo do tempo. Usaremos a biblioteca **Keras** para implementar o modelo.

##### a. Passo 1: Preparar os Dados
Os dados de uma série temporal precisam ser organizados em janelas de tempo (sequências) para alimentar a RNN.

```python
import numpy as np
import pandas as pd
from sklearn.preprocessing import MinMaxScaler

# Carregar os dados
data = pd.read_csv('demanda.csv')
data = data['demanda'].values.reshape(-1, 1)

# Normalizar os dados
scaler = MinMaxScaler(feature_range=(0, 1))
data_scaled = scaler.fit_transform(data)

# Criar sequências
def create_sequences(data, seq_length):
    x, y = [], []
    for i in range(len(data) - seq_length):
        x.append(data[i:i+seq_length])
        y.append(data[i+seq_length])
    return np.array(x), np.array(y)

seq_length = 10
x, y = create_sequences(data_scaled, seq_length)

# Dividir em treino e teste
train_size = int(len(x) * 0.8)
x_train, x_test = x[:train_size], x[train_size:]
y_train, y_test = y[:train_size], y[train_size:]
```

##### b. Passo 2: Construir o Modelo RNN

Usamos o Keras para construir o modelo RNN.

```python
from keras.models import Sequential
from keras.layers import SimpleRNN, Dense

# Criar o modelo
model = Sequential()

# Adicionar uma camada RNN
model.add(SimpleRNN(units=50, activation='tanh', input_shape=(seq_length, 1)))

# Adicionar uma camada densa de saída
model.add(Dense(units=1))

# Compilar o modelo
model.compile(optimizer='adam', loss='mean_squared_error')

# Treinar o modelo
model.fit(x_train, y_train, epochs=50, batch_size=32)
```

##### c. Passo 3: Fazer Previsões

Após o treinamento, podemos usar o modelo para fazer previsões.

```python
# Prever os dados de teste
y_pred = model.predict(x_test)

# Inverter a normalização para as previsões
y_pred_inverse = scaler.inverse_transform(y_pred)
y_test_inverse = scaler.inverse_transform(y_test)

# Visualizar as previsões
import matplotlib.pyplot as plt
plt.plot(y_test_inverse, color='blue', label='Demanda Real')
plt.plot(y_pred_inverse, color='red', label='Demanda Prevista')
plt.title('Previsão de Demanda com RNN')
plt.xlabel('Tempo')
plt.ylabel('Demanda')
plt.legend()
plt.show()
```

### RNN Debaixo do Capô

![imagem](https://wagon-public-datasets.s3.amazonaws.com/data-science-images/lectures/deep-learning/04/RNN_under_the_hood_full_no_seq.png)
![imagem](https://wagon-public-datasets.s3.amazonaws.com/data-science-images/06-DL/rnn_return_sequences_true.excalidraw.png)
![imagem](https://wagon-public-datasets.s3.amazonaws.com/data-science-images/lectures/deep-learning/04/sequence.png)


#### 7. Considerações Finais

- **Modelos mais complexos:** Se os dados possuem dependências temporais longas, você pode considerar usar variantes mais avançadas, como **LSTM** ou **GRU**.
- **Ajuste de Hiperparâmetros:** O número de unidades, camadas, tamanho de batch e número de épocas são parâmetros que precisam ser ajustados conforme a complexidade dos dados.
- **Escalabilidade:** RNNs podem ser escaladas e usadas para previsões em tempo real em grandes volumes de dados, dependendo da arquitetura e da capacidade computacional.


# Vamos Treinar!

### 1. Preparação dos Dados

Séries temporais geralmente consistem em uma sequência de observações em intervalos de tempo regulares, como vendas diárias ou mensais. O primeiro passo é organizar seus dados de uma forma que a RNN consiga aprender padrões temporais.

#### a. Importando as Bibliotecas Necessárias
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.preprocessing import MinMaxScaler
from keras.models import Sequential
from keras.layers import Dense, SimpleRNN
from sklearn.model_selection import train_test_split
```

#### b. Carregar os Dados
Assumindo que você tem um arquivo CSV com dados de demanda:

```python
data = pd.read_csv('demanda.csv')  # Ajuste o nome do arquivo
```

#### c. Exploração e Visualização dos Dados
```python
plt.plot(data['demanda'])
plt.title('Demanda ao longo do tempo')
plt.xlabel('Tempo')
plt.ylabel('Demanda')
plt.show()
```

#### d. Normalizar os Dados
RNNs funcionam melhor com dados normalizados (normalizados para um intervalo de 0 a 1).

```python
scaler = MinMaxScaler(feature_range=(0, 1))
data_normalized = scaler.fit_transform(data['demanda'].values.reshape(-1, 1))
```

#### e. Criar Sequências de Entrada e Saída
As RNNs precisam de sequências de entrada, então você deve transformar a série temporal em janelas de tempo.

```python
def create_sequences(data, seq_length):
    x = []
    y = []
    for i in range(len(data)-seq_length):
        x.append(data[i:i+seq_length])
        y.append(data[i+seq_length])
    return np.array(x), np.array(y)

seq_length = 10  # Janela de tempo de 10 dias, por exemplo
x, y = create_sequences(data_normalized, seq_length)

# Dividir os dados em treino e teste
x_train, x_test, y_train, y_test = train_test_split(x, y, test_size=0.2, shuffle=False)
```

### 2. Construção da Rede Neural Recorrente (RNN)

Agora, vamos construir o modelo de RNN. Para previsões de séries temporais, usaremos uma camada de RNN simples.

```python
model = Sequential()

# Camada RNN
model.add(SimpleRNN(units=50, activation='tanh', input_shape=(seq_length, 1)))

# Camada densa final
model.add(Dense(units=1))

# Compilar o modelo
model.compile(optimizer='adam', loss='mean_squared_error')
```

- `units=50`: Este é o número de células de memória na RNN. Você pode ajustar para mais ou menos unidades conforme necessário.
- `activation='tanh'`: A função de ativação `tanh` ajuda a regularizar a saída entre -1 e 1.

### 3. Treinamento do Modelo

Agora, vamos treinar o modelo. Você pode ajustar o número de épocas conforme a quantidade de dados e complexidade do problema.

```python
history = model.fit(x_train, y_train, epochs=50, batch_size=32, validation_data=(x_test, y_test))
```

### 4. Avaliação do Modelo

Podemos avaliar o desempenho do modelo e visualizar o processo de treinamento.

```python
plt.plot(history.history['loss'], label='Loss de Treino')
plt.plot(history.history['val_loss'], label='Loss de Validação')
plt.title('Perda ao longo do Treinamento')
plt.xlabel('Época')
plt.ylabel('Perda')
plt.legend()
plt.show()

# Avaliar no conjunto de teste
test_loss = model.evaluate(x_test, y_test)
print(f'Loss no conjunto de teste: {test_loss}')
```

### 5. Fazer Previsões

Agora que o modelo está treinado, vamos fazer previsões usando os dados de teste.

```python
predictions = model.predict(x_test)

# Inverter a normalização para voltar às unidades originais
predictions = scaler.inverse_transform(predictions)
y_test_inverted = scaler.inverse_transform(y_test)

# Visualizar as previsões
plt.plot(y_test_inverted, color='blue', label='Demanda Real')
plt.plot(predictions, color='red', label='Demanda Prevista')
plt.title('Previsão de Demanda')
plt.xlabel('Tempo')
plt.ylabel('Demanda')
plt.legend()
plt.show()
```

### 6. Ajustes e Melhoria

- **Unidades na RNN**: Você pode aumentar ou diminuir o número de unidades na camada RNN.
- **Camadas Empilhadas**: Adicionar mais camadas de RNN pode melhorar a capacidade de aprendizagem.
- **Parâmetros de Treinamento**: Ajustar o `batch_size`, `epochs`, e até o otimizador.

### 7. Implementação em Produção

Para previsões futuras (não apenas em dados de teste), você pode usar a saída prevista como entrada para o próximo passo:

```python
def predict_future(model, data, seq_length, future_steps):
    predictions = []
    last_sequence = data[-seq_length:]
    
    for _ in range(future_steps):
        pred = model.predict(last_sequence.reshape(1, seq_length, 1))
        predictions.append(pred)
        last_sequence = np.append(last_sequence[1:], pred)
    
    return scaler.inverse_transform(predictions)

futuro_predito = predict_future(model, data_normalized, seq_length, 30)  # Prever para 30 dias
```

### Considerações Finais

- **Hiperparâmetros**: Os hiperparâmetros, como o tamanho da sequência (`seq_length`), número de épocas, e unidades na RNN, devem ser ajustados com base nos seus dados.
- **Avaliação**: Use métricas como RMSE ou MAE para quantificar a precisão das previsões.

Esse passo a passo cobre os principais aspectos de uma RNN para previsão de séries temporais.

# Vamos fazer uma de verdade agora! Neste [Link](https://colab.research.google.com/drive/1JCISkHG0ogpPBCKQoVOuzhMjS5qISXG9?usp=sharing)

**Desafio:** Crie um RNN em casa para fazer a previsão de um arquivo que você vai procurar no Kaggle.