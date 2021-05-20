# Analisando dados em Experimentos Florestais

## Introdução

Vamos desenvolver nosso script para analisar dados relacionados a experimentos florestais;

Os dados foram obtidos por meio de inventário florestal realizado em área de experimentação de Eucalipto;

Iremos realizar uma análise exploratória dos dados com ênfase na Análise de Variância. 

## Explorando os dados pelo R
 
Para inicia,, precisamos importar nossos dados para o ambiente do RStudio. Existem duas formas de iniciarmos nossos primeiros passos, o primeiro seria utilizando a IDE do próprio R, direcionando a pasta onde estão os arquivos que se quer trabalhar. Você também pode optar por fazer essa mesma função por meio do script utilizando a função 

 Setwd

## Importando os dados

Existem diversos pacotes que possibilitam importar dados com vários formatos, exemplo que podemos importar dados em formato “.txt”, “.csv”, “.xlsx”, “.las”, “.tif”, etc.

Como nosso foco é em dados experimentais iremos trabalhar utilizando duas funções o read.csv() e read.table();

### Exemplo:

Criando um vetor com meus dados de df (Data Frame). O header é um comando que diz que seu arquivo possui nomes das variáveis na primeira coluna, então o “T”, significa True (verdadeiro). O sep””, significa que no meu arquivo os meus dados estão separados por espaço, caso fossem separados por ; ficaria da seguinte forma sep=”;”

Vocês podem acessar no seguinte repositório

https://raw.githubusercontent.com/emanuelmad/R-para-analise-de-dados/main/Eucalipto.txt

## Explorando os dados pelo R

temos então:

| Arvore |	DAP |
| -------| ------- |
|1 |	10.12 |
|2 |	15.88 |
|3 |	12.92 |
|4 |	13.75 |
|5 |	17.60 |
|6 |	12.96 |
|7 |	11.46 |
|8 |	12.48 |
|9 |	13.43 |
|10 |	11.46 |
|11 |	13.24 |
|12 |	14.80 |
|13 |	15.22 |
|14 |	14.32 |
|15 |	16.84 |
|16 |	14.23 |
|17 |	14.01 |
|18 |	15.57 |
|19 |	14.58 |
|20 |	12.83 |
|21 |	15.63 |
|22 |	15.50 |
|23 |	12.25 |
|24 |	15.25 |
|25 |	14.90 |

### Resumo estatístico dos dados

No R basta digitar o comando summary() e o nome do arquivo inserido entre parênteses

### Exemplo:

*summary(df)*

 |Arvore |               DAP   |   
 |------|----------------------|
 |Min.   : 1           | Min.: 10.12 | 
 |1st Qu.: 7         | 1st Qu.:12.92  |
 |Median :13       |Median: 14.23  |
 |Mean   :13      |  Mean: 14.05  |
 |3rd Qu.:19     |  3rd Qu.: 15.25  |
 |Max.   :25        | Max.: 17.60|

## Medidas de Posição e Dispersão
 
Caso o conjunto de dados estivesse em arquivo .csv, bastaria substituir o o read.table() por read.csv.

### Cálculo da média

Apesar de já termos feito o cálculo da média utilizando a função summary(), podemos utilizar a função mean() para obter a média do experimento. O simbolo $ significa que estou acessando a coluna DAP e quero apenas que retorne o resultado da mesma.

*mean(df$DAP)*

*[1] 14.0492*

### Cálculo da mediana

*median(df$DAP)*

*[1] 14.23*

### Cálculo da moda

Nesse caso, como não há na raiz do R uma função, é necessário instalar um pacote chamado “modeest” e a partir dai utilizar a função mfv()

*install.packages(“modeest”)*

*library(modeest)*

*mfv(df$DAP)*

*[1] 11.46*

### Cálculo da Amplitude

*max(df$DAP)-min(df$DAP)*

*[1] 7.48*

Nesse comando, você terá como retorno os valores mínimo e máximo do seu data frame

*range(df$DAP)*

*[1] 10.12 17.60*

### Cálculo da Variância

*var(df$DAP)*

*[1] 3.115683*

### Cálculo do Desvio Padrão

*sd(df$DAP)*

*[1] 1.76513*

### Cálculo do Coeficiente de Variação

*sd(df$DAP)/ mean(df$DAP)*100*

*[1] 12.56392*

## Testes de hipótese
 
Os testes de hipóteses são comumente utilizados para definir a aceitação ou rejeição de hipótese experimental;

É de onde calculamos a significância de tratamentos em função dos dados obtidos. 

Rejeitar ou aceitar uma hipótese depende da região crítica considerando a significância do teste. Geralmente é utilizado a significância de 5%.

Diante disso, valores de 𝑝 < 0,05 conduzem à rejeição da hipótese nula 𝐻0.

### Teste t 

Importando novo Data Frame agora com mais uma coluna de DAP em diferente espaçamento.

https://raw.githubusercontent.com/emanuelmad/R-para-analise-de-dados/main/Eucalipto2.txt

![image](https://user-images.githubusercontent.com/67385452/119032289-65d0c580-b982-11eb-9f05-a6c641ae6048.png)

*df2 =  read.table("eucalipto2.txt", header = T, sep="")*

*print(df2)*

|Arvore|DAP_3x3|DAP_3x4 |
|------|-------|-------|
|1|10.12|15.92 |
|2|15.88|16.49 |
|3|12.92|19.74 |
|4|13.75|18.14 |
|5|17.60|10.66 |
|6|12.96|12.48 |
|7|11.46|16.90 |
|8|12.48|14.32 |
|9|13.43|15.02 |
|10|11.46|17.79 |
|11|13.24|14.90 |
|12|14.80|14.96 |
|13|15.22|17.09 |
|14|14.32|15.60 |
|15|16.84|16.74 |
|16|14.23|16.39 |
|17|14.01|18.43 |
|18|15.57|15.69 |
|19|14.58|15.02 |
|20|12.83|16.74 |
|21|15.63|13.88 |
|22|15.50|15.98 |
|23|12.25|16.93 |
|24|15.25|13.37 |
|25|14.90|13.78 |

Paired t-test

data:  df2$DAP_3x3 and df2$DAP_3x4
t = -2.686, df = 24, p-value = 0.01291
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -2.951809 -0.386591
sample estimates:
mean of the differences 
                -1.6692

Ao analisar o resultado do teste-t nota-se que existe diferença significativa entre os dois DAP’s (p-valor < 0,05. Rejeita-se 𝐻0), logo pode ser considerado que o tipo de espaçamento influencia no crescimento do DAP para a mesma espécie. 


![image](https://user-images.githubusercontent.com/67385452/119033020-1dfe6e00-b983-11eb-9fa0-d824a228c24f.png)



















