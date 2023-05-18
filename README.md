<img  align="left" width="150" style="float: left;" src="https://www.upm.es/sfs/Rectorado/Gabinete%20del%20Rector/Logos/UPM/CEI/LOGOTIPO%20leyenda%20color%20JPG%20p.png">
<img  align="right" width="60" style="float: right;" src="https://www.dit.upm.es/images/dit08.gif">


<br/><br/>


# Practica Busqueda y Visualización de Datos - ELK

## 1. Objetivo

- Afianzar los conceptos sobre sistemas de almacenamiento y maniulación de datos
- Conocer y operar con los distintos componentes del Stack de ELK

## 2. Dependencias

Para realizar la práctica el alumno deberá tener instalado en su ordenador:
- Herramienta GIT para gestión de repositorios [Github](https://git-scm.com/downloads)
- Stack [ELK](https://www.elastic.co/es/elastic-stack/)
- Máquina virtual con sistema operativo linux y distribución Ubuntu 22.04 (Disponible en el enlace compartido en moodle) 


## 3. Descripción de la práctica

La práctica plantea un ejercicio que permite ejecutar y desplegar los componentes necesarios para visualizar datos provenientes de un fichero de logs que serán almacenados en elastic search y visualizados con kibana, haciendo uso del stack completo de ELK para dicho propósito.


## 4. Inicializar el entorno.

Para la realización de la práctica se ha provisionado una máquina virtual con sistema operativo linux y distribución Ubuntu. En los recursos de Moodle de la asignatura se acceder al enlace de descarga.

Descarge el fichero de VM con extensión .ova e importelo en virtualbox. 

Dentro de la máquina virtual abra un terminal y realice los siguientes pasos.

Clonar el repositorio de la práctica

```
git clone https://github.com/Big-Data-ETSIT/P9_ELK.git
```
Cambiar la ruta al directorio de la práctica
```
cd ./P9_ELK
```

Iniciar el los uno a uno los componentes del stack de ELK. Para ello las versiones que se deben descargar son las siguientes:

- ElasticSearch 8.7.1
- Logstash 8.7.1
- Kibana 8.7.1

### Inicialización de ElasticSearch:

Una vez que se haya descargado dicho componente, abrir un terminal y  cambiar al directorio donde se encuentran elasticsearch y luego ejecutar los siguientes comandos:


```
cd elasticsearch
bin/elasticsearch
```
Dicho comando iniciará una instancia de elasticsearch de forma predeterminada en `http://localhost:9200` y proveerá de un usuario, contraseña y un token que debemos guardar para posteriormente autenticar nuestra instancia de kibana y logstash

### Inicializar Kibana:

Para arrancar Kibana, es necesario ejecutar el siguiente comando en una nueva terminal usando como directorio de trabajo la carpeta raíz de la instalación de Kibana:

```
cd kibana
bin/kibana
```
La salida de dicho comando proveerá entre otras cosas la URL de acceso a la plataforma web que suele ser de forma predeterminada `http://localhost:5601` 


### Iniciar Logstash

Para iniciar logstash tene,mos que tener en cuenta varias cosas:

Descargar logstash
Descomprimir los datos de ejemplos almacenados en el fichero logs.zip
Referenciar al fichero apache.conf con la configuración en donde se indica tanto el origen como el destino de los logs.

Antes de arrancar el servicio es necesario hacer un par de cambios en el fichero apache.conf de acuerdo a nustra instalación local: para ello debemos cambiar la ruta donde se enuentran los datos de ejemplo, es decir cambiar está línea: `file {path => "/Users/admin/Downloads/P9_ELK/logs"`

Posterioemente debemos añadir el password generado en elastic search para nuestra instalación:

```
elasticsearch {
        hosts => [ "https://localhost:9200" ]

        ssl_certificate_verification => false

        user => "elastic"

        password => "kF=B=oJlDBCBcukRXz0F"
        

    }
```
Una vez que se hayan realizado estos pasos ya se puede iniciar logstash:

```
  cd logstash
  bin/logstash -f "file_path"/apache.conf
  
  Change file_path to path of file where you have stored apache.conf
  
```

En este punto nuestro stack ELK ya se encontraría desplegado y listo para crear visualizaciones de dichos datos por medio de la consola de Kibana.

Finalmente seguir los pasos que se van a proveer en el laboratorio para crear una visualización básica de los datos insertados.

## 5. Tareas a realizar.

Crear una visualización personalizada de los datos de logs donde se muestre un diagrama diferente al mostrado en clases.


## 6. Instrucciones para la Entrega y Evaluación.
El alumno debe subir un fichero pdf a moodle en donde se incluyan las dos capturas solicitadas y una descripción de las mismas.


