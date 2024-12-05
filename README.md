## **Introduccion**
---
Dentro de esta libreta, se pueden encontrar bastantes, bastantes y bastantes mas lineas de codigo en donde se puede apreciar el proceso de aprendizaje que tuvimos como equipo durante todo el semestre. Iniciando con la busqueda de datasets, pasando por los procesos de limpieza y analisis y terminando por el uso de spark y machine learning.

Nuestro objetivo originalmente era agarrar bastantes datasets con miles y diezmiles datos diferentes para ver si podiamos encontrar una relacion entre ellos.
Al principio teniamos varias ideas, ya sea sobre la educacion, sobre como los salarios afectaban ciertas comunidades, el como los crimenes se pueden ver afectados por diferentes factores, etc.
Finalmente tomamos la decision de concentrarnos en dos conclusiones. Los crimenes de odio, y los suicidios que podrian generar estos.

Veran, durante todo el proyecto nuestro plan era mayormente ver como los salarios, los indices de trabajo o los impuestos afectaban en esto, pero mas adeltante les explicaremos porque no se pudo cumplir con eso.

Ahora, vamos a pasar por todo el proceso de la libreta para explicar el porque o como fue que hicimos lo que hicimos.

## **Parte 1. Limpieza de Datos**
---
Lo primero que hicimos fue escoger los datasets que usariamos durante todo el proyecto. Desde un inicio tomamos la decision de agarrar multiples datasets en vez de solo uno complicado debido a las oportunidades que puede presentar esto. 
Gracias a esta decision, tuvimos que plantear desde el principio que era lo que ibamos a hacer como equipo.
Primero era limpiar los datos, despues seria ver que conclusiones podriamos sacar con estos, y finalmente implementar algun algoritmo de Machine Learning para probar nuestras teorias.

Inicialmente cargamos los datasets usando pandas debido a que eso era lo que sabiamos hacer. Esto originalmente parecia sencillo pero despues de conocer Spark nos dimos cuenta de las facilidades que incluia este ultimo. Pero por ahora solo era cargar datos, mostrar las tablas y ver que cosas teniamos que modificar para poder manejarlo.

Se utilizo mucho el concepto de DataFrame para manejar todos los datos, principalmente para poder limpiarlos haciendo uso de la funcion .map()
Se veia el dataset, se escogia una columna, se veian los valores unicos y finalmente se creaba el diccionario para el mapeo.

Al llegar al DataFrame de salarios nos encontramos un problema que decidio el camino del proyecto, muchas de las columnas que teniamos eran inutiles o redundantes, o eso pensamos al menos.
Cuando llegamos a 'Title Name' vimos como la columna describia todos los 4700+ nombres de los empleos que podias encontrar en el estado, esto ocasiono muchos problemas debido a la dificultad que era mapearlo y hasta la fecha el diccionario que se creo para poder cumplir esto mide mas de la mitad del proyecto.

Resources/2.png

Pensamos en que muchas de las columnas podian ser ignoradas, o que podriamos escoger mejor solo las columnas que podriamos necesitar y de ahi implementar lo demas.

## **Parte 2. Spark**
---
Despues de considerar cambiar completamente de proyecto, intentar con otras cosas y regresar a este, decidimos implementar todo el proyecto con Spark. 
Primero, que es Spark?
- Spark es una herrameinta creada por Apache para el procesamiento de datos a gran escala. 

Y o dios no sabiamos que lo ibamos a necesitar.

Nuestra aventura con spark inicio facil, se creaba una SparkSession, se escogia un dataset y experimentabamos que era lo que se podia utilizar.
De lo que mas hicimos uso fue del Schema que este incluia

Resources/3.png

El poder ver la informacion del dataset de esta manera fue completamente una bendicion debido a que podiamos escoger que teniamos que limpiar y como.
Pero en general empezabamos a ver todo lo que podiamos lograr. Usabamos las herramientas de sql para crear nuevos dataframes, los modificabamos al gusto, principalmente por 'Year' y nos ayudaba a ver que conclusiones podiamos sacar.

Durante un momento pensamos que podiamos implementar geopy para poder visualizar los datos en mapas de una forma agradable y estetica pero esto se vio como un problema muy grande debido al como estaban organizados los datasets y el como las librerias necesarias eran incompatibles unas con otras.

Por siguiente empezamos a hacer uso de matplotlib para ver la informacion que necesitabamos y poder probar nuestras hipotesis.
Al principio se vieron muchas ideas de graficas que podiamos utilizar para mostrar lo necesario pero nuestros datos eran bastante "stream lined"
Y seguimos experimentand con los salarios. Ya sea en promedios, en totales, por condado, por area, industria, relaciones, etc.

Pero al momento de llegar a los crimenes totales, decidimos usar graficos mas sencillos para mostrar las relaciones.

Y despues de muchoo tiempo conseguimos nuestra primera conclusion. 

Resources/4.png

"Relacion entre Delitos Totales y Promedios de Sueldos"

Nos dimos cuenta el como los delitos eran directamente proporcionales a los sueldos que se encontraban en el estado. 
Mientras mas sueldo existia, menos delitos habia. 
Originalmente esto era nuestra idea debido a que teniamos en la mente la hipotesis de que la gente no tenia que cometer delitos si podian tener una buena vida. Esto se pudo demostrar de una forma muy cruda con la grafica creada.

Despues empezamos a experimentar mas con los otros datasets que teniamos, hate crimes y suicides.
Se utilizaron los mismos metodos para las tablas y sus relaciones.
Al principio se intento probar si la educacion tenia algo que ver con los crimenes de odio que las personas generaban.

Resources/5.png

Esta imagen es importante porque muestra el como ciertos condados de New York tienen muchos mas crimenes de odio que los demas, lo cual debe tener un motivo debido a que uno pensaria que seria mas equitativo.

Despues de el analisis del dataset de suicidios intentamos relacionar los dos pero las limitaciones del dataset nos hicieron cambiar de rumbo.

## **Parte 3. Nuevo Dataset**
---

Los datasets que teniamos eran un poco limitados para lo que queriamos buscar asi que buscamos por algo que teniamos pensado antes. Educacion.
Sera que la cantidad y calidad de educacion por condado influye en lo anterior?
Pues si...
Pero no para lo que teniamos en mente.

Resources/6.png

Resources/7.png

Resources/8.png

Veran, estas imagenes son comparaciones de las graficas de la cantidad de graduados ya sea en universidades publicas, tecnologicas, entre otras, contra los crimenes de odio en esos mismos condados.
En algunas no se puede apreciar bien por la diferencia de orden entre los condados y el nombre de las universidades. Pero se puede notar una cosa. Algunas barras son muy similares. Y no solo en una grafica, en varias. 
Nosotros teniamos pensado que la relacion seria similar a la de los crimenes con el salario. Pero fue lo opuesto. 
La cantidad de alumnos que se graduaban de una universidad era proporcional a la cantidad de crimenes de odio que habia en el mismo condado.

Resources/9.png

Como podemos apreciar en esta grafica, es muy similar la cantidad que hay de ambos.
Y esta fue la segunda conclusion que sacamos. 
Aqui fue cuando decidimos hacer uso de Machine Learning para poder analizar mejor los datos y hacer predicciones para ver si los datos de verdad estaban relacionados.

## **Parte 4. Machine Learning**
---

Usando todo nuestro conocimiento de Spark, decidimos utilizarlo tambien para los modelso que queriamos crear. 
Aqui ira una explicacion mas a detalle de todo porque fue lo que mas se nos dificulto.

Lo primero que vamos a encontrar es los importes que utilizamos durante los modelos. SparkSession para usar spark, y los demas para el modelo.

Resources/10.png

Esta parte es muy importante. Originalmente spark no contaba con ninguna configuracion personalizada debido a que no sabiamos que lo ibamos a necesitar. 
La primera configuracion es para cambiar la carpeta de runtime de spark. Esto es porque al crear el modelo, la carpeta temporal que usaba se quedaba sin espacio muy rapido y no podia continuar el programa. 
Las siguientes 3 configuraciones son para la optimizacion de spark con nuestro equipo debido a que si era muy pesado lo que teniamos en mente.
La ultima fue de lo mas util. Veran, spark por puro concepto cuenta con la arquitectura para poder divir las tareas y procesos en particiones para conseguir una mayor eficiencia en tu programa. Esto fue algo que descubirmos al crear el modelo.

Los pasos basicos que hicimos fueron :

- Cargar los datasets de nuevo.
- Analizar los schemas.
- Limpiar los nulls y espacios.
- Y finalmente unirlos.

Unir los datasets originalmente fue facil.
Se creaba uno nuevo "r1" para explicar que era la primera relacion, se escogian las columnas que se iban a integrar y se avanzaba con el siguiente.
Esto fue asi hasta que se llego a r5 = suicides.
El programa crasheaba al momento de intentar unir este dataset debido a que la estructura de suicides era bastante compleja para los demas datasets. El programa se quedaba sin espacio y se rompia, entonces decidimos dejarlo en r4 y manejar los suicides aparte.

Aqui es cuando llegamos al modelo. El cual estuvo 180 minutos en ejecucion sin avanzar en lo absoluto.
Veran, lo que se estaba haciendo era implementar el algoritmo de RandomForestRegressor (Lo explicaremos mas adelante) para escoger las columnas y el dataset que se utilizaria en el entrenamiento de las predicciones. Todo marchaba bien hasta que llegaba a rf.fit(). Ahi es donde el programa dejaba de avanzar.

Despues de las 3 horas que se estuvo esperando. Empezamos a buscar soluciones. Primero el arreglar el espacio, como vimos anteriormente, se cambio a una carpeta local. Despues el mejorar el hardware prestado. Cada vez iba avanzando mejor. Pero no sucedia nada. Fue ahi cuando se penso en analizar las relaciones para ver cuantos datos estabamos manejando.

Para hacer esto implemento una funcion para agarrar el 1% del dataset y contar los datos. Pero se quedaba atorado igual. Bastante raro no?
Entonces fuimos probando relacion por relacion. R1 con 1000 datos, R2 con 200000 y R3 con 47000000 Millones de datos. Si R3 ya contaba con esta cantidad de datos, el 1% de R4 era exponencialmente mayor (Algo que jamas podemos descubrir debido al tiempo que iba a requerir) ahi fue cuando se implementaron diferentes tecnicas de spark. Se particionaron los datasets para que fuera mas eficiente, se acomodaron las columnas por pariticon para que no existiera un cuello de botella y se tomo la decision de entrenar el modelo con el 1% de R3.

Y finalmente conseguimos 

Resources/11.png

Pero que significa eso?
RMSE es el posible error que tiene el modelo con la relacion de los datos. Mientras mas bajo sea el numero, significa que tiene sentido el modelo. Pero que tan bajo es bajo? Pues en otro intento con otros datos el RMSE era de 600 asi que un 4 esta bastante bien.
El R2: es que tan viable es el modelo escogido para la prediccion que queremos. Cerca de 1 significa muy eficiente. Cerca de 0 significa muy similar a solo sacar el promedio y un numero negativo es que es mucho peor que solo sacar el promedio.
Luego en la tabla podemos ver los datos. Osea que, por cada victima, por cada persona y por cada persona graduada, nos decia la cantidad de crimenes de odio que deberia haber. Esto nos lleva a la tercera conclusion.

Resources/12.png

La prediccion es muy similar a los valores originales. Esto implica que si hay una relacion directa.

Aqui podemos apreciar un mejor analisis de lo parecido que es.

Finalmente intentamos hacer lo mismo con los suicidios pero debido al como manejamos los datasets.

Resources/13.png

Termino siendo muy diferente a lo esperado. Lo unico que se pudo sacar de ahi es que los crimenes de odio y los suicidios si tienen relacion pero el plan original era ver por raza o etnicidad. 

## **Final**

Que nos llevamos? Que aprendimos? Que podriamos mejorar?
Realmente fue de las mejores maneras de aprender a utilizar una herramienta para entender conceptos de lo que seria el Analisis de Datos.
Aprender Spark es de lo mas importante que pudimos llevarnos de esta materia. Es una herramienta bastante completa y eficaz que se puede utilizar para lo que tengas en mente relacionado al analisis de datos. Y aunque nos diera muchos problemas al inicio, es posible que el proyecto se pudo acabar como lo hizo gracias a esta. 

Tal vez no sea mucho pero lo que sacamos del proyecto fueron tres cosas.

- El indice de criminalidad de Nueva York es dependiente de cuanto salario tengan las personas. Creemos que es debido a las necesidades basicas de estas mismas ya que si cuentan con ellas, no se tendria motivo para cometer algun crimen.

- La gente se empieza a volver intolerante despues de pasar por la universidad. Esto no tenemos idea de porque puede suceder. Es algo que nos gustaria investigar mas.

- Los crimenes de odio si influyen en la cantidad de suicidios que hay en el estado. Y aunque no se pudo probar mucho, es posible que tambien tengan que ver las razas de las personas en esto.


Para finalizar, me gustaria comentar sobre el que para mejorar todo lo que hicimos, sera simplemente empezar de cero. Ya que ahora tenemos una idea de Spark, de como hacer uso de los datos y de la cantidad de cosas que se pueden hacer, lo dificil seria el pensar el como podriamos relacionar los datos nadamas. Sigo haciendo uso del ejemplo de los suicidios por raza, debido a la forma en la que agarramos esos datos, no se pudo comparar bien el dataset con la prediccion. Pero gracias a los valores de RMSE y R2 nos podemos dar cuenta de que al menos existen relaciones que se tendrian que investigar mas a fondo. Esto nos da idea de que podemos manejar los datos como queramos y seguir investigando en buscar cosas que pensabamos que entendiamos.