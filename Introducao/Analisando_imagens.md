# Analisando Imagens de Satélite

## A história

* Imagens de satélite sempre despertam interesse, pois tudo é visto de cima. Nas áreas ambientais tem um valor importante, pois pode auxiliar o entendimento de manifestações dinâmicas da natureza, humana, econômica, etc.

* Um dos sistemas mais utilizados para monitoramento é a série LANDSAT que desde 1972 vem produzindo imagens em todo o globo.

* Além disso, com as imagens podem ser calibradas para gerar vários índices que podem auxiliar os pesquisadores em seus trabalhos de pesquisas.

* Até o presente momento, temos o LANDSAT 8 com seu sensor acoplado OLI, possuindo as seguintes características:

|Sensor|	Bandas Espectrais|	Resolução Espectral|	Resolução Espacial|	Resolução Temporal|	Área Imageada|	Res.Radiométrica|
|------|-------------------|---------------------|--------------------|-------------------|--------------|-------------------|
|OLI (Operational Land Imager)|	(B1) COSTAL|	0.433 - 0.453 µm|	30 m|	16 dias|	185 km|	12 bits|
|	                             | (B2) AZUL|	0.450 - 0.515 µm|				|        |         |        |
|	                              |(B3) VERDE|	0.525 - 0.600 µm|				|        |         |        |
|	                              |(B4) VERMELHO|	0.630 - 0.680 µm|			|	      |        |        |   
|	                              |(B5) INFRAVERMELHO PRÓXIMO|	0.845 - 0.885 µm|				|       |     |       |
|	                              |(B6) INFRAVERMELHO MÉDIO|	1.560 - 1.660 µm|				|         |      |        |
|	                              |(B7) INFRAVERMELHO MÉDIO|	2.100 - 2.300 µm|				|          |      |        |
|	                              |(B8) PANCROMÁTICO|	0.500 - 0.680 µm|	15 m|			|            |       |        |
|	                              |(B9) Cirrus|	1.360 - 1.390 µm|	30 m|			|          |         |         |
|TIRS (Thermal Infrared Sensor)	|(B10) LWIR - 1|	10.30 - 11.30 µm|	100 m|	16 dias|	185 km | 12 bits|
|	                              |(B11) LWIR - 2|	11.50 - 12.50 µm|				|          |         |          |

A imagem baixada é oriunda do Serviço Geológico Americano por meio do endereço: 

https://earthexplorer.usgs.gov/

São da cena órbita 217 ponto 066 datada em 25 de março de 2019.

Ao fazer o download, é necessário dizipar o arquivo ficando da seguinte forma:

-[x] LC08_L1TP_217066_20190312_20190325_01_T1_B1.TIF       
-[x] LC08_L1TP_217066_20190312_20190325_01_T1_B2.TIF       
-[x] LC08_L1TP_217066_20190312_20190325_01_T1_B3.TIF       
-[x] LC08_L1TP_217066_20190312_20190325_01_T1_B4.TIF       
-[x] LC08_L1TP_217066_20190312_20190325_01_T1_B5.TIF       
-[x] LC08_L1TP_217066_20190312_20190325_01_T1_B6.TIF       
-[x] LC08_L1TP_217066_20190312_20190325_01_T1_B7.TIF       
-[x] LC08_L1TP_217066_20190312_20190325_01_T1_B9.TIF       
-[x] LC08_L1TP_217066_20190312_20190325_01_T1_B10.TIF       
-[x] LC08_L1TP_217066_20190312_20190325_01_T1_B11.TIF       
-[x] LC08_L1TP_217066_20190312_20190325_01_T1_B8.TIF       
-[x] LC08_L1TP_217066_20190312_20190325_01_T1_BQA.TIF   

*https://drive.google.com/file/d/1B8ESowfTrVsSTaxcSbfLrxNCd8Jy7HYD/view?usp=sharing*    

Agora podemos iniciar nosso Script de forma a gerar vários produtos de sensoriamento remoto, como índices e uma classificação não supervisionado utilizando o k-means.

Essa cena passa em cima da cidade de Petrolina-PE.

### VAMOS LÁ!!!

O primeiro passo é justamente instalar os pacotes necessários referente as funções que iremos utilizar

Instalando RStoolbox

RStoolbox está agora disponível no CRAN e pode ser instalado normalmente com

*install.packages("Rstoolbox")*

*library(RStoolbox)*

*install.packages("raster")*

*library(raster)*

*intall.packages("devtools")*

*library(devtools)*

*install_github("bleutner/RStoolbox")*


Em seguida podemos fazer a leitura do metadados das imagens e iniciar os trabalhos:

*mtlFile= readMeta("LC08_L1TP_217066_20190312_20190325_01_T1_MTL.txt")*

Quando utilizamos a função summary observaremos as informações contidas no metadados

*summary(mtlFile)*

* Resultado

*Scene:      LC82170662019071LGN00* 

*Satellite:  LANDSAT8*

*Sensor:     OLI_TIRS* 

*Date:       2019-03-12*

*Path/Row:   217/66* 

*Projection: +proj=utm +zone=24 +datum=WGS84 +units=m +no_defs*

*Data:*
                                                  *FILES QUANTITY CATEGORY*
*B1_dn   LC08_L1TP_217066_20190312_20190325_01_T1_B1.TIF       dn    image*

*B2_dn   LC08_L1TP_217066_20190312_20190325_01_T1_B2.TIF       dn    image*

*B3_dn   LC08_L1TP_217066_20190312_20190325_01_T1_B3.TIF       dn    image*

*B4_dn   LC08_L1TP_217066_20190312_20190325_01_T1_B4.TIF       dn    image*

*B5_dn   LC08_L1TP_217066_20190312_20190325_01_T1_B5.TIF       dn    image*

*B6_dn   LC08_L1TP_217066_20190312_20190325_01_T1_B6.TIF       dn    image*

*B7_dn   LC08_L1TP_217066_20190312_20190325_01_T1_B7.TIF       dn    image*

*B9_dn   LC08_L1TP_217066_20190312_20190325_01_T1_B9.TIF       dn    image*

*B10_dn LC08_L1TP_217066_20190312_20190325_01_T1_B10.TIF       dn    image*

*B11_dn LC08_L1TP_217066_20190312_20190325_01_T1_B11.TIF       dn    image*

*B8_dn   LC08_L1TP_217066_20190312_20190325_01_T1_B8.TIF       dn      pan*

*QA_dn  LC08_L1TP_217066_20190312_20190325_01_T1_BQA.TIF       dn       qa*

*Available calibration parameters (gain and offset):*

	*dn -> radiance (toa)*
  
	*dn -> reflectance (toa)*
  
	*dn -> brightness temperature (toa)*

Vamos chamar nosso mtlFile  de metaData para padronizar nossos trabalhos

*metaData = (mtlFile)*

*summary(metaData)*

Como a cena é muito grande 185 x 185km é interessante diminuir para que o processamento seja mais rápido, por isso agora vamos importar nosso vetor do Município de Petrolina-PE e fazer o recorte da cena

*limite = shapefile("petrolina.shp")*

*limite*

* Resultado

*class       : SpatialPolygonsDataFrame* 

*features    : 1* 

*extent      : -40.95732, -40.20901, -9.474836, -8.623511  (xmin, xmax, ymin, ymax)*

*crs         : +proj=longlat +ellps=GRS80 +towgs84=0,0,0,0,0,0,0 +no_defs* 

*variables   : 13*

*names       : OBJECTID, GEOCODIGO,      NOME, UF, ID_UF, REGIAO, MESOREGIAO, MICROREGIA, LATITUDE, LONGITUDE, SEDE,    Shape_Leng,   Shape_Area* 

*value       :        2,   2611101, Petrolina, PE,    26, Nordeste, SAO FRANCISCO PERNAMBUCANO,  PETROLINA,   -9.393,   -40.508, True, 2.97917219924, 0.3671855305*

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

*plot(limite, main = "Petrolina-PE")*

![image](https://user-images.githubusercontent.com/67385452/119181611-371d2280-ba48-11eb-8e08-8fac4e918e4a.png)

#### Agora vamos carregar a base raster do nosso metadados 

*lsat = stackMeta(mtlFile)*

*lsat*

* Resultado

*class      : RasterStack*

*dimensions : 7721, 7591, 58610111, 10  (nrow, ncol, ncell, nlayers)*

*resolution : 30, 30  (x, y)*

*extent     : 260985, 488715, -1075515, -843885  (xmin, xmax, ymin, ymax)*

*crs        : +proj=utm +zone=24 +datum=WGS84 +units=m +no_defs*

*names      : B1_dn, B2_dn, B3_dn, B4_dn, B5_dn, B6_dn, B7_dn, B9_dn, B10_dn, B11_dn*

*min values :     0,     0,     0,     0,     0,     0,     0,     0,      0,      0*

*max values : 65535, 65535, 65535, 65535, 65535, 65535, 65535, 65535,  65535,  65535*

-----------------------------------------------------------------------------------------------------------------------------------------

*plot(lsat)*

![image](https://user-images.githubusercontent.com/67385452/119181741-66cc2a80-ba48-11eb-82ca-a22a804a0b7e.png)

Agora vamos utilizar o recorte da cena com nosso vetor do Município de Petrolina-PE, que nesse caso, é nosso objeto de estudo. O primeiro passo é colocar o vetor na mesma projeção dos arquivos raster.

Coloca na mesma coordenada dos dados raster e que estou apenas atualizando meu vetor chamado limite com o corte do mesmo.

*limite <- spTransform(limite,crs(lsat))*

*limite*

Corta as imagens apenas no limite do Município de Petrolina-PE

*lsat_crop = crop(lsat, limite)*

*lsat_crop*

*plot(lsat_crop)*

![image](https://user-images.githubusercontent.com/67385452/119181816-81060880-ba48-11eb-9feb-4c26bcab68d4.png)

As imagens de satélite possuem em seu formato o DN, mais conhecido como Digital Number, ou simplesmente numeros digitais e para quem quer trabalhar com índices de vegetação é importante fazer a transformação para reflectância e ter em mãos parâmetros físicos da imagem.

Os métodos de correção atmosférica (sdos, dos e costz) aplicam-se à região óptica (solar) do espectro e não afetam a banda térmica.

Vamos iniciar convertendo os DN para a reflectância no topo da atmosfera e temperatura de brilho das bandas termais utilizando a função radcor

*lsat_ref = radCor(lsat, mtlFile, method = "apref")*

*lsat_ref*

* Resultado

*class      : RasterStack*

*dimensions : 7721, 7591, 58610111, 10  (nrow, ncol, ncell, nlayers)*

*resolution : 30, 30  (x, y)*

*extent     : 260985, 488715, -1075515, -843885  (xmin, xmax, ymin, ymax)*

*crs        : +proj=utm +zone=24 +datum=WGS84 +units=m +no_defs* 

*names      :      B1_tre,      B2_tre,      B3_tre,      B4_tre,      B5_tre,      B6_tre,      B7_tre,      B9_tre,      B10_bt,      B11_bt*

*min values :      0.0000,      0.0000,      0.0000,      0.0000,      0.0000,      0.0000,      0.0000,      0.0000,    147.5171,    141.6706*

*max values :   1.0000000,   1.0000000,   1.0000000,   1.0000000,   1.0000000,   1.0000000,   1.0000000,   0.1283646, 309.3165607, 302.9231399*

----------------------------------------------------------------------------------------------------------------------------------------------------------

*lsat_ref_crop = crop(lsat_ref,limite)*

*plot(lsat_ref_crop)*

![image](https://user-images.githubusercontent.com/67385452/119182001-c296b380-ba48-11eb-9742-c18b88babef4.png)

##### Podemos também utilizar o método do DOS

*lsat_sref = radCor(lsat, mtlFile, method = "dos")*

*lsat_sref*

* Resultado

*class      : RasterStack*

*dimensions : 7721, 7591, 58610111, 10  (nrow, ncol, ncell, nlayers)*

*resolution : 30, 30  (x, y)*

*extent     : 260985, 488715, -1075515, -843885  (xmin, xmax, ymin, ymax)*

*crs        : +proj=utm +zone=24 +datum=WGS84 +units=m +no_defs*

*names      :      B1_sre,      B2_sre,      B3_sre,      B4_sre,      B5_sre,      B6_sre,      B7_sre,      B9_sre,      B10_bt,      B11_bt*

*min values :      0.0000,      0.0000,      0.0000,      0.0000,      0.0000,      0.0000,      0.0000,      0.0000,    147.5171,    141.6706*

*max values :   1.0000000,   1.0000000,   1.0000000,   1.0000000,   1.0000000,   1.0000000,   1.0000000,   0.1312845, 309.3165607, 302.9231399*

------------------------------------------------------------------------------------------------------------------------------------------------------

*lsat_sref_crop = crop(lsat_sref, limite)*

*plot(lsat_sref_crop)*

![image](https://user-images.githubusercontent.com/67385452/119182217-038ec800-ba49-11eb-8b49-9f1332e47724.png)

Correção dos valores dos níveis digitais para reflectância de superfície utilizando o método do DOS.

Nesse caso utilizaremos apenas as bandas do visível e do infravermelho (1 a 7), fazendo um filtro no nosso conjunto de dados.

*hazeDN = estimateHaze(lsat_crop, hazeBands = 1:7, darkProp = 0.01, plot = TRUE)*

*lsat_sref <- radCor(lsat_crop, mtlFile, method = "sdos",* 
                    *hazeValues = hazeDN, hazeBands = 1:7)*
		    
![image](https://user-images.githubusercontent.com/67385452/119182286-186b5b80-ba49-11eb-9a1b-b6c2c12e47b2.png)
		    
* Caso queiram analisar estatisticamente as imagens geradas vocês podem baixar o pacote do ggplot2, o mesmo possui diversas funções e gráficos bastante robustos para construção.

*library(ggplot2)*

Pode ser calculado um índice bastante conhecido na literatura como o NDVI. 

#### Vamos ao script!!

*ndvi <- spectralIndices(lsat_crop, red = "B4_dn", nir = "B5_dn", indices = "NDVI")*

*ndvi*

* Resultado

*class      : RasterLayer*

*dimensions : 3136, 2747, 8614592  (nrow, ncol, ncell)*

*resolution : 30, 30  (x, y)*

*extent     : 284715, 367125, -1047765, -953685  (xmin, xmax, ymin, ymax)*

*crs        : +proj=utm +zone=24 +datum=WGS84 +units=m +no_defs*

*source     : memory*

*names      : NDVI*

*values     : -0.9998091, 0.6511334  (min, max)*

-----------------------------------------------------------------------------------------------------------------------------------------------------------

*plot(ndvi)*

![image](https://user-images.githubusercontent.com/67385452/119182508-5ff1e780-ba49-11eb-9247-ccb6df17b04f.png)boxplot(ndvi)

*boxplot(ndvi)*

![image](https://user-images.githubusercontent.com/67385452/119182544-6d0ed680-ba49-11eb-8c93-4f3ba496eb1c.png)

Podemos também analisar um histograma do NDVI

*hist(ndvi,
     main = "Distribution of NDVI values",
     xlab = "NDVI",
     ylab= "Frequency",
     col = "wheat",
     xlim = c(-0.5, 1),
     breaks = 30,
     xaxt = 'n')
axis(side=1, at = seq(-0.5,1, 0.05), labels = seq(-0.5,1, 0.05))*

![image](https://user-images.githubusercontent.com/67385452/119182604-80ba3d00-ba49-11eb-9544-d1fb3d06b7c8.png)

Notem que a maioria dos valores estão na frequência entre 0,2 a 0,4. 

Esse comando utilizando a função do *ggplot2* gera uma imagem em níveis de cinza do nosso NDVI criado. 

*ggR(ndvi, geom_raster = TRUE) +
  scale_fill_gradientn(colours = c("black", "white"))*
  
  ![image](https://user-images.githubusercontent.com/67385452/119182714-ab0bfa80-ba49-11eb-9ef0-2931f4a06763.png)

**Com apenas um único comando podemos calcular diversos índices de vegetação de uma só vez. A função spectralIndices tem em seu escopo fórmulas de vários índices utilizados em pesquisas**

*plot(SI)*

![image](https://user-images.githubusercontent.com/67385452/119182906-bfe88e00-ba49-11eb-8c5d-05a72f2f52d1.png)

![image](https://user-images.githubusercontent.com/67385452/119182918-c4ad4200-ba49-11eb-81dc-cf3f37372bd4.png)

*boxplot(SI)*

![image](https://user-images.githubusercontent.com/67385452/119182988-d858a880-ba49-11eb-8b7b-dbec2229555b.png)

Para uma melhor visualização dos boxplots é necessário avaliar cada índice, pois cada um tem uma escala diferente

*hist(SI)*

![image](https://user-images.githubusercontent.com/67385452/119183027-e7d7f180-ba49-11eb-9807-062e83018b4a.png)

Podemos salvar todas nossas imagens e trabalhar num outro software de GIS, como por exemplo Qgis e Arcgis.

*writeRaster(SI$CTVI, filename = "CTVI.tif")*

*writeRaster(SI$DVI , filename = "DVI.tif")*

*writeRaster(SI$EVI2, filename = "EVI2.tif")*

*writeRaster(SI$GEMI, filename = "GEMI.tif")*

*writeRaster(SI$MSAVI, filename = "MSAVI.tif")*

*writeRaster(SI$MSAVI2, filename = "MSAVI2.tif")*

*writeRaster(SI$NDVI, filename = "NDVI.tif")*

*writeRaster(SI$NRVI, filename = "NRVI.tif")*

*writeRaster(SI$RVI, filename = "RVI.tif")*

*writeRaster(SI$SAVI, filename = "SAVI.tif")*

## Classificação não-supervisionada de imagens

* Iremos dar mais um passo na utilização do R em análise de dados geoespaciais.

* Dessa vez, vamos classificar de forma automatizada (não-supervisionada) nossa imagem e para isso iremos utilizar a função do K-means.

* Primeiro iremos fazer um filtro de nossas imagens salvando apenas as imagens do visível e infravermelho, lembrando que, estou utilizando as imagens transformadas para reflectância.

*B1_tre = (lsat_ref_crop$B1_tre)*

*B2_tre = (lsat_ref_crop$B2_tre)*

*B3_tre = (lsat_ref_crop$B3_tre)*

*B4_tre = (lsat_ref_crop$B4_tre)*

*B5_tre = (lsat_ref_crop$B5_tre)*

*B6_tre = (lsat_ref_crop$B6_tre)*

*B7_tre = (lsat_ref_crop$B7_tre)

Como temos 7 bandas, precisamos juntá-las para um único data frame

*image = brick(B1_tre,B2_tre,B3_tre,B4_tre,B5_tre,B6_tre,B7_tre)*

* Resultado

*class      : RasterBrick* 

*dimensions : 3136, 2747, 8614592, 7  (nrow, ncol, ncell, nlayers)*

*resolution : 30, 30  (x, y)*

*extent     : 284715, 367125, -1047765, -953685  (xmin, xmax, ymin, ymax)*

*crs        : +proj=utm +zone=24 +datum=WGS84 +units=m +no_defs*

*source     : C:/Users/emanu/AppData/Local/Temp/Rtmpae7F9y/raster/r_tmp_2021-05-17_203930_22140_98977.grd* 

*names      :    B1_tre,    B2_tre,    B3_tre,    B4_tre,    B5_tre,    B6_tre,    B7_tre* 

*min values :         0,         0,         0,         0,         0,         0,         0*

*max values : 0.6148112, 0.7013985, 0.9265673, 1.0000000, 1.0000000, 1.0000000, 1.0000000*

-----------------------------------------------------------------------------------------------------------------------------------

*plot(image)

![image](https://user-images.githubusercontent.com/67385452/119183436-79476380-ba4a-11eb-90d5-59cb45ed86a3.png)

Executa a função kMeans com 25 sementes e 5 classes.

*set.seed(25)*

*unC = unsuperClass(image, nSamples = 100, nClasses = 5, nStarts = 5)*

*unC*

* Resultado

*unsuperClass results*

*************** Map ******************

*$map*

*class      : RasterLayer* 

*dimensions : 3136, 2747, 8614592  (nrow, ncol, ncell)*

*resolution : 30, 30  (x, y)*

*extent     : 284715, 367125, -1047765, -953685  (xmin, xmax, ymin, ymax)*

*crs        : +proj=utm +zone=24 +datum=WGS84 +units=m +no_defs* 

*source     : C:/Users/emanu/AppData/Local/Temp/Rtmpae7F9y/raster/r_tmp_2021-05-17_204542_22140_13233.grd* 

*names      : layer* 

*values     : 1, 5  (min, max)*

---------------------------------------------------------------------------------------------------------------------

*writeRaster(unC$map, filename = "unC.tif")*

*plot(unC$map)*

![image](https://user-images.githubusercontent.com/67385452/119183661-c9bec100-ba4a-11eb-8189-ba6d959ba343.png)

Podemos também fazer de outra forma como essa a seguir:

Execute a função kMeans no valor das imagens  (indicados pelo colchete e criando uma imagem com 5 classes) 

*kMeansResult <- kmeans(image[], centers=5)*

* Resultado

*class      : RasterLayer* 

*dimensions : 3136, 2747, 8614592  (nrow, ncol, ncell)*

*resolution : 30, 30  (x, y)*

*extent     : 284715, 367125, -1047765, -953685  (xmin, xmax, ymin, ymax)*

*crs        : +proj=utm +zone=24 +datum=WGS84 +units=m +no_defs* 

*source     : memory*

*names      : layer* 

*values     : 1, 5  (min, max)*

------------------------------------------------------------------------------------------------------------------------------------

-[x] Para fechar com chave de ouro, basta plotar nosso raster e depois salvar para visualizar com maiores detalhes num software GIS.

*plot(result)*

*writeRaster(result, filename = "unclass_kmean.tif")*

![image](https://user-images.githubusercontent.com/67385452/119183862-0a1e3f00-ba4b-11eb-95d6-8c2d412aefa2.png)

![image](https://user-images.githubusercontent.com/67385452/119184070-4782cc80-ba4b-11eb-86cb-83d11b2267ac.png)

### Existem várias maneiras de construção de um script.

#### Sejam criativos.

### Os códigos podem assustar um pouco no começo. Mas quando vocês começarem a desenvolver, ficarão felizes ao analisar e interpretrar os dados.

### Bom trabalho a todos!



























