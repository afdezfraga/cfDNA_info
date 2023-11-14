# Methylation x cfDNA, Review interna

## Introducción

### ¿Que es cfDNA?

ADN circulante (Circulating free DNA), también conocido como ADN libre (Cell free DNA) es **ADN que se encuentra en el plasma sanguíneo** y otros fluidos corporales [1].

El ADN circulante se encuentra mayoritariamente en forma de fragmentos de ADN de doble cadena de **70-200 pares de bases (bp)** de longitud y fragmentos más grandes de **hasta 21 kb** (21.000 bp)[2].
Sin embargo, estudios recientes han mostrado que el ctDNA tiende a ser más corto que el cfDNA de celulas normales.

La mayoría de la investigación se ha centrado en el **cfDNA derivado de células tumorales (ctDNA)**, que se encuentra en el plasma sanguíneo y otros fluidos corporales de pacientes con cáncer. A mayores, el cfDNA ha demostrado ser un **biomarcador utíl para muchos otros tipos de procesos biológicos**, como el embarazo, el trasplante de órganos o la enfermedad cardiovascular entre otros.

### ¿Que es la metilación del ADN?

La metilación del ADN es un proceso epigenético que se produce por la adición de un grupo metilo (-CH3) a la citosina, una de las cuatro bases del ADN. 

La metilación del ADN puede cambiar la actividad de un segmento de ADN sin cambiar la secuencia, y cuando se produce en una región promotora, la metilación del ADN puede silenciar la expresión génica. La metilación del ADN también puede desempeñar un papel en la diferenciación celular (especialización de las células) durante el desarrollo embrionario.

Podemos medir la metilación del ADN mediante la secuenciación del ADN por bisulfito (BS-seq), que es una técnica de secueniación de nueva generación que permite la detección de la metilación del ADN a nivel de nucleótido. Si el nucleotido es metilado, la citosina (C) se convierte en timina (T), mientras que si no está metilado, la citosina (C) se convierte en uracilo (C).

### ¿Por que es importante la metilación del ADN en cfDNA?

El cfDNA se esta convirtiendo en el método favorito para la detección de cáncer, ya que es un método no invasivo y se puede obtener mediante una simple extracción de sangre (biopsia líquida). 

Sin embargo, la sensibilidad y especificidad de la detección de cfDNA es baja, por lo que se necesitan biomarcadores adicionales para mejorar la detección de cfDNA.

La metilación del ADN es un biomarcador prometedor para la detección de cfDNA, ya que la metilación del ADN es un evento temprano en la carcinogénesis y se ha demostrado que la metilación del ADN es un biomarcador útil para la detección de cáncer.

## WGBS vs RRBS

** **DISCLAIMER** ** BS-seq no es la única forma de sequenciación de datos para trabajar con metilación (Ver Not_BS-seq.pdf). 
Example 1. -> MeDIP-seq / cfMeDIP-seq (https://doi.org/10.1038/s41586-018-0703-0) ...
Example 2. -> TAPS / cfTAPS (https://doi.org/10.1126/sciadv.abh0534) ...
Example 3. (To confirm) CHIP-seq ???
Example 4. -> (To confirm) Meth + RNA-seq (https://doi.org/10.1080/15592294.2020.1816774) ...

![Seq. methods](./images/SeqMethods.png "https://doi.org/10.3390/biom10121677" )

![Other seq. methods with ONT](./images/meth-seq.jpg "https://doi.org/10.3389/fgene.2021.671057" )



Para medir la metilación del ADN se puede utilizar la secuenciación del ADN por bisulfito (BS-seq).

Dos de los métodos más utilizados para la secuenciación del ADN por bisulfito son el **secuenciación de genoma completo (WGBS)** y el **secuenciación de representación reducida (RRBS)**.

WGBS es un método que analiza los niveles de metilación de todo el genoma y identifica los niveles de metilación a nivel de nucleótido.

RRBS es un método que enriquece las regiones del genoma que contienen citosinas CpG y analiza los niveles de metilación de estas regiones. Esto permite obtener la misma profundidad de cobertura que WGBS en estas regiones, necesitando menos lecturas. La desventaja es que la metilación en areas con poca densidad de CpG no se puede medir, aunque esto normalmente no tiene consecuencias ya que la mayoría de la metilación se produce en regiones con alto contenido CpG.

Elegir entre WGBS y RRBS depende de los objetivos del estudio. En general, la decisión depende del número de muestras que se van a analizar y de la profundidad de cobertura que se necesita. Como RRBS requiere menos lecturas, eso lo hace más barato.

## Plan de acción

cfDNA tiene una aplicción o una ventaja principal. Que permite aplicar la técnica de biopsia liquida. Principalmente esto se utiliza para dettección temprana se cancer.

Entonces, nuestro plan es como podemos aplicar metilación a cfDNA para sacar ventaja de esa biopsia liquida y aprovecharla para detección de cancer.

Sin embargo, no existen muchos softwares que apliquen análisis a este tipo de datos.

## Cuales son los principales objetivos de los papers?

Por un lado la mayoría de los papers se centran en la detteción de cancer, se ha demostrado que el uso de metilacón en cfDNA es un biomarcador prometedor para la detección de cancer. Supera el método anterior, que era la detección de mutaciones en cfDNA, ya que proporciona más información.

En general, el cancer se materializa con Hypermetílación en las islas CpG y Hypometilación en las regiones abiertas del cromatina (y en el resto del genoma).

Aunque sí supera al método anterior, no existen demasiados metodos analiticos que llegen a convertirse propiamente en Software (Ver "Not a Tool"). La mayoría de los papers se centran en uno de estos dos factores.
 - En la **precisión** de la detección de cancer. Y en como seleccionan los biomarcadores para ello.
 - En el **coste** de la implementación clínica de esos metodos. Existen algunos métodos de empresas privadas que cuestan algunos cientos de dolares. El coste de WGBS se sigue reduciendo y mejorando, aun así sigue siendo la opción por defecto para el análisis y desarrollo de métodos.


Y la precisión? en que se basa?
Pues principalmente en los biomarcadores - regiones elegidas para medir la metilación. Pero por que? Pues porque casi todos los papers usan el mismo modelo LASSO+LR+RF. Y por que? Es un modelo que se ha demostrado que sea superior? No, de hecho, si algo es, es inferior. No sé cual es el motivo, simplicidad, facilidad de implementación, copiar el estado del arte anterior, etc. Pero biologicamnete no parece un modelo muy adecuado, porque los patrones de cancer no siguen una distribución lineal entre los distintos biomarcadores. \[[CITA](https://www.cell.com/iscience/pdf/S2589-0042(19)30132-4.pdf)\].


Respecto al coste, un paper propone un nuevo método de secuenciación y otro un nuevo método de analisis de secuencias (que compite con bismark, picard, ...) y en una comparación de costes se dice que bismark es mucho más lento y constoso en memoria.

## Datasets

[TODO] The Circulating Cell-free Genome Atlas (CCGA; NCT02889978) study...

[TODO] The Cancer Genome Atlas... 

## Desafios / Problemas

 - Como detecta cada uno sus biomarcadores? Cada uno elige unos candidatos particulares.

 - El porcentage de ctDNA es bajo. 

 - Con que precisión detecta cada tipo de cancer / TOO ?

 - Precio del tratamiento / método para su implementación clinicamente. (https://doi.org/10.1126/sciadv.abn4030)

 - Según [Drag et. all., Pg. 8/40](https://doi.org/10.1152/physiolgenomics.00086.2020)"__En la actualidad, el mayor reto técnico que dificulta la aplicación clínica de los ensayos de cfADN en los trastornos metabólicos es la lentitud de los plazos y la infraestructura informática que requieren los ensayos basados en NGS y ómicas.__" (con 3 citas)

## Métodos

## Flujo general

Lo normal es que los papers no ofrezcan una herramienta, o nisiquiera codigo GH. Cada uno alinea al genoma de referencia con pre-procesados y post-procesados estandard, utiliza alguna función custom para medir los datos que le interesa de los datos alineados, en particular de los biomarcadores¿? o regiones concretas que ellos han demostrado que son relevantes. Y luego utilizan algun algoritmo de ML para clasificar los datos, generalmente LASSO + LR + RF (LR no debería ser una buena decisión, ver comparativa de ML). 

Es decir, en la mayoría de los papers el foco no está en la velocidad, sino en la precisión, y en la base biológica de los biomarcadores.
En muchos casos hay una falta de calidad en el aspecto "generar Software reusable" para que sea fácil de utilizar para otros investigadores, usuarios, clinicamente, etc.
Posiblemente, aunque aquí me mojo menos, hay una falta de calidad en el uso de los modelos matemáticos subjacentes y en las decisiones de ML asociadas.

### LASSO?

### PanSeer

### DISMIR

Según dicen su modelo es generalizable a más tipos de cancer pero hacen algunas trampitas.
Lo prueban para HCC, entonces, como biológicamente se sabe que los pacientes con HCC presentan diferencias sobretodo en regones hypometiladas se centran en estas regiones. ¿En cuantas de ellas? En tantas como para cubrir los mismos 'bp' que CancerDetector. O sea, que dicen que es generalizable, pero a la hora de probarlo ellos hacen las pruebas aprovechando mucho conocimiento previo. Y tomando decisiones según otras publicaciones.

## Referencias

 1. [Wikipedia](https://en.wikipedia.org/wiki/Circulating_free_DNA)

 2. ["Circulating Tumor Cells and Cell-Free DNA in Pancreatic Ductal Adenocarcinoma"](https://doi.org/10.1016%2Fj.ajpath.2018.03.020)