![image](https://user-images.githubusercontent.com/67385452/119029197-b80fe780-b97e-11eb-8093-40156a90d035.png)

**RStudio** é um software livre de ambiente de desenvolvimento integrado para R, uma linguagem de programação para gráficos e cálculos estatísticos.

# Sobre o RStudio

O RStudio está disponível em duas edições: RStudio Desktop, que roda localmente como um aplicativo desktop padrão; e RStudio Server, que permite acessar o RStudio usando um navegador web enquanto ele roda em um servidor GNU/Linux remoto.

Pacotes de instalação do RStudio Desktop estão disponíveis para Microsoft Windows, Mac OS X, e GNU/Linux.

O RStudio é escrito na linguagem de programação C++ e usa o framework Qt para sua interface gráfica de usuário.

## INSTALAÇÃO
 
Para instalar o RStudio é necessário já possuir o R, ele funciona como uma IDE do R.

Vocês podem baixar o RStudio no endereço:

https://www.rstudio.com/products/rstudio/download/#download


## INICIANDO O RStudio
 
No R Studio temos quatro janelas: editor, o console, o environment e o output.

As principais janelas são o Editor/Scripts, onde será bastante utilizado para gerar os dados e o console onde é rodado o script e as saídas dos resultados. 

![image](https://user-images.githubusercontent.com/67385452/119029495-13da7080-b97f-11eb-9c3c-fa63c136dab4.png)

Além dessas principais janelas, existem também outras abas como:
 
**History**: painel com um histórico dos comandos rodados.

**Files**: mostra os arquivos no diretório de trabalho. É possível navegar entre diretórios.

**Packages**: apresenta todos os pacotes instalados e carregados.

**Help**: janela onde a documentação das funções serão apresentadas.

**Viewer**: painel onde relatórios e dashboards serão apresentados.

Para iniciar um projeto no RStudio, é necessário criar uma pasta no “C:” e direcionar o caminho para ela, na própria IDE você pode ir na aba “Sessão” > “Setar diretório de trabalho” > “Escolher diretório”. 

Nesse caminho, você vai direcionar a pasta onde estão seus arquivos de dados.

A partir dai, você pode iniciar todas as análises de dados e se divertir com o RStudio. 

![image](https://user-images.githubusercontent.com/67385452/119029659-4c7a4a00-b97f-11eb-8325-6912a5fe7b8d.png)

## Vetores

O R possibilita criação de vetores, que nada mais é um conjunto de valores, podendo ser numéricos ou texto. 
Para criar um vetor basta colocar os valores separados por vírgula dentro de um “c()”

### Exemplo:

*DAP = c( 10.5, 11.2, 10.2, 15.7)*

*H = c(20.2, 22.4, 20.0, 29.4)*

*Especie =c(“Eucalipto”, “Pinus”, “Acácia”, “Araucária”)*

Lembrando que, por se tratar de uma string (texto) os nomes devem vir entre “ ”.

Cada valor dentro de um vetor tem uma posição, ou seja, a ordem é dada pela posição de inserção dos valores.

### Exemplo:

*DAP[3]*

*[1] 10.2*

Além disso, um vetor só pode ser a mesma classe dos seus objetos, um comando utilizado para saber a classe do vetor é:

*class(Especie)*

*[1] "character"*

Pode ser realizado alguns cálculos entre vetores:

Um exemplo é a soma de vetores, nesse exemplo estamos apenas utilizando o código para somar dois vetores. Porém, na prática não é recomendável somar DAP e H, pois são dados com características diferentes.  

*DAP + H* 

*[1] 30.7 33.6 30.2 45.1*

## Data Frame

O dataframe é um conjunto de vetores combinados em um único dado. Pode ser utilizado tanto valores numéricos como texto.

É de extrema relevância, pois aqui iremos partir para o início dos nossos estudos de diversas fontes de dados. 

Utilizando os dados anteriores, podemos criar um data frame com DAP, H e Especie utilizando o comando data.frame

*df = data.frame(DAP, H, Especie)*

*df*

Resultado

  |DAP    |H|   Especie|
  --------|--|---------|
|10.5 |20.2 |Eucalipto|
|11.2 |22.4 |Pinus|
|10.2 |20.0 |Acácia|
|15.7 |29.4 |Araucária|

Essa apostila é de carater para iniciar os primeiros passos no R, logicamente deve-se pesquisar e procurar mais detalhes em outras fontes, além disso, a comunidade científica do R é bastante robusta e possui diversos tipos de materiais para auxiliá-los na pesquisa.

Comecem a observar o uso dos pacotes disponíveis para análise de dados, com certeza algum servirá para as pesquisas de vocês.

# <center> Agora vamos praticar um pouco e nos desafiar!!! </center> 







 


