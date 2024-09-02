Vou ajustar as fórmulas para que fiquem formatadas corretamente em LaTeX.

### 1. Introdução à Inteligência Artificial (IA)

A Inteligência Artificial (IA) é um ramo da ciência da computação que se concentra em criar sistemas capazes de realizar tarefas que, normalmente, exigiriam inteligência humana. Essas tarefas incluem reconhecimento de fala, aprendizado, planejamento e resolução de problemas.

IA pode ser dividida em duas categorias principais:

- **IA Estreita (Narrow AI)**: Projetada para executar uma tarefa específica, como reconhecimento de imagem ou processamento de linguagem natural. Exemplo: assistentes virtuais como Siri ou Alexa.
- **IA Geral (General AI)**: Uma IA que poderia executar qualquer tarefa cognitiva que um ser humano pode. Este nível de IA ainda está no campo teórico e não foi alcançado.

### 2. O que é um Perceptron

Um **perceptron** é um modelo matemático que tenta simular o comportamento de um neurônio biológico. Ele é o bloco de construção básico das redes neurais artificiais. O perceptron recebe múltiplas entradas, aplica pesos a elas, soma essas entradas ponderadas e, em seguida, passa o resultado através de uma função de ativação para produzir uma saída.

A fórmula básica do perceptron é:

![perceptron](https://media.licdn.com/dms/image/v2/D4D12AQHJK385DbGo2g/article-inline_image-shrink_1500_2232/article-inline_image-shrink_1500_2232/0/1686888552617?e=1730937600&v=beta&t=6Y3J8bXsv5tJkGg59gTaO7WVsc5c4lI2u_YG1I85CNE)

![formula](https://media.licdn.com/dms/image/v2/D4D12AQHFDLpAut87Ag/article-inline_image-shrink_1500_2232/article-inline_image-shrink_1500_2232/0/1686924043256?e=1730937600&v=beta&t=tREBkmt34Kn4Kp8clGsQlSqu33hAYho8uXEHeoTHPQw)


### 3. Implementação de um Perceptron em Python

Vamos implementar um perceptron simples que aprende a realizar uma operação lógica AND. A operação AND retorna 1 se ambas as entradas forem 1, caso contrário, retorna 0.

```python
import numpy as np

# Função de ativação - Degrau
def step_function(x):
    return 1 if x >= 0 else 0

# Classe Perceptron
class Perceptron:
    def __init__(self, input_size, learning_rate=0.1, epochs=1000):
        self.weights = np.zeros(input_size + 1)  # Pesos inicializados com 0
        self.learning_rate = learning_rate
        self.epochs = epochs

    def predict(self, x):
        # Adiciona o bias (termo de interceptação)
        x = np.insert(x, 0, 1)
        # Calcula a soma ponderada e aplica a função de ativação
        weighted_sum = np.dot(self.weights, x)
        return step_function(weighted_sum)

    def fit(self, X, y):
        # Treinamento do perceptron
        for _ in range(self.epochs):
            for i in range(y.size):
                prediction = self.predict(X[i])
                # Calcula o erro
                error = y[i] - prediction
                # Atualiza os pesos
                self.weights[1:] += self.learning_rate * error * X[i]
                self.weights[0] += self.learning_rate * error

# Dados de treinamento para a operação AND
X = np.array([
    [0, 0],
    [0, 1],
    [1, 0],
    [1, 1]
])

# Labels correspondentes
y = np.array([0, 0, 0, 1])

# Cria o perceptron
perceptron = Perceptron(input_size=2)

# Treina o perceptron
perceptron.fit(X, y)

# Testa o perceptron
print("Pesos finais:", perceptron.weights)
print("Predição para [0, 0]:", perceptron.predict([0, 0]))
print("Predição para [0, 1]:", perceptron.predict([0, 1]))
print("Predição para [1, 0]:", perceptron.predict([1, 0]))
print("Predição para [1, 1]:", perceptron.predict([1, 1]))
```

### Explicação do Código

- **Função de Ativação**: Utilizamos uma função degrau simples que retorna 1 se a entrada é maior ou igual a 0, caso contrário retorna 0.
- **Classe Perceptron**: Esta classe define o perceptron. O método `__init__` inicializa os pesos, a taxa de aprendizado, e o número de épocas. O método `predict` calcula a saída do perceptron, e o método `fit` ajusta os pesos durante o treinamento.
- **Treinamento**: O perceptron é treinado utilizando o algoritmo de aprendizado supervisionado, onde os pesos são atualizados de acordo com o erro (diferença entre a previsão e o valor real).

### Testando o Perceptron

Após o treinamento, o perceptron deve ser capaz de prever corretamente o resultado da operação AND:

```
Pesos finais: [bias, peso1, peso2]
Predição para [0, 0]: 0
Predição para [0, 1]: 0
Predição para [1, 0]: 0
Predição para [1, 1]: 1
```

Vamos avançar um pouco mais e utilizar um dataset mais complexo para demonstrar o uso de um perceptron na classificação de vinhos. Usaremos o dataset de vinhos disponível na biblioteca `scikit-learn`, que contém características químicas de diferentes tipos de vinho e os classifica em três categorias.

### Implementação com o Dataset de Vinho

1. **Importar as Bibliotecas Necessárias**: Vamos usar o `scikit-learn` para carregar o dataset e realizar a separação dos dados.
2. **Pré-processamento dos Dados**: Normalizar os dados para melhorar o desempenho do perceptron.
3. **Implementar o Perceptron com `scikit-learn`**: Utilizar a classe `Perceptron` do `scikit-learn`.
4. **Treinar o Modelo**: Usar uma parte dos dados para treinar o modelo.
5. **Avaliar o Modelo**: Testar o modelo com os dados de teste e avaliar sua acurácia.

### 1. Importar as Bibliotecas Necessárias

Vamos começar importando as bibliotecas:

```python
import numpy as np
from sklearn.datasets import load_wine
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import Perceptron
from sklearn.metrics import accuracy_score, classification_report
```

### 2. Carregar e Pré-processar o Dataset

Carregar o dataset de vinhos e dividir em conjuntos de treinamento e teste:

```python
# Carregar o dataset de vinhos
data = load_wine()
X = data.data
y = data.target

# Dividir o dataset em conjuntos de treinamento e teste
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Normalizar os dados
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)
```

### 3. Implementar o Perceptron com `scikit-learn`

Agora vamos utilizar a implementação de perceptron da biblioteca `scikit-learn`:

```python
# Criar o modelo Perceptron
model = Perceptron(max_iter=1000, eta0=0.1, random_state=42)

# Treinar o modelo
model.fit(X_train, y_train)
```

### 4. Treinar o Modelo

O treinamento é feito utilizando o método `.fit()` que ajusta o modelo aos dados de treinamento.

```python
# Prever nos dados de teste
y_pred = model.predict(X_test)
```

### 5. Avaliar o Modelo

Podemos calcular a acurácia do modelo e imprimir um relatório de classificação:

```python
# Avaliar o modelo
accuracy = accuracy_score(y_test, y_pred)
print(f"Acurácia do modelo: {accuracy:.2f}")

# Relatório de classificação
print("Relatório de Classificação:\n", classification_report(y_test, y_pred, target_names=data.target_names))
```

### Explicação do Código

- **Dataset de Vinho**: O dataset contém 13 características químicas de diferentes vinhos, classificados em três categorias (classes).
- **Pré-processamento**: Normalizamos os dados utilizando `StandardScaler` para que todas as características tenham a mesma escala, o que é importante para o treinamento do perceptron.
- **Perceptron**: Utilizamos o perceptron do `scikit-learn`, que é uma implementação otimizada e eficiente do perceptron.
- **Acurácia**: Calculamos a acurácia para medir a porcentagem de previsões corretas feitas pelo modelo.

### Resultados Esperados

O perceptron deve ser capaz de classificar o vinho em uma das três categorias com uma acurácia razoável. O resultado pode variar dependendo da aleatoriedade no `train_test_split` e da inicialização dos pesos no perceptron.

Exemplo de saída esperada:

```
Acurácia do modelo: 0.96
Relatório

 de Classificação:
               precision    recall  f1-score   support

    class_0       0.97      1.00      0.99        16
    class_1       0.97      0.88      0.92        25
    class_2       0.94      1.00      0.97        13

accuracy                           0.96        54
macro avg       0.96      0.96      0.96        54
weighted avg    0.96      0.96      0.96        54
```

## Missão!

Refaça os passos desta [publicação](https://www.linkedin.com/pulse/perceptron-fundamentos-funcionamento-e-aplica%C3%A7%C3%B5es-naomi-lago-/). Qual a pegada? Tem que achar este dataset na internet ou um similar. Procure no [Kaggle](https://www.kaggle.com/datasets)