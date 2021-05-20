# Delineamento em Blocos Casualizados (DBC)

Nesse experimento vamos importar um arquivo relacionado a comprimento de raízes (cm) de mudas de eucalipto de um experimento conduzido no DBC com 3 repetições, onde foram avaliados sete tratamentos. 

https://raw.githubusercontent.com/emanuelmad/R-para-analise-de-dados/main/DBC.txt

Os tratamentos foram:

**T1 = testemunha (sem produto para enraizamento)**
**T2 = Produto A**
**T3 = Produto B**
**T4 = Produto C**
**T5 = Produto D**
**T6 = Produto E**
**T7 = produto F**

**Bloco 1 = A**
**Bloco 2 = B**
**Bloco 3 = C**

A hipótese de pesquisa é:

### Tratamentos

*𝐻0: todas as médias dos tratamentos são iguais entre si*
*𝐻1: há pelo menos dois tratamentos cujas médias são diferentes entre si* 

### Blocos

*H0: blocos não heterogêneos*
*H1: blocos heterogêneos*

Nesse experimento iremos utilizar os seguintes pacotes

- [x] install.packages("agricolae")
- [x] install.packages("gtools")
- [x] install.packages("lmtest")
- [x] install.packages("hnp")
- [x] require(agricolae)
- [x] require(gtools)
- [x] require(lmtest)
- [x] require(hnp)

**Lembrem-se de instalar e depois utilizar o library ou require para ativar.**

Criando nosso dafa frame

*df =  read.table("DBC.txt", header = T, sep="")* 
*print(df)*

  | Tratamento| Bloco| Raiz|
  |-----------|------|-----|
   |T1     |A   |10|
   |T1     |B   |12|
   |T1     |C    |8|
   |T2     |A   |12|
   |T2     |B   |13|
   |T2     |C    |8|
   |T3     |A   |12|
   |T3     |B   |11|
   |T3     |C    |7|
   |T4     |A   |13|
   |T4     |B   |13|
   |T4     |C   |16|
   |T5     |A   |13|
   |T5     |B   |17|
   |T5     |C   |15|
   |T6     |A   |17|
   |T6     |B   |15|
   |T6     |C   |13|
   |T7     |A   |18|
   |T7     |B   |16|
   |T7     |C   |14|

Para ver nossa análise dos dados utilizar a função summary:

*summary(df)

|Tratamento|Bloco|         |Raiz|
|---------------------|-------------------|---------|-------|
|Length:21|Length:21| Min.   :| 7 | 
|Class :character|Class :character|1st Qu.:|12| 
|Mode  :character   |Mode  :character   |Median :|13| 
| -             |     -     |  Mean   :|13| 
| -           |       -     |  3rd Qu.:|15| 
|  -      |       -      | Max.   :|18 | 

Agora veremos os dados de forma a abranger as categorias de tratamentos e blocos

*mediatrat = tapply(df$Raiz, df$Tratamento, mean)
*print(mediatrat)

|T1| T2| T3| T4| T5| T6| T7 |
|---|---|---|---|---|---|---|
|10| 11| 10| 14| 15| 15| 16|

*mediabloco = tapply(df$Raiz, df$Bloco, mean)*
*print(mediabloco)*

 |    A |       B |       C |
 |----|---------|-----------|
|13.57143| 13.85714| 11.57143|

*vartrat = tapply(df$Raiz, df$Tratamento, var)*
*print(vartrat)*

|T1 |T2| T3| T4| T5| T6| T7| 
|---|---|------|---|---|---|---|
| 4|  7|  7|  3|  4|  4|  4|

*varbloco = tapply(df$Raiz, df$Bloco, var)*
*print(varbloco)*

 |   A |        B|         C| 
 |----|---------|-----------|
| 8.285714|  4.809524| 14.285714|

*sdtrat = tapply(df$Raiz, df$Tratamento, sd)*
*print(sdtrat)*

 |  T1 |      T2 |      T3|       T4|       T5|       T6|       T7| 
 |---|---|------|---|---|---|---|
|2.000000| 2.645751| 2.645751| 1.732051| 2.000000| 2.000000| 2.000000|

*sdbloco = tapply(df$Raiz, df$Bloco, sd)*
*print(sdbloco)*

|A        |B        |C |
|----|---------|-----------|
|2.878492 |2.193063 |3.779645|

*cvtrat = (sdtrat/mediatrat)*100*
*cvtrat*

|T1|       T2|       T3|       T4|       T5|       T6|       T7|
|---|---|------|---|---|---|---|
|20.00000| 24.05228| 26.45751| 12.37179| 13.33333| 13.33333| 12.50000|

*cvbloco = (sdbloco/mediabloco)*100*
*cvbloco*
 
 |A   |     B  |      C |
 |----|---------|-----------|
|21.20994| 15.82623| 32.66360|

Após algumas análises estatísticas das principais medidas do nosso banco de dados, vamos fazer a análise de variância para esse experimento.

Primeiro habilitando o acesso ao nosso data frame e depois utilizando a função aov da raiz do R.

*attach(df)*
*anova=aov(Raiz~Tratamento+Bloco)*
*summary(anova)*

|FV	|GL (df)|	SQ (Sum Sq)|	QM (Mean Sq)|	F	Pr(>F)|
|----|-----|------------|---------------|--------|
|Tratamento|	6|	120	|20|	5.419|	0.00636 **|
|Bloco|	2|	21.71|	10.86|	2.942|	0.09127|
|Resíduo|	12|	44.29|	3.69|		
Total|	20|	186|			|
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1


**Resultado dos blocos:**

* Conclusão: FCALC (2,94) é < FTAB (3,89) logo não rejeita-se H0 e conclui-se que os blocos não são heterogêneos e que o uso de blocos não foi eficiente. Em próximos experimentos poderia utilizar o DIC.

**Para os tratamentos:**

* Conclusão: FCALC (5,42) é > FTAB (3,00) logo rejeita-se H0 e conclui-se que as médias dos tratamentos diferem entre si, em nível 5% de significância. As diferenças entre as médias não podem ser atribuídas ao acaso.

Como os tratamentos tiveram diferenças pela análise de variância, é necessário fazer um teste de médias para descobrir quais as diferenças entre os tratamentos

*attach(df)*
*HSD.test(anova,as.factor("Tratamento"),console=TRUE)*

Study: anova ~ as.factor("Tratamento")
HSD Test for Raiz 
Mean Square Error:  3.690476 
Tratamento,  means

|  | Raiz|      std| r| Min |Max|
|---|----|---------|---|----|----|
|T1   |10 |2.000000 |3 |  8  |12|
|T2   |11 |2.645751 |3  | 8  |13|
|T3   |10| 2.645751 |3 |  7  |12|
|T4   |14 |1.732051 |3 | 13  |16|
|T5   |15 |2.000000 |3 | 13  |17|
|T6   |15 |2.000000 |3 | 13  |17|
|T7   |16 |2.000000 |3 | 14  |18|

Alpha: 0.05 ; DF Error: 12 
Critical Value of Studentized Range: 4.949594 

Minimun Significant Difference: 5.48972 

Treatments with the same letter are not significantly different.

|  | Raiz| groups|
|----|----|------|
|T7  | 16 |     a|
|T5  | 15 |    ab|
|T6  | 15 |    ab|
|T4  | 14 |    ab|
|T2  | 11 |    ab|
|T1  |  10 |     b|
|T3  | 10 |     b|

### Conclusão:

* Médias dos tratamentos não seguidas por mesma letra diferem pelo teste de Tukey, ao nível de 5% de significância. 
O tratamento 7 apresentou o maior crescimento das raizes em cm, que não diferiu significativamente do 
dos tratamentos 5, 6, 4, 2. O tratamento 1 e o 3 apresentaram os menores crescimentos de raizes.

Vamos agora gerar um gráfico dos nossos dados utilizando a função boxplot para tratamento e bloco

*boxplot(Raiz~Tratamento)*

![image](https://user-images.githubusercontent.com/67385452/119053789-ef8d8c80-b99c-11eb-87c1-026da6eb662d.png)

*boxplot(Raiz~Bloco)*

![image](https://user-images.githubusercontent.com/67385452/119053812-fa482180-b99c-11eb-9fc0-92eb10e9123a.png)

### Pressuposições

**Normalidade dos erros**

* H0: Os erros seguem distribuição normal
* H1: Os erros não seguem distribuição normal

*(norm=shapiro.test(anova$residuals))*

#### Shapiro-Wilk normality test

data:  anova$residuals
W = 0.94449, p-value = 0.2669

Como p-valor calculado (p=0.2669) é maior que o nível de significância adotado (α = 0,05), não rejeita-se HO. Logo, os erros seguem distribuição normal.

Gerando um gráfico de normalidade

*hnp::hnp(anova, las=1, xlab="Quantis teóricos", pch=16)*

![image](https://user-images.githubusercontent.com/67385452/119053890-1a77e080-b99d-11eb-8de1-0b0e82a1d989.png)

### Homogeneidade de Variâncias

* H0 As Variâncias são homogêneas
* H1 As Variâncias não são homogêneas

*(homog=with(df, bartlett.test(anova$residuals ~ Tratamento)))*

#### Bartlett test of homogeneity of variances

data:  anova$residuals by Tratamento
Bartlett's K-squared = 3.2242, df = 6, p-value = 0.7802

Como p-valor calculado (p=0.7802) é maior que o nível de significância adotado (p=0,05), não rejeita H0. Logo, as Variâncias são homogêneas.

### Independência dos erros

* H0 = Os erros são independentes
* H1 = Os erros não são independentes

*lmtest::dwtest(anova)*

#### Durbin-Watson test

data:  anova
DW = 2.729, p-value = 0.683
alternative hypothesis: true autocorrelation is greater than 0

* Como p-valor calculado (p=0.683) é maior que o nível de significância adotado (p=0,05), não rejeita-se H0. Logo, os erros são independentes. 
A Figura apresenta os resíduos brutos. Percebe-se que os resíduos estão distribuídos de forma totalmente aleatória, evidenciando a sua independência.

*plot(anova$residuals, las=1, pch=19, col='red', ylab='Resíduos brutos')
abline(h=0)*

![image](https://user-images.githubusercontent.com/67385452/119054163-8a866680-b99d-11eb-9f08-63869d7bc28a.png)

![image](https://user-images.githubusercontent.com/67385452/119054191-940fce80-b99d-11eb-8d57-42a1b75e32b3.png)

# Chegamos ao fim, mas não tão fim assim. 

* No R, existem várias possibilidades de análises estatísticas, essa apostila é apenas a ponta do Iceberg. 

* Desenvolvam seus scripts, observem os pacotes, pesquisem os conteúdos baseados em R.

* Essa ferramenta pode ser muito útil para o desenvolvimento profissional e acadêmico.



