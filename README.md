# Perceptron para uma função lógica AND com entrada binária(1,0) e alvo bipolar(1,-1)

## 1. Descrição do projeto

Este projeto implementa, em Java, um **Perceptron** para aprender a função lógica **AND**, utilizando entradas binárias (`0` e `1`) e alvos bipolares (`1` e `-1`). O código é baseado no Exemplo 2.11, página 61, do livro *Fundamentals of Neural Networks*, de Laurene V. Fausett.

O programa treina a rede a partir de quatro padrões de entrada, ajustando os pesos e o bias sempre que a saída produzida for diferente do alvo esperado. Ao final do treinamento, permite testar os padrões por meio de caixas de diálogo.

## 2. Objetivos

- Implementar o algoritmo Perceptron em Java.
- Aprender a função lógica AND com entradas binárias e alvos bipolares.
- Inicializar pesos e bias com valores definidos.
- Aplicar uma função de ativação com três possíveis saídas: `1`, `0` e `-1`.
- Atualizar pesos e bias quando a saída for diferente do alvo.
- Registrar as informações de cada época e permitir testes interativos da rede treinada.

## 3. A função lógica AND

A função AND retorna verdadeiro somente quando as duas entradas são `1`. Neste programa, a saída desejada é representada por valores bipolares: `1` para a combinação verdadeira e `-1` para as demais combinações.

| Entrada `x1` | Entrada `x2` | Alvo |
|---:|---:|---:|
| 1 | 1 | 1 |
| 1 | 0 | -1 |
| 0 | 1 | -1 |
| 0 | 0 | -1 |

Os padrões de entrada são armazenados na matriz `s`, e os alvos correspondentes, no vetor `alvo`. A variável `num` define a quantidade de padrões de treinamento, enquanto `n` informa a quantidade de entradas por padrão.

## 4. Conceito de Perceptron

O Perceptron é um modelo de rede neural artificial que calcula uma soma ponderada das entradas e adiciona um bias. O resultado dessa soma é submetido a uma função de ativação, que determina a saída da rede.

A soma de entrada é calculada por:

\[
y_{in} = \sum_{i=1}^{n} x_i w_i + b
\]

Em que:

- `x_i` representa uma entrada;
- `w_i` representa o peso associado à entrada;
- `b` representa o bias;
- `n` é a quantidade de entradas;
- `y_in` é a soma ponderada antes da ativação.

## 5. Função de ativação

O código utiliza uma função de ativação com três possíveis resultados, considerando o parâmetro `omega` como limite de tolerância ao redor de zero.

| Condição | Saída `y` |
|---|---:|
| `y_in > omega` | `1` |
| `-omega <= y_in <= omega` | `0` |
| `y_in < -omega` | `-1` |

No programa, `omega` recebe o valor `0.2`. Assim, valores de `y_in` maiores que `0.2` produzem saída `1`; valores entre `-0.2` e `0.2`, inclusive, produzem saída `0`; e valores menores que `-0.2` produzem saída `-1`.

## 6. Regra de aprendizagem

O programa compara a saída produzida pela rede (`y`) com o alvo desejado (`t`). Se forem diferentes, os pesos e o bias são atualizados.

A atualização de cada peso é:

\[
w_i \leftarrow w_i + \alpha \cdot t \cdot x_i
\]

A atualização do bias é:

\[
b \leftarrow b + \alpha \cdot t
\]

No código, `alfa` é a taxa de aprendizagem e recebe o valor inteiro `1`. O ajuste é realizado somente quando `y != t`. Quando a saída coincide com o alvo, os parâmetros permanecem inalterados para aquele padrão.

## 7. Como o programa funciona

A implementação está concentrada no método `main` da classe `Principal`. O programa executa as seguintes etapas:

1. Define os quatro padrões binários da função AND e os alvos bipolares.
2. Define a taxa de aprendizagem, o limite da ativação e o número máximo de épocas.
3. Inicializa o bias e os pesos com zero.
4. Percorre os padrões de treinamento e calcula a soma ponderada `y_in`.
5. Aplica a função de ativação para obter `y`.
6. Compara a saída com o alvo e, se forem diferentes, atualiza os pesos e o bias.
7. Marca que houve alteração de pesos durante a época.
8. Repete o treinamento enquanto não atingir o limite de épocas e enquanto houver alterações de pesos.
9. Registra e apresenta as estatísticas do treinamento.
10. Permite ao usuário testar um dos quatro padrões por meio de caixas de diálogo.

### 7.1 Parâmetros utilizados

| Parâmetro | Valor utilizado | Significado |
|---|---:|---|
| `num` | `4` | Quantidade de padrões do conjunto de treinamento. |
| `n` | `2` | Quantidade de entradas por padrão. |
| `alfa` | `1` | Taxa de aprendizagem utilizada na atualização dos pesos e do bias. |
| `omega` | `0.2` | Limite usado pela função de ativação para definir a região em que a saída é `0`. |
| `epoca` | `10` | Número máximo de épocas de treinamento. |
| `b` | `0` | Bias inicial. |
| `w` | `{0, 0}` | Pesos iniciais das duas entradas. |
| `conta_epoca` | Inicialmente `0` | Contador das épocas executadas. |
| `alterou_peso` | Inicialmente `1` | Indica se houve alteração de pesos durante a época; permite encerrar o treinamento quando não houver atualizações. |

O treinamento termina quando são alcançadas `10` épocas ou quando uma época inteira é executada sem alterações nos pesos e no bias.

## 8. Principais métodos e recursos

O código fornecido concentra a implementação no método `main`; não há métodos auxiliares definidos na classe `Principal`.

| Método ou recurso | Responsabilidade |
|---|---|
| `main(String args[])` | Ponto de entrada. Define os dados, inicializa os parâmetros, treina o Perceptron e conduz os testes. |
| `JOptionPane.showInputDialog(...)` | Exibe caixas de diálogo para perguntar se o usuário deseja testar a rede e qual padrão deseja executar. |
| `String` e concatenação | Armazenam as estatísticas das épocas na variável `saida` para exibição ao final do treinamento. |

### 8.1 Tecnologias e ferramentas

| Tecnologia ou ferramenta | Utilização |
|---|---|
| **Java 8 (JDK 8)** | Linguagem e ambiente de desenvolvimento utilizados para implementar e executar o programa. |
| **Apache Maven** | Gerencia a estrutura do projeto, as configurações de compilação e as tarefas definidas no arquivo `pom.xml`. O código apresentado não possui dependências externas explícitas. |
| `javax.swing.JOptionPane` | Exibe caixas de diálogo para a interação com o usuário durante os testes. |
| `String` | Armazena as estatísticas de treinamento que serão apresentadas no terminal. |

## 9. Requisitos

- **JDK 8** ou versão compatível.
- **Apache Maven** instalado e configurado, caso a compilação e a execução sejam feitas por Maven.
- Ambiente com interface gráfica para utilizar as caixas de diálogo do `JOptionPane`.
- Terminal ou prompt de comando para executar os comandos Maven.

## 10. Estrutura do projeto

Considerando a estrutura convencional de um projeto Maven, os arquivos podem estar organizados da seguinte forma:

```text
perceptron-and/
├── pom.xml
├── README.md
└── src/
    └── main/
        └── java/
            └── Principal.java
```

O arquivo `Principal.java` contém o treinamento e os testes. O arquivo `pom.xml` define as configurações do projeto Maven. Se o projeto utilizar um pacote Java ou uma estrutura diferente, ajuste essa representação para corresponder à organização real dos arquivos.

## 11. Compilação e execução

Na pasta raiz do projeto, onde está localizado o arquivo `pom.xml`, execute:

```bash
mvn clean package
```

Esse comando limpa os arquivos de compilação anteriores e empacota o projeto. A forma exata de execução depende das configurações definidas no `pom.xml`.

Se o projeto estiver configurado com o plugin Maven Exec, execute:

```bash
mvn exec:java -Dexec.mainClass="Principal"
```

Se a classe `Principal` estiver dentro de um pacote, informe o nome totalmente qualificado, por exemplo `br.edu.exemplo.Principal`.

Em um projeto simples sem pacote, também é possível compilar e executar diretamente pelo JDK:

```bash
javac -d target/classes src/main/java/Principal.java
java -cp target/classes Principal
```

## 12. Saída e interação do programa

Durante o treinamento, o programa apresenta:

- Mensagem de início do treinamento.
- Número da época atual.
- Entradas, taxa de aprendizagem, soma de entrada `y_in`, saída ativada `y`, alvo, pesos e bias.
- Mensagem de término do treinamento.

Na etapa de testes, o usuário informa se deseja realizar um teste e seleciona o índice do padrão. Os índices válidos são `0`, `1`, `2` e `3`, correspondentes às quatro linhas da matriz `s` e do vetor `alvo`. O resultado apresenta o padrão escolhido, seu alvo e a saída calculada.

## 13. Observações sobre a implementação

- Os pesos e o bias começam em zero.
- O treinamento não utiliza um cálculo de erro quadrático como condição de parada. A interrupção depende da quantidade máxima de épocas e da ocorrência de atualizações dos pesos e do bias.
- A variável `alterou_peso` é definida como `1` quando há pelo menos uma atualização durante a época. No início de cada época, ela é zerada e só volta a `1` quando a saída de algum padrão difere do alvo.
- A função de ativação pode retornar `0`, mas os alvos definidos são somente `1` e `-1`. Nesse caso, a saída `0` é considerada diferente de qualquer alvo e provoca atualização dos parâmetros.
- O programa não valida os valores informados pelo usuário. O índice escolhido deve estar entre `0` e `3`, e as respostas às caixas de diálogo devem ser números inteiros válidos.
- A variável `saida` acumula as estatísticas de todas as épocas em uma única `String`, o que pode aumentar o consumo de memória em execuções mais longas.
- Embora o projeto seja descrito como Perceptron, a função de ativação com uma região de saída `0` é a regra específica implementada neste código.

## 14. Limitações

- O programa trabalha apenas com os quatro padrões definidos para a função AND com duas entradas binárias.
- O treinamento é limitado a `10` épocas.
- A região de ativação definida por `omega = 0.2` permite uma saída intermediária igual a `0`, embora os alvos sejam bipolares.
- Não há validação dos dados digitados durante os testes.
- A interface utiliza `JOptionPane`, exigindo um ambiente gráfico.
- A implementação está concentrada no método `main`, o que limita a modularidade e a reutilização do código.

## 15. Referência

FAUSETT, Laurene V. *Fundamentals of Neural Networks: Architectures, Algorithms, and Applications*. Exemplo 2.11, p. 61.