# Análise de Variância
 
A análise de variância é bastante utilizado em estatística experimental. Utiliza a hipótese de nulidade para mais de duas médias. Pode encontrar o efeito de tratamentos e a variação do acaso.

Como sabemos existem três tipos de delineamentos:

* Delineamento Inteiramente Casualizado (DIC)

* Delineamento em Blocos Casualizados (DBC)

* Delineamento em Quadrado Latino (DQL)


No exemplo da nossa apostila vamos aplicar um script para desenvolver a análise de variância de um Delineamento Inteiramente Casualizado (DIC)

https://github.com/emanuelmad/R-para-analise-de-dados/blob/main/Eucalipto3.txt

#### Delineamento Inteiramente Casualizado (DIC)

Nesse experimento vamos importar um arquivo relacionado a experimento com eucalipto em diferentes tipos de espaçamento, para isso foram delineados os seguintes tratamentos:

* **T1 = espaçamento 3x4**

* **T2 = espaçamento 3x2**

* **T3 = espaçamento 3x3**

A hipótese de pesquisa é:

***𝐻0: todas as médias dos tratamentos são iguais entre si***

***𝐻1: há pelo menos dois tratamentos cujas médias são diferentes entre si***

![image](https://user-images.githubusercontent.com/67385452/119034176-75e9a480-b984-11eb-884c-ea7e5cb18782.png)

df3 =  read.table("eucalipto3.txt", header = T, sep="") 
print(df3)

|Tratamento|   Rep|
|----------|------|
|T1 |13.53 |
|T1 |13.40 |
|T1 |12.54 |
|T1 |16.68 |
|T1 |11.94 |
|T2 |16.30 |
|T2  |5.09 |
|T2 |15.53 |
|T2 |15.88 |
|T2 |13.94 |
|T3 |11.49 |
|T3 |12.70 |
|T3 |10.98 |
|T3 |14.01 |
|T3 |13.66 |

A princípio a primeira coisa a se fazer é analisar os dados descritivos do experimento, por isso utilizaremos a função summary() para fazer uma análise exploratória de cada tratamento.

summary(df3)

|Tratamento |          |   Rep     | 
|-----------|----------|-----------|
|Length:15 | Min.:| 5.09  |
|Class :character | 1st Qu.:|12.24 | 
|Mode  :character |Median :| 13.53  |
|                     | Mean: | 13.18|  
|                     | 3rd Qu.: | 14.77 | 
|                     | Max.: | 16.68 |

Para calcular a média de cada tratamento, nesse caso é necessário criar um vetor com a função tapply.

Esta função é bastante utiizada quando nosso data frame possui uma variável categorica (tratamento), sendo assim ela agrupa os dados nos diferentes níveis da pesquisa, pois pode ser obtido a média e variância de cada tratamento do experimento.

media = tapply(df3$Rep, df3$Tratamento, mean)
print(media)

  T1     T2     T3 
13.618 13.348 12.568

Da mesma forma para a variância

var = tapply(df3$Rep, df3$Tratamento, var)
print(var)

|T1|       T2 |      T3 |
|-------|----------|----------|
 |3.35222 |22.10787|  1.74327|

É importante também aplicar o teste de homogeneidade das variâncias por meio do teste de Bartlett

bartlett.test(df3$Rep, df3$Tratamento)

Bartlett test of homogeneity of variances

data:  df3$Rep and df3$Tratamento

|Bartlett's K-squared = 6.3103| df = 2| p-value = 0.04263|

Um gráfico muito interessante que pode ser plotado para visualizar a relação entre os espaçamentos e o dap é o boxplot. 

boxplot(df3$Rep ~ df3$Tratamento, 
	main="Eucalipto", xlab="Tratamentos", ylab="DAP (cm)") 
points(media, pch=20, col=2, cex=1.5)

![image](https://user-images.githubusercontent.com/67385452/119049140-8f93e780-b996-11eb-8aa7-96314a80e4a7.png)

Você pode também adicionar cores para cada boxplot com a função col

boxplot(df3$Rep ~ df3$Tratamento,col=c("blue", "green", "yellow"), 
	main="Eucalipto", xlab="Tratamentos", ylab="DAP (cm)") 
points(media, pch=20, col=2, cex=1.8)

![image](https://user-images.githubusercontent.com/67385452/119049191-9cb0d680-b996-11eb-8147-2fc54b29c4c1.png)

Agora entraremos no cálculo da Análise de variância. Existem diversas maneiras e pacotes para essa função. Porém o próprio R em sua raiz possui a função aov().

anova.DIC = aov(df3$Rep ~ df3$Tratatamento, data=df3)

  |           | Df| Sum Sq| Mean Sq| F |value Pr(>F)|
  |-----------|---|-------|--------|---|------------|           
|df3$Tratamento| 2|   2.97|   1.486|   0.164|  0.851|
|Residuals|      12| 108.81|   9.068|  
---
Signif. codes: 0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Para visualizar os gráficos da ANOVA, basta utilizar a função plot()

plot(anova.DIC)

![image](https://user-images.githubusercontent.com/67385452/119049634-28c2fe00-b997-11eb-8371-de56c7fff95e.png)
![image](https://user-images.githubusercontent.com/67385452/119049649-2d87b200-b997-11eb-8d1b-09af0b53cc2e.png)
![image](https://user-images.githubusercontent.com/67385452/119049668-324c6600-b997-11eb-9729-d48186db8fb4.png)
 
No nosso caso, não houve diferença estatística entre os tratamentos, ou seja, aceita a hipotese de nulidade (H0), pois o Fcalculado < Ftabelado a nível de 5% de probabilidade. Isso quer dizer que os diferentes tipos de espaçamentos não influenciaram o DAP e as diferenças estão relacionadas ao acaso. 

## FIM DA ANÁLISE DO EXPERIMENTO!!!

Dessa forma não é necessário proceder com o teste de médias (Tukey), mas caso fosse, teríamos que utilizar a função TukeyHSD()

Apenas a nível de informação, supondo que o nosso experimento tivesse apresentado um Fcalculado > Ftabelado, o código ficaria da seguinte forma:

Tukey = TukeyHSD(anova.DIC) 
print(Tukey)
plot(Tukey)






