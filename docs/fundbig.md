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

---

# Ferramentas que Iremos Utilizar Para a Nossa Aplicação

## Introdução ao Tkinter

### Conceitos Básicos

Tkinter é a biblioteca padrão do Python para a criação de interfaces gráficas (GUIs). É uma das opções mais populares devido à sua simplicidade e integração direta com o Python.

### Principais Características

- **Simplicidade**: Fácil de aprender e usar.
- **Integração**: Faz parte da biblioteca padrão do Python.
- **Componentes**: Oferece uma variedade de widgets (botões, labels, entradas de texto, etc.).
- **Compatibilidade**: Funciona em várias plataformas (Windows, macOS, Linux).

## Widgets Comuns

- **Label**: Exibe texto ou imagens.
- **Button**: Botão que pode executar uma ação quando clicado.
- **Entry**: Campo para entrada de texto.
- **Text**: Campo de texto multi-linhas.
- **Frame**: Contêiner para organizar outros widgets.
- **Canvas**: Área para desenhar formas, gráficos e imagens.
- **Menu**: Barras de menu e menus pop-up.

## Exemplos de Uso do `pack()`

### Método `pack()`

O método `pack()` é um dos três gerenciadores de layout (também conhecidos como geometry managers) oferecidos pelo Tkinter, sendo os outros dois `grid()` e `place()`. O `pack()` organiza widgets dentro de um contêiner (como uma janela ou um frame) de forma sequencial, uma após a outra, com base na ordem de inclusão.

### Características do `pack()`

- **Simplicidade**: É o método mais simples e rápido de usar.
- **Organização**: Organiza widgets em blocos, que podem ser empilhados vertical ou horizontalmente.
- **Personalização**: Permite ajustes de preenchimento, margens e alinhamento.

### Parâmetros Principais

- **side**: Especifica o lado do contêiner onde o widget será ancorado. Valores possíveis: `TOP` (padrão), `BOTTOM`, `LEFT`, `RIGHT`.
  
  ```python
  widget.pack(side=tk.LEFT)
  ```

- **fill**: Define se e como o widget deve preencher o espaço disponível. Valores possíveis: `NONE` (padrão), `X`, `Y`, `BOTH`.
  
  ```python
  widget.pack(fill=tk.BOTH)
  ```

- **expand**: Se verdadeiro (`True`), permite que o widget se expanda para usar o espaço não utilizado no contêiner.
  
  ```python
  widget.pack(expand=True)
  ```

- **padx** e **pady**: Adiciona espaço (padding) ao redor do widget, na direção horizontal (`padx`) e vertical (`pady`).
  
  ```python
  widget.pack(padx=10, pady=5)
  ```

- **anchor**: Especifica onde o widget será ancorado dentro do espaço alocado. Valores possíveis: `N`, `S`, `E`, `W`, `NE`, `NW`, `SE`, `SW`, `CENTER` (padrão).
  
  ```python
  widget.pack(anchor=tk.CENTER)
  ```

## Gerenciamento de Layout

- **Pack**: Organiza widgets em blocos antes ou depois uns dos outros.
- **Grid**: Organiza widgets em uma grade.
- **Place**: Organiza widgets em posições absolutas.

## Eventos

Eventos são ações ou ocorrências detectadas por um programa. Eventos podem ser acionados por interações do usuário (como cliques de mouse, pressionamentos de teclas), mudanças de estado do sistema, ou outras atividades que o programa está monitorando. Em Python, especialmente em interfaces gráficas (GUIs), eventos são frequentemente utilizados para permitir a interação do usuário com a aplicação.

### Sistema de Eventos

- **Emissor de Eventos**: O componente que gera um evento.
- **Ouvinte de Eventos (Event Listener)**: O componente que aguarda a ocorrência de um evento específico.
- **Manipulador de Eventos (Event Handler)**: A função ou método que é chamado em resposta a um evento.

### Eventos Comuns

- `<Button-1>`: Clique do botão esquerdo do mouse.
- `<Button-3>`: Clique do botão direito do mouse.
- `<Key>`: Qualquer tecla pressionada.
- `<Return>`: A tecla Enter/Return pressionada.
- `<Motion>`: Movimento do mouse.

## Características do `mainloop()`

- **Responsividade**: Mantém a interface gráfica ativa e pronta para responder a eventos.
- **Bloqueante**: O método `mainloop()` é bloqueante, ou seja, o código após a chamada deste método não será executado até que a janela seja fechada.
- **Eventos**: Gere eventos como cliques, teclas pressionadas, movimentação do mouse, etc., permitindo que a interface gráfica interaja com o usuário.

### Comportamento do `mainloop()`

- **Inicialização**: Quando `mainloop()` é chamado, ele inicializa o loop de eventos do Tkinter.
- **Eventos**: O loop de eventos aguarda e despacha eventos, como cliques de mouse e teclas pressionadas.
- **Interrupção**: O loop é interrompido quando a janela principal é fechada pelo usuário.

## Exemplos Práticos

### Criando uma Janela Simples

```python
import tkinter as tk

# Criação da janela principal
root = tk.Tk()
root.title("Minha Primeira Janela")

# Rótulo
label = tk.Label(root, text="Olá, Tkinter!")
label.pack()

# Botão
button = tk.Button(root, text="Clique Aqui")
button.pack()

# Iniciando o mainloop
root.mainloop()
```

### Entrada de Texto e Botão

```python
import tkinter as tk

# Função para exibir o texto da entrada
def mostrar_texto():
    texto = entrada.get()
    label['text'] = texto

# Criação da janela principal
root = tk.Tk()
root.title("Entrada de Texto")

# Entrada de Texto
entrada = tk.Entry(root)
entrada.pack()

# Botão
button = tk.Button(root, text="Mostrar Texto", command=mostrar_texto)
button.pack()

# Rótulo
label = tk.Label(root, text="")
label.pack()

# Iniciando o mainloop
root.mainloop()
```

### Área de Desenho (Canvas)

```python
import tkinter as tk

# Criação da janela principal
root = tk.Tk()
root.title("Canvas")

# Canvas
canvas = tk.Canvas(root, width=400, height=300)
canvas.pack()

# Desenhando um retângulo
canvas.create_rectangle(50, 50, 200, 150, fill="blue")

# Iniciando o mainloop
root.mainloop()
```

## Introdução ao PyInstaller

### O que é PyInstaller?

PyInstaller é uma ferramenta poderosa que converte scripts Python em executáveis autônomos (Windows, macOS e Linux). Com PyInstaller, você pode distribuir suas aplicações Python sem precisar instalar o interpretador Python nas máquinas dos usuários.

### Funcionalidades Principais

- **Criação de Executáveis**: Converte scripts Python em arquivos executáveis.
- **Autônomos**: Inclui o interpretador Python e todas as dependências necessárias.
- **Multiplataforma**: Suporte para Windows, macOS e Linux.
- **Múltiplos Arquivos de Entrada**: Suporte para aplicativos que consistem em vários módulos e pacotes.

### Instalação do PyInstaller

PyInstaller pode ser instalado via `pip`:

```sh
pip install pyinstaller
```

### Uso Básico do PyInstaller

Para criar um executável de um script Python, basta usar o comando:

```sh
pyinstaller your-script.py
```

Por padrão, este comando cria um diretório `dist` contendo o executável e todas as bibliotecas necessárias.

### Exemplos de Uso

- **Criar um Executável Simples**:

  ```sh
  pyinstaller hello.py
  ```

- **Criar um Executável Único (um único arquivo)**:

  ```sh
  pyinstaller --onefile hello.py
  ```

- **Criar um Executável sem Console e com um Ícone Personalizado**:

  ```sh
  pyinstaller --onefile --noconsole --icon=icon.ico hello.py
  ```

- **Incluir Arquivos de Dados Externos**:

  Quando sua aplicação depende de arquivos de dados externos, como arquivos de configuração, imagens, ou qualquer outro tipo de recurso, você pode incluí-los no executável usando a opção `--add-data`.

  ```sh
  pyinstaller --onefile --add-data 'source_path:destination_path' your-script.py
  ```

### Opções Comuns

- **--onefile**: Cria um único arquivo executável.
- **--noconsole**: (ou `--windowed` em Windows/macOS) Executa a aplicação sem abrir uma janela de terminal/console.
- **--name**: Define o nome do executável.
- **--icon**: Especifica um ícone para o executável.

### Importações Dinâmicas

Algumas bibliotecas podem utilizar importações dinâmicas que não são detectadas automaticamente pelo PyInstaller. Nesses casos, você pode especificar essas importações manualmente com a opção `--hidden-import`.

```sh
pyinstaller --onefile --hidden-import 'module_name' your-script.py
```

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

# Prática

## Passo a Passo: Criação de uma Aplicação Simples com Tkinter e PyInstaller

### 1. Instalação do Python

Certifique-se de ter o Python instalado em sua máquina. Você pode baixá-lo do site oficial [python.org](https://www.python.org/).

### 2. Criando o Script Tkinter

Crie um arquivo Python chamado `app.py` e adicione o seguinte código:

```python
import tkinter as tk

def mostrar_texto():
    texto = entrada.get()
    label.config(text=texto)

# Criação da janela principal
root = tk.Tk()
root.title("Minha Aplicação Tkinter")

# Entrada de Texto
entrada = tk.Entry(root)
entrada.pack(padx=10, pady=10)

# Botão
botao = tk.Button(root, text="Mostrar Texto", command=mostrar_texto)
botao.pack(padx=10, pady=10)

# Rótulo
label = tk.Label(root, text="")
label.pack(padx=10, pady=10)

# Iniciando o mainloop
root.mainloop()
```

Este script cria uma janela simples com um campo de entrada de texto, um botão e um rótulo que exibe o texto inserido.

### 3. Executando o Script

Para testar a aplicação, execute o script com o comando:

```sh
python app.py
```

### 4. Instalação do PyInstaller

Instale o PyInstaller usando o `pip`:

```sh
pip install pyinstaller
```

### 5. Criando o Executável

Para criar um executável básico, use o comando:

```sh
pyinstaller app.py
```

Este comando cria um diretório `dist` contendo o executável e todas as bibliotecas necessárias.

### 6. Criando um Executável Único

Para criar um único arquivo executável, use a opção `--onefile`:

```sh
pyinstaller --onefile app.py
```

### 7. Criando um Executável sem Console e com Ícone Personalizado

Para criar um executável que não abre uma janela de console e usa um ícone personalizado, você precisa garantir que o arquivo de ícone (`icon.ico`) esteja no caminho correto. Coloque o arquivo `icon.ico` no mesmo diretório que o seu script `app.py`. Em seguida, use as opções `--noconsole` e `--icon`:

```sh
pyinstaller --onefile --noconsole --icon=icon.ico app.py
```

### 8. Solução para Problemas de Compatibilidade com Python 3.12

Se você encontrar problemas de compatibilidade com a versão do Python, como mostrado na mensagem de erro:

```sh
The current project's supported Python range (>=3.12,<4.0) is not compatible with some of the required packages Python requirement:
  - pyinstaller requires Python <3.13,>=3.8, so it will not be satisfied for Python >=3.13,<4.0
```

Você pode ajustar a versão do Python utilizada no seu projeto. Uma maneira de fazer isso é criar um ambiente virtual com uma versão compatível do Python. Certifique-se de que a versão do Python instalada é compatível com PyInstaller (por exemplo, Python 3.11).

### 9. Criando um Ambiente Virtual com uma Versão Específica do Python

Se você estiver usando `pyenv` ou `virtualenv`, pode criar um ambiente virtual com uma versão específica do Python. Exemplo com `pyenv`:

```sh
pyenv install 3.11.4
pyenv virtualenv 3.11.4 myenv
pyenv activate myenv
```

Ou com `virtualenv`:

```sh
virtualenv -p python3.11 myenv
source myenv/bin/activate  # No Windows, use `myenv\Scripts\activate`
```

### 10. Instalando Dependências no Ambiente Virtual

Depois de ativar o ambiente virtual, instale as dependências necessárias:

```sh
pip install pyinstaller
```

### 11. Criando o Executável no Ambiente Virtual

Agora, crie o executável usando o PyInstaller no ambiente virtual:

```sh
pyinstaller --onefile --noconsole --icon=icon.ico app.py
```

## Conclusão

Neste passo a passo, criamos uma aplicação simples usando Tkinter e a convertimos em um executável utilizando PyInstaller. Também abordamos como resolver problemas de compatibilidade de versão do Python usando ambientes virtuais e como garantir que o arquivo de ícone esteja no caminho correto. Com esses conhecimentos, você pode desenvolver e distribuir suas próprias aplicações Python com interfaces gráficas de forma eficiente.

## Referências

- [Documentação do Tkinter](https://docs.python.org/3/library/tkinter.html)
- [Documentação do PyInstaller](https://pyinstaller.readthedocs.io/en/stable/)
- [Python Virtual Environments](https://docs.python.org/3/tutorial/venv.html)