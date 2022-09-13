# Clustering-Uni-Score
El siguiente dataset de college scoreboard se usara para una agrupacion y caracterizacion de instituciones, para esto usaremos la tecnica del one hot encoding para variables categoricas y se aplicara el metodo de k-means , de esto sacaremos los grupos y podremos interpretar sus caracteristicas con las nuevas variables obtenidas por el one hot encoding


## Pre-procesamiento de datos
El dataset contiene una dimensionalidad extremadamente alta de 1715 columnas , siendo estas muchas variables , para ello empezaremos por descartar columnas que posean algún dato nulo, dejando únicamente 16 columnas.

usando un código para descartar las variables que no son numéricas, y al final nos quedan 12 columnas con datos unicamente numéricos y sin valores nulos, lo siguiente sera eliminar variables que no son utiles , por ejemplo UNITD,OPEID, opeid6 son simplemente identificadores y no aportan informacion util , variables como st_fips son una representacion de un codigo postal , si bien puede decir informacion del estado de la institucion, tiene demasiados valores distintos para poder presentar efectivamente la informacion.

## Matriz de correlacion
Lo siguiente sera escoger las posibles variables a analizar para aplicar el metodo de k-means, para esto hacemos una matriz de coorelacion y escogemos las variables mas dispersas

![](https://github.com/d3yn3r/TAE-T1/blob/main/Imagenes_2/Mapa%20de%20correlacion.PNG)



Como vemos las variables que quedaron  , en su mayoría casi no se relacionan linealmente con excepcion de HIGHDEG Y PREDDEG , estas tienen una relacion de 0.92 de similitud , por ende eliminaremos una de las 2 , siendo PREDDEG.


## One hot encoding

### Categorizacion
Las variables son numericas pero tienden a representar informacion de manera categorica (con excepcion de NUMBRANCH que representa su informacion numerica sin representar información categorica, por ende se separara de estas variables) , para esto transformaremos los numeros en palabras que definan bien que significan.

#### CONTROL
- 1, Public
- 2, Private nonprofit
- 3, Private for-profit

####  REGION
- 1, New England
- 2, Mid East
- 3, Great Lakes
- 4, Plains
- 5, Southeast
- 6, Southwest
- 7, Rocky Mountains
- 8, Far West
- 9, Outlying Areas

#### HIGHDEG

- 0, Non-degree-granting
- 1, Certificate degree
- 2, Associate degree
- 3, Bachelor's degree
- 4, Graduate degree

#### main
- 1, Main campus
- 0, Branch

#### CURROPER
- 0, Closed
- 1, Operating

#### HCM2
- 0, not under investigation
- 1, under investigation

Una vez identificadas las variables aplicamos el one hot encoding , asi creamos variables numericas dentro del rango de 1 y 0 que describen la situacion, por ende no es necesario normalizarlas.

Lo siguiente sera correr los codigos para la curva de codo y el estadistico de gap los cuales nos indicaran un buen k , para el metodo de k-means
## Curva del codo

Para la curva del codo la primera inclinación importante la tomaremos en k=4

![](https://github.com/d3yn3r/TAE-T1/blob/main/Imagenes_2/codo.PNG)

## Estadistico de Gap
El estadistico de gap si bien en el codigo analisis nos muestra un k alto , en la imagen la tendencia empieza a notarse en un k igual a 4, por ende el k definitivo sera en k=4

![](https://github.com/d3yn3r/TAE-T1/blob/main/Imagenes_2/gap.png)

## Dendograma 

![](https://github.com/d3yn3r/TAE-T1/blob/main/Imagenes_2/dendograma.PNG)

## Caracterización

### Grupo 0




|index|HCM2\_not under investigation|HCM2\_under investigation|main\_Main campus|main\_branch|HIGHDEG\_Associate degree|HIGHDEG\_Bachelor&\#39;s degree|HIGHDEG\_Certificate degree|HIGHDEG\_Graduate degree|HIGHDEG\_Non-degree-granting|CONTROL\_Private Non Profit|CONTROL\_Private for profit|CONTROL\_Public|region\_Far West|region\_Great Lakes|region\_Mid East|region\_New England|region\_Outlying Areas|region\_Plains|region\_Rocky Mountains|region\_Southeast|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|count|2232\.0|2232\.0|2232\.0|2232\.0|2232\.0|2232\.0|2232\.0|2232\.0|2232\.0|2232\.0|2232\.0|2232\.0|2232\.0|2232\.0|2232\.0|2232\.0|2232\.0|2232\.0|2232\.0|2232\.0|
|mean|0\.9995519713261649|0\.00044802867383512545|0\.07347670250896057|0\.9265232974910395|0\.19578853046594982|0\.14381720430107528|0\.3163082437275986|0\.12813620071684587|0\.21594982078853048|0\.11648745519713262|0\.8019713261648745|0\.08154121863799284|0\.1442652329749104|0\.16980286738351255|0\.11738351254480286|0\.042114695340501794|0\.0228494623655914|0\.07840501792114696|0\.036738351254480286|0\.2585125448028674|
|std|0\.02116668783336508|0\.021166687833365082|0\.26097584411121455|0\.2609758441112145|0\.39689539925523026|0\.35098291732803477|0\.465138980945418|0\.33431630199276613|0\.4115718502142815|0\.32088044334176025|0\.3986031898861239|0\.2737258066305532|0\.3514372073424385|0\.37554365985585897|0\.3219488502470152|0\.20089581833450598|0\.14945692429073607|0\.2688681072668232|0\.18816085415388026|0\.4379152056266434|
|min|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|25%|1\.0|0\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|50%|1\.0|0\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|75%|1\.0|0\.0|0\.0|1\.0|0\.0|0\.0|1\.0|0\.0|0\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|1\.0|
|max|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|




### Grupo 1


|index|HCM2\_not under investigation|HCM2\_under investigation|main\_Main campus|main\_branch|HIGHDEG\_Associate degree|HIGHDEG\_Bachelor&\#39;s degree|HIGHDEG\_Certificate degree|HIGHDEG\_Graduate degree|HIGHDEG\_Non-degree-granting|CONTROL\_Private Non Profit|CONTROL\_Private for profit|CONTROL\_Public|region\_Far West|region\_Great Lakes|region\_Mid East|region\_New England|region\_Outlying Areas|region\_Plains|region\_Rocky Mountains|region\_Southeast|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|count|1871\.0|1871\.0|1871\.0|1871\.0|1871\.0|1871\.0|1871\.0|1871\.0|1871\.0|1871\.0|1871\.0|1871\.0|1871\.0|1871\.0|1871\.0|1871\.0|1871\.0|1871\.0|1871\.0|1871\.0|
|mean|1\.0|0\.0|0\.9882415820416889|0\.011758417958311064|0\.4917156600748263|0\.053981827899518976|0\.17530732228754678|0\.27899518973810794|0\.0|0\.0|0\.0|1\.0|0\.13094601817210047|0\.1288081239978621|0\.13201496525921966|0\.05291288081239979|0\.012827365045430252|0\.09727418492784608|0\.042223409941207914|0\.2832709780865847|
|std|0\.0|0\.0|0\.10782565350338312|0\.10782565350338309|0\.5000650186234663|0\.22604225077369675|0\.38033140508643054|0\.4486250598906348|0\.0|0\.0|0\.0|0\.0|0\.33743149476885537|0\.3350770061676981|0\.33859753496594175|0\.22391941923364256|0\.1125592968835758|0\.29640997979036054|0\.2011522298658999|0\.4507073357151385|
|min|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|25%|1\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|50%|1\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|75%|1\.0|0\.0|1\.0|0\.0|1\.0|0\.0|0\.0|1\.0|0\.0|0\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|1\.0|
|max|1\.0|0\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|0\.0|0\.0|0\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|


### Grupo 2

|index|HCM2\_not under investigation|HCM2\_under investigation|main\_Main campus|main\_branch|HIGHDEG\_Associate degree|HIGHDEG\_Bachelor&\#39;s degree|HIGHDEG\_Certificate degree|HIGHDEG\_Graduate degree|HIGHDEG\_Non-degree-granting|CONTROL\_Private Non Profit|CONTROL\_Private for profit|CONTROL\_Public|region\_Far West|region\_Great Lakes|region\_Mid East|region\_New England|region\_Outlying Areas|region\_Plains|region\_Rocky Mountains|region\_Southeast|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|count|1994\.0|1994\.0|1994\.0|1994\.0|1994\.0|1994\.0|1994\.0|1994\.0|1994\.0|1994\.0|1994\.0|1994\.0|1994\.0|1994\.0|1994\.0|1994\.0|1994\.0|1994\.0|1994\.0|1994\.0|
|mean|0\.9658976930792377|0\.034102306920762285|0\.9974924774322969|0\.0025075225677031092|0\.1534603811434303|0\.05717151454363089|0\.7266800401203611|0\.06018054162487462|0\.0025075225677031092|0\.009528585757271816|0\.9874623871614845|0\.003009027081243731|0\.1715145436308927|0\.1374122367101304|0\.14794383149448345|0\.04513540621865597|0\.027582748244734202|0\.07372116349047142|0\.05616850551654965|0\.2296890672016048|
|std|0\.1815375087951316|0\.1815375087951316|0\.05002489288603876|0\.05002489288603876|0\.3605211170660216|0\.2322282898272719|0\.445775522308945|0\.23788069022567887|0\.05002489288603876|0\.0971726673545019|0\.11129525171907288|0\.05478574716181704|0\.3770525204134602|0\.3443683886852159|0\.35513336060968204|0\.20765313893979767|0\.16381513457974708|0\.2613821276248556|0\.2303045905024387|0\.42073837040134626|
|min|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|25%|1\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|50%|1\.0|0\.0|1\.0|0\.0|0\.0|0\.0|1\.0|0\.0|0\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|75%|1\.0|0\.0|1\.0|0\.0|0\.0|0\.0|1\.0|0\.0|0\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|max|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|

### Grupo 3

|index|HCM2\_not under investigation|HCM2\_under investigation|main\_Main campus|main\_branch|HIGHDEG\_Associate degree|HIGHDEG\_Bachelor&\#39;s degree|HIGHDEG\_Certificate degree|HIGHDEG\_Graduate degree|HIGHDEG\_Non-degree-granting|CONTROL\_Private Non Profit|CONTROL\_Private for profit|CONTROL\_Public|region\_Far West|region\_Great Lakes|region\_Mid East|region\_New England|region\_Outlying Areas|region\_Plains|region\_Rocky Mountains|region\_Southeast|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|count|1707\.0|1707\.0|1707\.0|1707\.0|1707\.0|1707\.0|1707\.0|1707\.0|1707\.0|1707\.0|1707\.0|1707\.0|1707\.0|1707\.0|1707\.0|1707\.0|1707\.0|1707\.0|1707\.0|1707\.0|
|mean|1\.0|0\.0|1\.0|0\.0|0\.04452255418863503|0\.210896309314587|0\.06502636203866433|0\.6608084358523726|0\.018746338605741066|0\.9900410076157|0\.0017574692442882249|0\.008201523140011716|0\.12126537785588752|0\.1616871704745167|0\.22612770943175162|0\.09548916227299356|0\.018746338605741066|0\.1054481546572935|0\.01757469244288225|0\.20210896309314588|
|std|0\.0|0\.0|0\.0|0\.0|0\.20631343158543478|0\.4080644621905965|0\.24664462692156502|0\.4735736803189247|0\.1356675933157729|0\.09932567817803074|0\.041897600231965766|0\.09021655162771752|0\.32653108265361164|0\.3682714772804587|0\.41844538957418015|0\.29397552608207|0\.1356675933157729|0\.30722000869203014|0\.13143798261820724|0\.4016907465712011|
|min|1\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|25%|1\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|50%|1\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|1\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|75%|1\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|1\.0|0\.0|1\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|max|1\.0|0\.0|1\.0|0\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|1\.0|

## Propuesta
Para poder implementar esto a colombia , se podria aplicar un sondeo similar buscando donde se ubica cada institucion en el pais , cual es la maxima titulación que obtienen y que tipo de organizacion es.
