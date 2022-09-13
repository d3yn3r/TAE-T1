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
Las variables son numericas pero tienden a representar informacion de manera categorica (con excepcion de NUMBRANCH que representa su informacion numerica sin representar informacio categorica) , para esto transformaremos los numeros en palabras que definan bien que significan.

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

Una vez identificadas las variables aplicamos el one hot encoding , asi creamos variables numericas dentro del rango de 1 y 0 que describen la situacion.

Lo siguiente sera correr los codigos para la curva de codo el cual nos indicaran un buen k , para el metodo de k-means
## Curva del codo

Para la curva del codo la primera inclinación importante la tomaremos en k=3

![](https://github.com/d3yn3r/TAE-T1/blob/main/Imagenes_2/codo.PNG)

## Estadistico de Gap
El estadistico de gap nos muestra una grafica en cual el primer cambio positivo ocurre en k=3 , al igual que en la curva del codo

![](https://github.com/ancgarciamo/Clustering-Uni-Score/blob/main/Imagenes/GAP.png)

## Coeficiente de la silueta 
El coeficiente mas alto es con k=5 , sin embargo como está muy cerca de k=3 y como k=3 es de las mejores elecciones desde los metodos anteriores , para el clustering se usará k-means con k=3 

![](https://github.com/ancgarciamo/Clustering-Uni-Score/blob/main/Imagenes/siluetas%20puntajes.PNG)
![](https://github.com/ancgarciamo/Clustering-Uni-Score/blob/main/Imagenes/K2.png)
![](https://github.com/ancgarciamo/Clustering-Uni-Score/blob/main/Imagenes/K3.png)
![](https://github.com/ancgarciamo/Clustering-Uni-Score/blob/main/Imagenes/K4.png)
![](https://github.com/ancgarciamo/Clustering-Uni-Score/blob/main/Imagenes/K5.png)
![](https://github.com/ancgarciamo/Clustering-Uni-Score/blob/main/Imagenes/K6.png)
## Dendograma 

![](https://github.com/ancgarciamo/Clustering-Uni-Score/blob/main/Imagenes/dendrograma.png)
## Caracterización
### Grupo 0
El primer grupo se caracteriza que en las regiones mas a las cuales tienen indice mas alto son “Rocky Mountains” , “Far West” y “Outlying areas” tiendan a ser las que mantienen una titulacion mas alta, asi mismo las instituciones privadas sin esperar beneficios tambien son las que mantienen una titulacion mas alta.


![](https://github.com/ancgarciamo/Clustering-Uni-Score/blob/main/Imagenes/Grupo%200.png)


### Grupo 1
En el segundo grupo las cosas son parecidas pero es más equilibrado , ahora todas las regiones tienden a ser iguales respecto a la titulación más alta que posean 

![](https://github.com/ancgarciamo/Clustering-Uni-Score/blob/main/Imagenes/Grupo%201.png)

### Grupo 2
Este es el grupo con menos datos y está enfocado a las instituciones que mantienen más su titulación más alta y tendiendo a ser de regiones más al oeste, lo mismo siendo instituciones que sean privadas sin esperar beneficios.

![](https://github.com/ancgarciamo/Clustering-Uni-Score/blob/main/Imagenes/Grupo%202.png)

Un buen grupo seria el primero ya que es el que tiene muestras mas balanceadas de las instituciones siendo el que da un mejor panorama, que casos aislados como el grupo 2 o que tienden hacia un lado como el grupo 0.

## Propuesta
Para poder implementar esto a colombia , se podria aplicar un sondeo similar buscando donde se ubica cada institucion en el pais , cual es la maxima titulación que obtienen y que tipo de organizacion es.
