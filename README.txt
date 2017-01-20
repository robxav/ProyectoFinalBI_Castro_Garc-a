*****PROYECTO*****
Diseño e Implementación de un sistema clasificador de sentimientos

*****PROCESO*****
Recolección de datos.
---------------------
Para obtener una fuente de datos se analizó diferentes sitios, ubicando texto referente a comentarios.
La fuente de datos, se analizó, se separaron comentarios y se guardaron en un archivo para su posterior clasificación.

En primeras instancias se definó adjetivos y verbos para su análisis.
Luego, con forme se revizaban los comentarios se necesitaron más atributos.
Los comentarios sin contenido alfanumérico fueron descartados por la falta de información para su análisis (ejm. "...").
Cada paràmetro como adjetivos, verbos y demás fueron comparados con un listado de dichos atributos existentes en el idioma inglés y español para definir su significado positivo o negativo. Cabe mencionar que en el idioma ingles existen adjetivos y verbos con calificativos positivos y engativos sin necesitad de una preposición que niegue la palabra.
La creación del archivo arff. se lo realizó a mano, ya que las diferentes herramientas no brindaban un análisis a profundidad desde nuestra perspectiva y criterio.
El dataset de pruebas se lo hizo de forma manual, debido a la complejidad de la composición de los comentarios y la falta de información brindada por el análisis de herramientas como WORDNET2.1. y RITAWORDNET.

Preguntas.
----------
• ¿Cuándo se alcanza la mejor precisión?
Con un conjunto de atributos y conbinaciones que contesten a la mayor cantidad de datos de prueba.

• ¿Es importante el número de atributos (features) en el clasificador?
SI, ya que con pocos atributos se puede tener un resultado erróneo, sin embargo al añadir atributos se debe verificar la contraparte de dicho atributo para definir si es necesario añadir mas.

• ¿Es importante el número de instancias?. ¿En qué casos?
SI, dependiendo de los datos que vamos a analizar, ya que un modelo aprende y se adapta a la distribución de los datos, mejorando cuando se tiene un gran numero de datos para um método de discretización.
NO, cuando el numero de datos es pequeño y método a usa es uno de distribución.

• ¿Es importante considerar diferentes pesos para cada atributo? ¿por qué?
SI, debido a valores neutrales obtenidos en el análisis, con pesos se lograría evitar dichos neutrales.

• ¿Está su modelo sobreajustado “overfitted”?
NO, ya que el conjunto de datos y su contenido es diverso e impredecible, denotando en muchos casos malinterpretación en los mismos, como el sarcasmo en las frases.

• ¿Los atributos contínuos son mejores o peores en el clasificador Naive Bayes?
Son peores ya que para clasificarlos es necesario segmentarlos por clase, y calcular la media y la variaza para cada una de ellas.


• Comparar los diferentes algoritmos con su conjunto de datos y determinar cuál de ellos es el que
mejor se ajusta?
Con el algoritmo j48 se ajusta mejor, debido a que el % de error es menor, pese a que en los dos algoritmos el valor de instancias clasificadas corretamente es el mismo.


• ¿Es mejor utilizar validación cruzada (cross-validation) o un test dataset para realizar la evaluación
del clasificardor? ¿Por qué?
El data set ayuda con la variedad de datos de entrada para lograr el entrenamiento más correcto a la realidad, el ajuste del modelo en al clasificación dependerá de la variedad de los datos de entrada.

*****RESULTADOS*****
Pruebas.
--------
Naive Bayes.

=== Stratified cross-validation ===
=== Summary ===

Correctly Classified Instances          54               69.2308 %
Incorrectly Classified Instances        24               30.7692 %
Kappa statistic                          0.4827
Mean absolute error                      0.2635
Root mean squared error                  0.3678
Relative absolute error                 63.3737 %
Root relative squared error             80.4187 %
Total Number of Instances               78     

=== Detailed Accuracy By Class ===

TP Rate   FP Rate   Precision   Recall  F-Measure   Class
  0.925     0.211      0.822     0.925     0.871    si
  0.667     0.211      0.538     0.667     0.596    no
  0.176     0.066      0.429     0.176     0.25     neutro

=== Confusion Matrix ===

  a  b  c   <-- classified as
 37  3  0 |  a = si
  3 14  4 |  b = no
  5  9  3 |  c = neutro

J48.

=== Stratified cross-validation ===
=== Summary ===

Correctly Classified Instances          50               64.1026 %
Incorrectly Classified Instances        28               35.8974 %
Kappa statistic                          0.3857
Mean absolute error                      0.2786
Root mean squared error                  0.4409
Relative absolute error                 67.0158 %
Root relative squared error             96.4037 %
Total Number of Instances               78     

=== Detailed Accuracy By Class ===

TP Rate   FP Rate   Precision   Recall  F-Measure   Class
  0.9       0.342      0.735     0.9       0.809    si
  0.571     0.123      0.632     0.571     0.6      no
  0.118     0.131      0.2       0.118     0.148    neutro

=== Confusion Matrix ===

  a  b  c   <-- classified as
 36  1  3 |  a = si
  4 12  5 |  b = no
  9  6  2 |  c = neutro

Discusión de Resultados.
-------------------------

Obteniendo el resultado de los dos clasificadores, podemos decir que el clasificador Naive Bayes se ajusta a nuestro modelo con mayor precisón.


Conclusiones.
-------------
Tenemos mejores resultados utilizando el clasificador Naive Bayes, ya que el error disminuye en comparación al J48, dependiendo del número de instancias usadas para el entrenameinto.

Consideramos como importantes los atributos: adjetivos (+ -), verbos (+ -), negación de verbos y adjetivos, así como conjunciones y prepocisiones que alteran el sentido de la oración.




*****IMPLANTACIÓN*****
Instalación.
-------------
Debido a que el proyecto no es un ejecutable, se mostrará los pasos para ejecutar los archivos generados.

1. Del repositorio GITHUB, descargarse el archivo proyectobi_sentimientos.arff
2. Desde el programa WEKA abrir el archivo descargado anteriormente. Preprocess --> Open file... --> archivo.arff
3. Desde WEKA, escogemos el algoritmo con el cual trabajaremos en nuestro modelo. Opción Classify --> Choose --> Menu Desplegable --> bayes --> NaiveBayes (algoritmo) --> Start.

Funcionamiento.
---------------
El modelo establece los siguientes atributos.
Adjetivos.
	Los adjetivos son analizados dependiento del tipo de adjetivo, 		si denota positivismo o negatividad. Ejm Alegre (+), Triste (-).
Negaciones de Adjetivos.
	Establece el último significado del adjetivo sea positivo o 	negativo. 
	Ejm. No estoy feliz --> aunq tiene un adjetivo positivo 		tiene 	una negación al mismo, lo cual da como resultado una 		oración negativa.
Verbos.
	Los verbos son analizados dependiendo de su denotación sea 		positiva o negativa. Ejm. Prestar (+), Quitar (-).
Negaciones de Verbos.
	Establece el último significado del verbo dentro de una oración.
	Ejm. Yo no presto (-), Yo no quito (+)
Preposiciones.
	Son conectores positivos o negativos que influyen dentro de 	la oración, negando uan frase completa o dejando de lado un 	significado positivo o negativo.
	Ejm. Me gustan las verduras, pero mi mamá no las cocina. El 	conector "pero" denota un negativisto con la oracion inicial 	positiva teniendo uan segunda frase negativa y con ayuda del 	conecto despeja la oracion a un significado negativo.

Clasificación.
--------------
Teniendo los valores de los atributos antes mencionados, solamente deberá establecer el valor de los positivos y negativos, sin dejar de lado el análisis de los conectores y las negaciones de adjetivos y verbos.
Sin duda existen valores neutros, los cuales se diserniran con el peso de cada atributo.
