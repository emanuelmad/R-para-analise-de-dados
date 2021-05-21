# A história

* A ciência do Sensoriamento Remoto, tem avançado na busca da compreensão entre a interessão da radiação eletromagnética e os alvos observados;

* Uma das boas relações estudadas e que possibilitam diversos estudos de fenômenos ambientais são os valores de reflectância;

* Esses valores consistem em variáveis físicas, permitindo relacionar as variáveis com situações existentes de campo.

* A espectrorradiometria de reflectância permite mensurar, em diferentes níveis de comprimento de onda, a energia refletida dos objetos e possibilita analisar em forma de gráficos, tabelas e curvas de reflectância

![image](https://user-images.githubusercontent.com/67385452/119065149-5027c400-b9b3-11eb-8dea-a121270cb2b5.png)

### Primeiro Projeto

* Nosso primeiro projeto é baseado em dados de reflectância de folhas de algumas espécies localizadas no Rio Grande do Sul como: Açoita Cavalo, Aroeira Vermelha, Aroeira Brava, Ingá e Pata de Vaca.

* Os dados espectrais foram coletados com a utilização do espectrorradiômetro FieldSpec®3, modelo RST 3ZC (Analytical Spectral Devices, Inc., EUA). A faixa espectral analisada foi entre 350 a 2500 nm. 

* A calibração foi realizada por meio de uma placa de referência padrão antes da mensuração do valor da refletância das diferentes espécies.

Instalação do Pacote “agricolae” para analisar médias com o teste de Tukey e plotar as letrinhas das diferenças das médias.

*install.packages("agricolae")*

*require(agricolae)*

Caso queiram saber mais sobre esse pacote acessem pelo link:

https://cran.r-project.org/web/packages/agricolae/agricolae.pdf

Para darmos início ao nosso projeto, vocês podem baixar o arquivo no seguinte endereço:

https://raw.githubusercontent.com/emanuelmad/R-para-analise-de-dados/main/Alvos.csv

Este comando faz com que você importe o arquivo para a estrutura do R

*Alvos <- read.csv ("Alvos.csv",header=TRUE,sep=",",dec=".")*

Também pode ser importado pelo código:

*Alvos <- read.csv ("Alvos.csv")*

Nesse caso, os parâmetros definidos estão em default, e o R entende que você está utiizando dados nos padrões de unidades inglesas;

Apresenta os dados

*Alvos*

Aqui no caso utilizei o comando head(Alvos) para aparecer apenas as primeiras linha, pois nosso conjunto de dados possui mais de duas mil linhas

|Wavelength|     Acoita| Aroeira_vermelha| Aroeira_braba|       Inga Pata_de_vaca|
|----------|----------|-----------------|---------------|------------------------|
|350 |1.66878917|      0.095508732|   6.014867620| 0.36832961|  0.570653290|
|351 |0.72942547|      0.100001200|  0.404067618| 0.09326813|  0.323317413|
|352 |0.47846506|      0.066667869|   0.161507531| 0.08338450|  0.165272754|
|353 |0.65603818|      0.278697619|   0.195255603| 0.41285667|  0.009490587|
|354 |0.24209775|      0.564954984|   0.289825147| 1.14750975|  0.289824847|
|355 |0.27625701|      0.441769224|   2.109235362| 1.11944907|  0.548035328|
|356 |0.90523061|      0.241451526|   0.400000900| 0.17760814|  0.993146400|


Habilita o acesso aos valores dos dados e nomes dos vetores

*attach(Alvos)*

The following objects are masked from Alvos (pos = 9):

    Acoita, Aroeira_braba, Aroeira_vermelha, Inga, Pata_de_vaca, Wavelength

Apresentar Síntese da Estatística do conjunto de dados. 

Nesse caso podemos utilizar os intervalos dos comprimentos de onda do Azul, Verde, Vermelho, Infravermelho. Lembrando que as informações das bandas são provenientes do satélite LANDSAT5 sensor TM.

- [x] B1 – como comprimento do Azul
- [x] B2 - como comprimento do Verde
- [x] B3 – Como comprimento do Vermelho
- [x] B4 - como comprimento do infravermelho Próximo
- [x] B5 – Como comprimento do infravermelho Médio
- [x] B7 - como comprimento do infravermelho Médio/distante

B1 <- subset(Alvos,(Wavelength >= 450 & Wavelength <= 520),select = c(names(Alvos)))
sinteste_estatisca_B1 <- summary(B1)
sinteste_estatisca_B1

|Wavelength|        Acoita   |     Aroeira_vermelha | Aroeira_braba      |    Inga           | Pata_de_vaca  | 
|----------|-----------------|-----------------------|-------------------|-------------------|--------------|
 |Min.   :450.0|   Min.   :0.06060|   Min.   :0.07123|   Min.   :0.06003  | Min.   :0.04775  |Min.   :0.08448 | 
 |1st Qu.:467.5 |  1st Qu.:0.06662 |  1st Qu.:0.07970 |  1st Qu.:0.06945  | 1st Qu.:0.05924  |1st Qu.:0.09507  |
 |Median :485.0 |  Median :0.06900  | Median :0.08474  | Median :0.07637  | Median :0.06211  |Median :0.10203  |
 |Mean   :485.0 |  Mean   :0.07105  | Mean   :0.08921  | Mean   :0.08463  | Mean   :0.06337  |Mean   :0.11009  |
 |3rd Qu.:502.5 |  3rd Qu.:0.07395  | 3rd Qu.:0.09807  | 3rd Qu.:0.08760  | 3rd Qu.:0.06712  |3rd Qu.:0.11310  |
 |Max.   :520.0 |  Max.   :0.09656  | Max.   :0.13090  | Max.   :0.15652  | Max.   :0.08221  |Max.   :0.17893|

Fazer agora para as outras bandas do nosso estudo

*B2 <- subset(Alvos,(Wavelength >= 530 & Wavelength <= 610),select = c(names(Alvos)))*

*sinteste_estatisca_B2 <- summary(B2)*

*sinteste_estatisca_B2*

*B3 <- subset(Alvos,(Wavelength >= 630 & Wavelength <= 690),select = c(names(Alvos)))*

*sinteste_estatisca_B3 <- summary(B3)*

*sinteste_estatisca_B3*

*B4 <- subset(Alvos,(Wavelength >= 780 & Wavelength <= 900),select = c(names(Alvos)))*

*sinteste_estatisca_B4 <- summary(B4)*

*sinteste_estatisca_B4*

*B5 <- subset(Alvos,(Wavelength >= 1550 & Wavelength <= 1750),select = c(names(Alvos)))*

*sinteste_estatisca_B5 <- summary(B5)*

*sinteste_estatisca_B5*

*B7 <- subset(Alvos,(Wavelength >= 2090 & Wavelength <= 2350),select = c(names(Alvos)))*

*sinteste_estatisca_B7 <- summary(B7)*

*sinteste_estatisca_B7*

O comando "ls()" lista os objetos criados

*ls()*

O comando "length(B1)" apresenta o tamanho do objeto B1

*length(B1)*

*[1] 6*

Habilita acesso direto aos valores e as variáveis

*attach(B1)*
*[1] 71*

*length(Wavelength)*

*detach(B1)*

Estas operações devem ser repetidas para todos os objetos de maneira a se obter o comprimento das bandas espectrais (número de observações).

*attach(B2)*

*length(Wavelength)*

*detach(B2)*

*attach(B3)*

*length(Wavelength)*

*detach(B3)*

*attach(B4)*

*length(Wavelength)*

*detach(B4)*

*attach(B5)*

*length(Wavelength)*

*detach(B5)*

*attach(B7)*

*length(Wavelength)*

*detach(B7)*

Criação dos "data.frames" para cada um dos objetos (bandas espectrais) gl = graus de liberdade (número de variáveis, número de observações) 

Aqui abaixo, deve-se atentar também, os nomes das variáveis utilizadas no arquivo de vocês. O símbolo “<-“ funciona como o “=”

* B1.Alvos<- data.frame(Alvos_B1=gl(5,71),Reflectancias_B1=c(B1$Acoita,B1$Aroeira_vermelha,B1$Aroeira_braba,B1$Inga,B1$Pata_de_vaca))

* B2.Alvos<- data.frame(Alvos_B2=gl(5,81),Reflectancias_B2=c(B2$Acoita,B2$Aroeira_vermelha,B2$Aroeira_braba,B2$Inga,B2$Pata_de_vaca))

* B3.Alvos<- data.frame(Alvos_B3=gl(5,61),Reflectancias_B3=c(B3$Acoita,B3$Aroeira_vermelha,B3$Aroeira_braba,B3$Inga,B3$Pata_de_vaca))

* B4.Alvos<-data.frame(Alvos_B4=gl(5,121),Reflectancias_B4=c(B4$Acoita,B4$Aroeira_vermelha,B4$Aroeira_braba,B4$Inga,B4$Pata_de_vaca))
* B5.Alvos<-data.frame(Alvos_B5=gl(5,201),Reflectancias_B5=c(B5$Acoita,B5$Aroeira_vermelha,B5$Aroeira_braba,B5$Inga,B5$Pata_de_vaca))
* B7.Alvos<-data.frame(Alvos_B7=gl(5,261),Reflectancias_B7=c(B7$Acoita,B7$Aroeira_vermelha,B7$Aroeira_braba,B7$Inga,B7$Pata_de_vaca))

lista os objetos criados (data.frames)

*ls()*

*attach(B1.Alvos)*

*B1.Alvos*

Obtém os nomes das colunas do dataframe

*names(B1.Alvos)*

Verifica se "Alvos_B1" é um fator

*is.factor(Alvos_B1)*

A sequência abaixo de comandos, realiza a ANOVA para o conjunto de dados segmentado por Banda Espectral, no caso abaixo: Banda 1 

Em síntese, deve-se repetir a sequência abaixo para as demais bandas, cuidando-se para alterar os nomes de variáveis e parâmetros nas sentenças. 

O comando "aov" faz a análise de variância para o conjunto de dados objeto B1 

Os comandos abaixo, devem ser repetidos para cada uma das Bandas Espectrais  respeitando-se as nomenclaturas anteriormente utilizadas.

*B1.aov <- aov(Reflectancias_B1 ~ Alvos_B1)*

*Tabela_ANOVA_B1 <- summary(B1.aov)*

*Tabela_ANOVA_B1*

*summary(B1.aov)*


|FV	|GL (df)|	SQ (Sum Sq)|	QM (Mean Sq)|	F	|Pr(>F)|
|----|-----|------------|---------------|------------|
|Alvos_B1|	4|	0.09235	|0.023087|	81.88|< 2e-16 *** |
|Resíduo|	350|	0.09869|	0.000282|---	|-----|	
|Total|	20|	186|	----	| -------|------|
  
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Esse comando é levado em consideração o pacote Agricolae

*tukey_especies_B1 <- HSD.test(B1.aov, c("Alvos_B1"), main="Comprimento de Onda B1", console=TRUE)*

Study: Comprimento de Onda B1

HSD Test for Reflectancias_B1 

Mean Square Error:  0.0002819724 

Alvos_B1,  means

|--|  Reflectancias_B1|         std|  r|        Min|        Max|
|---|-----------------|------------|---|-----------|-----------|
|1|       0.07104950| 0.007563580| 71| 0.06060115| 0.09655893|
|2       |0.08920504| 0.014941701 |71| 0.07122968 |0.13089848|
|3       |0.08462920| 0.023532225| 71 |0.06002787 |0.15652471|
|4       |0.06337418| 0.007364709 |71 |0.04775059 |0.08221133|
|5       |0.11008844| 0.022834081| 71 |0.08448404| 0.17893401|

Alpha: 0.05 ; DF Error: 350 
Critical Value of Studentized Range: 3.877847 

Minimun Significant Difference: 0.00772796 

Treatments with the same letter are not significantly different.

|-- | Reflectancias_B1| groups|
|-- |-----------------|-------|
|5    |   0.11008844 |     a|
|2   |    0.08920504  |    b|
|3  |     0.08462920   |   b|
|1 |      0.07104950    |  c|
|4|       0.06337418     | c|

plot(tukey_especies_B1)
![image](https://user-images.githubusercontent.com/67385452/119066402-13a99780-b9b6-11eb-98f5-144d8b9eaacb.png)

Esse comando é uma função Raiz do R e não precisa de pacote

*pares_especies_B1 <- TukeyHSD(B1.aov,ordered=TRUE)*

*pares_especies_B1*

*plot(TukeyHSD(B1.aov,ordered=TRUE))*

Comando para salvar a imagem criada

*png("TukeyB1_Landsat.png")*

*plot(TukeyHSD(B1.aov,ordered=TRUE))*

*dev.off()*

* Aproveito e deixo aqui o código para criar o gráfico de linha de todas as espécies com todos os comprimentos de onda. Notem a estrutura do gráfico se não é idêntica a uma vegetação sadia que eu venho mostrando, vocês também podem colocar os intervalos para o gráfico ficar mais claro.

*plot(Alvos$Wavelength, Alvos$Acoita, type="l", main="Curvas espectrais das Espécies analisadas",xlab="Comprimento de Onda",ylab="Reflectância %",col="blue",ylim=c(0,0.65))

*lines(Alvos$Wavelength, Alvos$Aroeira_vermelha, type='l', col = "green")*

*lines(Alvos$Wavelength, Alvos$Aroeira_braba, type='l', col = "red")*

*lines(Alvos$Wavelength, Alvos$Inga, type='l', col = "cyan")*

*lines(Alvos$Wavelength, Alvos$Pata_de_vaca, type='l', col = "orange")*

![image](https://user-images.githubusercontent.com/67385452/119066620-8c105880-b9b6-11eb-94b4-a8acb2ec3e7d.png)











