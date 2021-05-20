# Comandos Básicos

O R considera letras minúsculas e maiúsculas como objetos diferentes, nele podemos digitar expressões ou atribuições, sendo que as expressões quando não recebem uma atribuição são processadas, apresentam os valores e posteriormente são perdidas;

Sempre que pressionarmos a tecla “enter” o comando que está digitado é executado e se não houver comando nada será processado apenas mudamos de linha. 


![image](https://user-images.githubusercontent.com/67385452/119024346-58630d80-b979-11eb-9543-aea84677b754.png)

## INICIANDO O R
 
“>“ este símbolo (prompt do R) significa que o programa está pronto para receber os comandos. 

Sempre que forem inseridos comentários devemos iniciar a frase com o símbolo #, pois essas linhas serão ignoradas pelo R;

Quando se trabalha com conjuntos de dados vindos de outros programas, por exemplo, do Excel, necessita-se utilizar uma função de “read_excel, porém é mais comumente utilizado a extensão “.csv” 

O R necessita da especificação de um diretório, ou seja, uma pasta criada no “C” do computador;

No programa R basta ir em Arquivo/Mudar dir... e definir o diretório em que será salvo o  arquivo, ou simplesmente digitando o caminho no script. 

Quando abrir a página “alteração do diretório”, escolha o diretório (pasta) em que está salvo o arquivo.

### Numéricos

O R possibilita seu uso como calculadora, podendo operar facilmente cálculos e funções, necessitando apenas que o usuário tenha conhecimento dos símbolos usados.


| Símbolo | Significado |
| --------- | ---- |
| ^ ou **| Potenciação |
| * | Multiplicação |
| / | Divisão |
| + | Soma |
| - | Subtração |
| log (x,b) | Logaritmo de x com base b |
| log (x) | Logaritmo natural de x (e)
| log10 (x) | Logaritmo de x com base 10 |
| exp (x) | Exponencial elevado na x (e) |
| sin (x) | Seno de x |
| cos (x) | Cosseno de x |
| tan (x) | Tangente de x |
| sqrt (x) | Raiz quadrada de x |
| asin (x) | Função trigonométrica inversa |
| acos (x) | Função trigonométrica inversa |
| atan (x) | Função trigonométrica inversa | 
| pi | 3,14.. |
| %/% | Divisão inteira |

### Exemplos

a) 5 + 3*10  

 [1] 35                              
 
 b) 20 / 5 ^ 3
 
 [1] 0.16                                  
 
 c) log(5)
 
 [1] 1.609438 
  
 d) log10(100)
 
 [1] 2
  
 e) sqrt(4)
 
 [1] 2
  
 f) sin (90)
 
 [1] 1

## Comandos Incompletos

Sempre que aparecer um sinal de “+” indica ao usuário que falta o restante do código e que o R está esperando para poder interpretar e executar.

10 *
+

E ai você pode digitar o número que faltou e apertar “enter” que o R irá entender que é uma continuação da linha de código.

### Script

No R ao invés de você avançar linha por linha, fica mais interessante criar um script e deixar rodando. Para abrir a janela do script clique em “Arquivo”/“Novo Script”.

![image](https://user-images.githubusercontent.com/67385452/119027420-ad545300-b97c-11eb-9a52-8689183ce29e.png)

Nessa nova janela de script, você pode começar a editar os códigos numa sequência de linhas.
Para fazer com que o script rode, basta clicar   em cada linha que o código irá diretamente para o console onde será rodado e interpretado.

![image](https://user-images.githubusercontent.com/67385452/119027593-e68cc300-b97c-11eb-8bb8-ba1721c631e0.png)
![image](https://user-images.githubusercontent.com/67385452/119027602-eab8e080-b97c-11eb-8519-9d2be9d6185c.png)

## Instalando Pacotes

Existem pacotes nos repositórios criados por diversos usuários distribuídos pelo mundo. Esses pacotes podem ser utilizados em várias análises, como por exemplo, na manipulação de imagens, gráficos, análises estatísticas, etc.

Qualquer pessoa pode criar um pacote e disponibilizá-lo para a comunidade científica. 

Tentem criar um quando finalizarem suas pesquisas.

Os pacotes podem ser instalados de duas maneiras por meio de código ou direto no console.

### Pelo Código

Para instalar o pacote por meio de código, você pode utilizar a função “install.packages”, essa função busca o pacote no repositório e instala no seu computador. 

Ex: Para instalar um pacote que utiliza a função de criação de gráficos

Install.packages(“ggplot2”)

Lembrando que, todo nome do pacote deve estar entre aspas.

Nos dois casos, aparecerá uma janela solicitando em qual espelho você deseja instalar. Pode escolher o “Brazil”.

### Pelo Console

Pelo console é bem simples, na aba  “Pacote”/“instalar Pacote” 

# 
Só que diferentemente do uso do código aparecerá uma janela com vários pacotes onde você deve escolher o que quer instalar.

Porém, apesar dos pacotes instalados, ele ainda não está disponível para uso, existem duas maneiras de habilitá-los, utilizando a função “require” ou “library”:

Require(ggplot2)
Library(“ggplot2”)

![image](https://user-images.githubusercontent.com/67385452/119027771-1e940600-b97d-11eb-907a-07e4af77c6db.png)

Toda vez que for abrir o R, o procedimento de chamar o pacote deve ser feito.

# <center> Agora vem a modernidade!!! </center>






