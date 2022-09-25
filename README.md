# Steps to setup OBP local environment

> System Requirements
> - Java v1.8
> - Maven 3.8
> - Docker & Docker Compose
> - PostgreSql
> - Git & GitBash
> - python 3


## Project folder structure

 ```bash
consent_flow_obp/ 
├── props
│   └── OBP-API.default.props
├── docker-compose.yml


 ```

## Setup OBP-API

1.- Clonar el siguiente repositorio dentro de "Documentos" o  raíz "C:\"

 ```bash 
 git clone git@github.com:rengerden/consent_flow_obp.git
 ```

2.- Crear la base de datos con ayuda de Docker Compose

 ```bash 
 docker-compose up -d
 ```

3.- Clonar el proyecto OBP-API

 ```bash 
 git clone git@github.com:OpenBankProject/OBP-API.git
 ```

4.- Dentro del proyecto que se descargo en el paso 1 se encuentra  el archivo OBP-API.default.props, es necesario copiar este archivo  a la ruta del proyecto OBP-API. Para ello ejecute el siguiente comando.

 ```bash
 cp props/OBP-API.default.props OBP-API/obp-api/src/main/resources/props/default.props
 ```
 5.- Compilar y Ejecutar el proyecto

 ```bash 
 mvn install -pl .,obp-commons && mvn jetty:run -pl obp-api
 ```
 6.- Ingresar al portal (localhost:8080) para proceder a registrarte 
 > 6.1.- Debido a que el envio de correos no esta configurado se necesita hacer una aprobación manual del usuario que acabas de registrar, para ello es necesario acceder a la base de datos y hacer una actualizacion de la tabla `authuser`, buscas el registro y modificas el campo `validated` con el valor `true`. 
 De esta forma ya podras iniciar sesión y proceder a obtener tu API Key, la cual es necesaria colocar en los properties del `API-Manager` y `API-Explorer`.
