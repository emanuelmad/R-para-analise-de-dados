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

*class       : SpatialPolygonsDataFrame* 

*features    : 1* 

*extent      : -40.95732, -40.20901, -9.474836, -8.623511  (xmin, xmax, ymin, ymax)*

*crs         : +proj=longlat +ellps=GRS80 +towgs84=0,0,0,0,0,0,0 +no_defs* 

*variables   : 13*

*names       : OBJECTID, GEOCODIGO,      NOME, UF, ID_UF, REGIAO, MESOREGIAO, MICROREGIA, LATITUDE, LONGITUDE, SEDE,    Shape_Leng,   Shape_Area* 

*value       :        2,   2611101, Petrolina, PE,    26, Nordeste, SAO FRANCISCO PERNAMBUCANO,  PETROLINA,   -9.393,   -40.508, True, 2.97917219924, 0.3671855305*

*plot(limite, main = "Petrolina-PE")*






