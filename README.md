# SPS_Challenge
Este repositorio es para registrar paso a paso como aprendi a usar ElastricSearch por parte de Apache Lucene y de como completé este reto para la vacante de Data Engineer Jr de SPS.

Uno de los primeros pasos fue investigar sobre ElasticSearch para entender bien su concepto y saber de que se trata. 
En sintesis, es un open source desarrolado apartir de Apache Lucene. Es un conjugado de elementos que permiten analizar datos, extraer datos, visualizar datos y crear Dashboards. Conocido por sus API REST simples, naturaleza distribuida, velocidad y escalabilidad, Elasticsearch es el componente principal del Elastic Stack, un conjunto de herramientas gratuitas y abiertas para la ingesta, el enriquecimiento, el almacenamiento, el análisis y la visualización de datos. Comúnmente denominado el ELK Stack (por Elasticsearch, Logstash y Kibana), el Elastic Stack ahora incluye una gran colección de agentes ligeros conocidos como Beats para enviar los datos a Elasticsearch.

El tutorial que utilize para aprender sobre ElasticSearch y la documentacion que utilize 

https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html

![image](https://user-images.githubusercontent.com/101696287/185002165-ed8dd51a-0f16-415b-97c0-551a16cc415b.png)



Task A. Creacion de un indice

1.- Abriendo Dev Tools para la creacion del indice. En este punto no entendia bien la interfaz de usuario (UI) por lo cual tuve que investigar en youtube o en la pagina de elastic como usar esta herramienta.

Los datos son almacenados como Documents files en formato JSON.

Empeze por ingresar comandos basicos para entender mas la dinamica 


![image](https://user-images.githubusercontent.com/101696287/185001578-bf7e02ea-86c3-4c75-bed4-457f667fa603.png)



2.- Creando el indice atraves del JSON. Usando la sintaxis PUT agregamos el nombre que queremos para nuestro indice 


![image](https://user-images.githubusercontent.com/101696287/185001976-11e8c186-019f-41e2-a6f2-c3e3b126e4b6.png)


A la hora de de tratar de almacenar los indices en el documento me salio este error 

![image](https://user-images.githubusercontent.com/101696287/185002504-df3a7f76-c52d-4190-8ec3-2219c136ad57.png)

el error es muy obvio. Al parecer tienes que usar el metodo POST para almacenar en un documento.

Indice log_consultas creado exitosamente 

![image](https://user-images.githubusercontent.com/101696287/185002814-7c5ea1d8-d6f5-44c5-8bea-adb6059a0d97.png)

3.- Obteniendo el mapping y creado el template

Para obtener el mapping del documento creador se utiliza el siguiente comando

![image](https://user-images.githubusercontent.com/101696287/185007222-8fcf2574-4d6e-4cf3-94c4-deff3d69194d.png)

Obteniendo lo siguiente 

![image](https://user-images.githubusercontent.com/101696287/185007294-088b9f5b-16c3-4579-bd1c-ddb8eb99eb0f.png)


como podemos observar del mapping resultante el tipo de los datos concuerdan.

Tuve el problema que al crear el TEMPLATE los corchetes no estaban bien identados por lo cual tarde mas de 30 minutos buscando la identacion correcta. Pero finalmente logre obtener el template del documento

![image](https://user-images.githubusercontent.com/101696287/185009476-b3d657d1-61ba-49da-9d43-06504339c2b8.png)

![image](https://user-images.githubusercontent.com/101696287/185009519-0f422a98-d8da-420b-bf54-ecbbf01f5352.png)

4. Una vez definido tu template cargaras una serie de documentos en tu índice utilizando el archivo que se encuentra en el escritorio: log_consultas.json. Para esto utiliza el API (BULK).

En esta seccion ha sido la que mas me he tardado. Queria cargar los datos directamente del documento JSON estuve viendo documentación y tutoriales pero la manera en lo que lo hacian no entendia del todo. Unos usaron docker y otros desde el bash. Pero creo que se necesitaba installar en la computadora ElasticSearch. Por lo tanto, carge los datos del JSON file directamente a la consola con el API _bulk. Ya que las agregaciones de los datos son demasiadas lineas solo capture las primeras por cuestiones practicas. 
 

![image](https://user-images.githubusercontent.com/101696287/185020651-1ea55a2a-07ee-4ea4-beba-6326569eae43.png)

Al hacer el query con el siguiente comando en el documento  

![image](https://user-images.githubusercontent.com/101696287/185020753-eb3e1561-b97b-4670-b02a-16eafaff7093.png)

observamos si se habian cargado de manera correcta los datos, obtenemos:

![image](https://user-images.githubusercontent.com/101696287/185020947-764899f7-7035-4603-a7fd-e6d3c2560d5c.png)

Al observar el valor de "Values" obtenemos 300 que son los indices que tenemos de la agregacion de los datos.


TASK B. Realizar  busquedas sobre indices

Los tutoriales que utlize para este parte fueron

BASIC QUERIES DSL

https://www.youtube.com/watch?v=UStLBiVQ-M0&t=89s

COMPOUND QUERIES(QUERIE DSL)

https://www.youtube.com/watch?v=ybu8XwbwXCQ

Para utilizar el API de "_search" tuve que incurrir en documentacion por parte de elastic y tutoriales de youtube. Hay dos maneras de hacer queries, la primera es directamente sobre el comando "_search" y el otro con un comando JSON con la palabra clave "query"

Ejemplo.- GET "target"/_search?q=* -- hace un query que despliega todo. Lo mismo que un SELECT * FROM TABLE_NAME:

Ejemplo.- GET "target"/_search 

            {
            
            "query": "parameters" 
            
            }

Este ultimo tiene mas juego de consulta

1.- Obtener el número de registros con estado_consulta igual a error y consumo.

Obteniendo registro de error

Query

![image](https://user-images.githubusercontent.com/101696287/185027894-15bdb619-e5a6-4cd8-ae03-fc499bd86ab8.png)

Results

![image](https://user-images.githubusercontent.com/101696287/185027985-d31f15bf-d861-470e-b0e5-b9ea6ffcc087.png)

Obteniendo registros de consumo

Query

![image](https://user-images.githubusercontent.com/101696287/185028058-5b451a99-45fb-4b29-9809-ec29e8d088ab.png)

Results

![image](https://user-images.githubusercontent.com/101696287/185028115-c99513ec-a5a3-4b53-b57d-37c8944a797a.png)

2. Obtener el número de registros realizados por el administrador Juan Lara.

Query 

![image](https://user-images.githubusercontent.com/101696287/185028383-9e217708-8174-4bcf-a9fe-415888011a8a.png)

Results

![image](https://user-images.githubusercontent.com/101696287/185028420-3ff94c48-b67b-4c26-993a-bbe1c923f101.png)

3. Obtener el número de registros con estado_consulta igual a informativo y servicio igual a borrado
Consulta extra

Query

![image](https://user-images.githubusercontent.com/101696287/185028702-4b102940-e84d-482b-8f86-579207b8b424.png)


Results

![image](https://user-images.githubusercontent.com/101696287/185028721-94aa45e5-8ca8-4cd4-b0be-06bb663f920d.png)

4. Obtener la suma de los valores en consultas_realizadas con estado_consulta igual a error.

Este query ocupa del metodo de agregacion lo cual es otra forma en la que se puede consultar los datos en elasticSearch

NOTA: Algo que en este punto logre comprender que ElasticSearch es un base de datos NoSQL del tipo documento. Es decir, que los datos son almacenados como documentos donde cada dato es considerado un "documento", son almacenados en forma de JSON o XML. Ademas de que ElasticSearch tiene escalacion horizontal, quiere decir, que podemos agregar cluters o nodos para aumentar la capacidad de almacenamiento.

Query 

![image](https://user-images.githubusercontent.com/101696287/185031054-13e086e1-3047-477c-a9ba-fb6833c76dc4.png)


Results

![image](https://user-images.githubusercontent.com/101696287/185031099-ee24837a-cfd8-4206-aebf-cb9d1c6ba8c5.png)
![image](https://user-images.githubusercontent.com/101696287/185031138-5285131e-29cf-4094-87e9-4293cb7f181b.png)


TASK C. Realizar un tablero para visualizar información de empleados

1. Vista de heat map, donde mostraras el número de servicios realizados por administrador.

Para esta parte tuve el problema donde los datos me aparecian sin ningun valor. Esto se debio a que el timestamp de los datos estaba fuera de rango. En este problema dure alrededor de una hora buscando documentacion y ayuda en foros como StackOverflow. Lo bueno de la GUI de Kibana que es muy interactiva y como tengo experiencia usando Cogno Analytics de IBM Cloud la cual tiene una misma intefaz de usuario parecida, se me hizo bastante intuitivo realizar las vizualizaciones. 

![image](https://user-images.githubusercontent.com/101696287/185042676-2a22db6d-394c-48ae-aa5c-ba73e53f6dca.png)

Una vez cambiado estos filtros donde solamente coloque la fecha que correspondia en el timestamp los datos se pusieron como disponibles.

Metiendo correctamente los datos en eje el filtro de timestamp, obtenemos el siguiente Heat Map:

![image](https://user-images.githubusercontent.com/101696287/185044204-ff0a397d-7bfb-490a-a046-4680e0b68650.png)

2. Vista de Barras, donde se grafique el número de registros con estado_consulta igual a error a través
del tiempo.

Obtenemos:


![image](https://user-images.githubusercontent.com/101696287/185048239-a461b978-0733-4241-bd30-521cb4212012.png)


##EXTRA. genera un tablero con las 2 visualizaciones que acabas de crear.

Creacion del dashboard con las dos visualizaciones creadas en la tarea anterior 

![image](https://user-images.githubusercontent.com/101696287/185048546-fe74e54c-3df7-4ce9-a09f-741acc122612.png)

https://sps-test.kb.us-east-2.aws.elastic-cloud.com:9243/app/r/s/edrsH



