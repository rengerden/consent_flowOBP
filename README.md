# Steps to setup OBP local environment

> System Requirements
> -- Java v1.8
> -- Maven 3.8
> -- Docker & Docker Compose
> -- PostgreSql
> -- Git & GitBash


## Project folder structure

 ```bash
consent_flow_obp/ 
├── props
│   └── OBP-API.default.props
├── docker-compose.yml


 ```

## Setup OBP-API

1.- Clonar el siguiente repositorio dentro de "Documentos" o  raíz "C:\"

`git clone git@github.com:rengerden/consent_flow_obp.git`

2.- Crear la base de datos con ayuda de Docker Compose

`docker-compose up -d`

3.- Copiar el archivo OBP-API.default.props a la ruta del OBP-API`

`cp props/OBP-API.default.props OBP-API/obp-api/src/main/resources/props/default.props`
 4.- Compilar y Ejecutar el proyecto

`nohup ./mvn.sh clean install -pl .,obp-commons && ./mvn.sh jetty:run -pl obp-api`
