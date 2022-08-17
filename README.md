# SPS_Challenge
Este repositorio es para registrar paso a paso como aprendi a usar ElastricSearch por parte de Apache Lucene y de como completé este reto para la vacante de Data Engineer en SPS.

Uno de los primeros pasas fue investigar sobre ElasticSearch para entender bien su concepto y saber de que se trata. 
En sintesis, es un open source ElastisSearch es parte de ElasticStack un conjugado de elementos que permiten analizar datos, extraer datos, visualizar datos y crear Dashboards.

El tutorial que utilize para aprender sobre ElasticSearch 


![image](https://user-images.githubusercontent.com/101696287/185002165-ed8dd51a-0f16-415b-97c0-551a16cc415b.png)



Task A. Creacion de un indice

1.- Abriendo Dev Tools para la creacion del indice. En este punto no entendia bien la interfaz de usuario (UI) por lo cual tuve que investigar en youtube o en la pagina de elastic como usar esta herramienta.

Los datos son almacenados como Documents files en forma de JSON

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

En esta seccion ha sido la que mas me he tardado. Queria cargar los datos directamente del documento JSON estuve viendo documentación y tutoriales pero la manera en lo que lo hacian no entendia del todo. Unos usaron docker y otros desde el bash. Pero creo que se necesitaba installar en la computadora ElasticSearch. Por lo tanto, carge los datos del JSON file directamente a la consola con el API _bulk. Ya las agregaciones son demasiadas lineas solo capture las primeras por cuestiones practicas. 

![image](https://user-images.githubusercontent.com/101696287/185020651-1ea55a2a-07ee-4ea4-beba-6326569eae43.png)

Al hacer el query con el siguiente comando en el documento  

![image](https://user-images.githubusercontent.com/101696287/185020753-eb3e1561-b97b-4670-b02a-16eafaff7093.png)

observamos si se habian cargado de manera correcta los datos, obtenemos:

![image](https://user-images.githubusercontent.com/101696287/185020947-764899f7-7035-4603-a7fd-e6d3c2560d5c.png)

Al observar el valor de "Values" obtenemos 300 que son los indices que tenemos de la agregacion de los datos.


TASK B. Realizar  busquedas sobre indices

Para utilizar el API de "_search" tuve que incurrir en documentacion por parte de elastic y tutoriales de youtube. Hay dos maneras de hacer queries, la primera es directamente sobre el comando "_search" y el otro con un comando JSON con la palabra clave "query"

Ejemplo.- GET "target"/_search?q=* -- hace un query que despliega todo lo mismo que un SELECT * FROM TABLE:

Ejemplo.- GET "target"/_search 
            {
            
            "query": "parameters" 
            
            }

Este ultimo tiene mas posibilidades de consulta

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




