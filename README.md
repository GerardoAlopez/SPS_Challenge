# SPS_Challenge
Este repositorio es para registrar paso a paso como aprendi a usar ElastricSearch por parte de Apache Lucene y de como completé este reto para la vacante de Data Engineer en SPS.

Uno de los primeros pasas fue investigar sobre ElasticSearch para entender bien su concepto y saber de que se trata. 
En sintesis, es un open source ElastisSearch es parte de ElasticStack un conjugado de elementos que permiten analizar datos, extraer datos, visualizar datos y crear Dashboards.

El tutorial que utilize para aprender sobre ElasticSearch 


![image](https://user-images.githubusercontent.com/101696287/185002165-ed8dd51a-0f16-415b-97c0-551a16cc415b.png)



Task 1. Creacion de un indice

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




