# Steps to setup OBP local environment

> System Requirements
> - Java v1.8
> - Maven 3.8
> - Docker & Docker Compose
> - PostgreSql
> - Git & GitBash
> - python 3.9


## Project folder structure

 ```bash
consent_flow_obp/ 
├── props
│   └── OBP-API.default.props
│   └── API-Explorer.default.props
│   └── API-Manager.local_settings.py
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

4.- Dentro del proyecto que se descargo en el `paso 1` se encuentra  el archivo OBP-API.default.props, es necesario copiar este archivo dentro de la ruta `OBP-API/obp-api/src/main/resources/props/` del proyecto OBP-API. Para ello ejecute el siguiente comando.

 ```bash
 cp props/OBP-API.default.props OBP-API/obp-api/src/main/resources/props/default.props
 ```
 5.- Compilar y Ejecutar el proyecto

 ```bash 
 mvn install -pl .,obp-commons && mvn jetty:run -pl obp-api
 ```
 > *Nota* Si al abrir el protal no te aparecen los botones en el lado superior derecho correspondiente a `Register y Logon` lo mas seguro es que tengas un problema por el path del JDK utilizado, debido a los espacios con los que Windows trabaja, la solución es que agregues el JDK a otra ruta por ejemplo `C:\opt\jdk1.8.0_341` y actualizar la variable de entorno JAVA_HOME `setx -m JAVA_HOME "C:\Progra~1\Java\jdk1.8.0_XX"`, con esto reinicias tu consola y vuelves a aplicar los pasos anteriores.
 
 6.- Ingresar al portal (localhost:8080) para proceder a registrarte 
 
 > 6.1  Debido a que el envio de correos no esta configurado se necesita hacer una aprobación manual del usuario que acabas de registrar, para ello es necesario acceder a la base de datos y hacer una actualizacion de la tabla `authuser`, buscas el registro y modificas el campo `validated` con el valor `true`. 
 De esta forma ya podras iniciar sesión y proceder a obtener tu `Conusmer key` y `Consumer Secret`, la cual es necesaria colocar en los properties del `API-Manager` y `API-Explorer`.
 
 7.- Inicia sesion en el portal y da click en `Get API Key` completa el formulario y guarda la información que te proporciona, debido a que no la vuelve a mostrar jamás.
 > **Nota** En el campo de `Redirect URL (Optional)` coloca la URL `http://localhost:8082`

---
## Setup API-Explorer

1.- Clonar el proyecto API-Explorer
 ```bash 
 git@github.com:OpenBankProject/API-Explorer.git
 ```

2.- Dentro del proyecto que se descargo en el `paso 1` se encuentra  el archivo `API-Explorer.default.props`, es necesario copiar este archivo dentro de la ruta `API-Explorer/obp-api/src/main/resources/props/` del proyecto OBP-API. Para ello ejecute el siguiente comando.
```bash
cp props/API-Explorer.default.props API-Explorer/src/main/resources/props/default.props
```
3.- Modificar el archivo default.props agregando tu `Conusmer key` y `Consumer Secret`
> **Importante** 
> Es necesario haber completado el paso 6 y 6.1 de Setup OBP-API para obtener el secret y el key

4.- Procede a ejecutar el proyecto con el siguiente comando
 ```bash 
  mvn -Djetty.port=8082 jetty:run
 ```
> *Nota* Si se siguieron los pasos correctos podras iniciar sesión en el `API-Explorer` a traves del login del `OBP-API` y este te redireccionara al `API-Explorer` automaticamente, en caso contrario podras actualizar el dato `redirect-url` a traves del API `/obp/v5.0.0/management/consumers/CONSUMER_ID/consumer/redirect_url` o acutalizando el dato en la tabla `consumer` busca el registro y actualiza el campo `redirecturl`.

----
## Setup API-Manager


1.- Clonar el proyecto API-Explorer
 ```bash 
 git@github.com:OpenBankProject/API-Manager.git
 ```
2.- Dentro del proyecto que se descargo en el `paso 1` se encuentra  el archivo `API-Manager.local_settings.py`, es necesario copiar este archivo dentro de la ruta `API-Explorer/obp-api/src/main/resources/props/` del proyecto OBP-API. Para ello ejecute el siguiente comando.
```bash
cp props/API-Manager.local_settings.py API-Manager\apimanager\apimanager\local_settings.py
```
> **Nota** En la documantación tienen un error ya que mencionan que debe crear el archivo `local_setting.py` pero le falta una `s`
> 
