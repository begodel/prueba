
**CORE_SEGURIDAD_FILTER: **Filtro de Seguridad para aplicaciones FW2 

MANUAL DE USUARIO DEL FILTRO DE SEGURIDAD PARA APLICACIONES DE FRAMEWORK 2 O FRAMEWORK 2R

Versión 2.2.0

**Área de Arquitectura de Aplicaciones y Plataformas de Identidad Digital**

# INTRODUCCIÓN
## Audiencia objetivo
Este documento va dirigido a todos aquellos desarrolladores de aplicaciones framework 2 y 2R para mejorar la seguridad de sus aplicaciones.
## Conocimientos previos
Para un mejor entendimiento de este documento se recomienda tener conocimientos en:
-   Java
-   Framework 2 y Framework 2R
-   Configuración de Servlets (web.xml).
-   Framework 2.
-   Filtros http.

# DESCRIPCIÓN
El presente documento es una guia para la utilización del filtro de seguridad en aplicaciones de FW2. En el se describen los pasos necesarios para incluir el filtro y configurarlo.

El motivo para la creación del filtro de seguridad es que las aplicaciones Web pueden sufrir ataques de distintos tipos para obtener información de los usuarios y de los sistemas que utilizan estas aplicaciones (Servidores, BBDD, etc). Con el objetivo de evitar algunos de estos ataques, se ha creado un filtro HTTP denominado filtro de seguridad que analiza todas las peticiones recibidas por una aplicación buscando indicios de estos ataques e impidiendo que se ejecuten. Este filtro de seguridad comprueba los ataques de tipo SQL Inyection y XSS verificando las cabeceras, los parámetros y el querystring de cada una de las peticiones.

El filtro también comprueba que todas las cookies de la aplicación sean seguras, siempre que el protocolo de la aplicación sea https, haciendolas si no lo son.

Además, comprueba que la JSESSIONID tenga el atributo HttpOnly, incluyendoselo si no lo tiene, para que no se pueda obtener desde scripts. Esto hace que las aplicaciones seán menos vulnerables a otros tipos de ataques.

Este filtro de seguridad se puede utilizar en todas las aplicaciones Web de framework 2. Se instala a nivel de servidor para que las aplicaciones simplemente tengan que configurarlo. La instalación del filtro se va a realizar únicamente en los servidores que contienen aplicaciones de FW2.

En aplicaciones de FW2, el uso del filtro de seguridad requiere la actualización de la librería de Sistemas, al menos a la  versión versión 2.6.0 en aplicaciones instaladas en servidores Weblogic 11 y Sistemas  version 2.8.0 en aplicaciones instaladas en servidores Tomcat 7.

El filtro de seguridad es básicamente una librería java (core-seguridad-filter-2.2.0.jar) que requiere para su ejecución las librerias log4j-1.2.17.jar y esapi-2.1.0.jar. Esta librería se encarga de realizar comprobaciones sobre las peticiones que se realizan a una aplicación buscando posibles ataques.

Además de estas librerías java, el filtro requiere una serie de ficheros de configuración que definen el comportamiento del filtro de forma general. Estos ficheros son aplicacion.ctrl y sentencias.npe, el primero permite configurar para que aplicaciones esta activo el filtro y el segundo contiene la lista de negra de sentencias SQL utilizadas en el analisis de ataques de tipo SQLInyection.

Además de los ficheros anteriormente indicados, el filtro modifica su comportamiento con un fichero que se incluye en cada una de las aplicaciones, listaBlancaSQL.npe. Este fichero define las sentencias SQL que debe ignorar el filtro a la hora de comprobar ataques de tipo SQLInyection.

En los apartados de instalacion y configuración se indica como instalar el filtro en un entorno local, incluirlo en una aplicación y configurarlo.

A continuación se detallan las comprobaciones realizadas por el filtro de seguridad:

## Ataques de tipo SQL Inyection:
Los ataques de inyeccion de SQL se realizan incluyendo sentencias SQL dentro de parámetros de aplicación o añadiendo estas mismas sentencias en el QueryString para conseguir que la aplicación al ejecutar una consulta devuelva más información de la que debe. Para evitar que se realicen estos ataques se pueden buscar en las request de las aplicaciones sentencias utilizadas de forma común para realizar estos ataques.

La comprobación de SQL Inyection en el filtro de seguridad se realiza mediante un sistema de lista negra general que contiene las sentencias SQL que se pueden utilizar para realizar este tipo de ataque y lista blanca particular con las sentencias que es necesario ignorar en cada aplicación para su correcto funcionamiento.

La lista negra se ha definido en un fichero plano de texto que se encuentra en el servidor de aplicaciones para poder actualizarlo de forma independiente a las aplicaciones

La lista blanca de la aplicación se define a nivel de aplicación, incluyendo un fichero en la propia aplicación, para poder personalizar las sentencias permitidas. Este fichero no es imprescindible, de hecho, si no existe, la lista blanca que se utiliza estará vacia.

Para realizar la comprobación el filtro elimina las sentencias definidas en la lista blanca y valida el resto de la cadena contra la lista negra (sentencias NO permitidas).

## Ataques de tipo XSS
Los ataques de XSS se realizan incluyendo texto que contiene scripts ejecutables en parámetros de aplicación o modificando el QueryString de una petición para incluir en la petición el texto el script. Al realizar estas acciones se pretende que la aplicación incluya de forma involuntaria script que permiten al atacante obtener información que no tendría que tener accesible de la propia aplicación o de los usuarios que la utilizan.

La comprobación de XSS que realiza el filtro de seguridad busca este tipo de scripts maliciosos en cabeceras, parámetros y QueryString de las peticiciones de una aplicación para evitar que se puedan ejecutar en las vistas devueltas por la aplicación. Para realizar esta comprobación se utilizan una serie de patrones comunes para buscar estos scripts.

## Cookies
En cada petición de una aplicación se envian cookies con información de la aplicación o del usuario, cuando la aplicación esta publicada por protocolo seguro, para evitar que estas cookies sean facilmente accesibles el filtro de seguridad comprueba en cada petición que todas tengan el atributo secure activado, si alguna no lo tienen, se actualiza para ponerselo. Este atributo hace que las cookies de la aplicación se envien encriptadas dificultando el acceso a los datos que contienen.

## JSESSIONID
Uno de los datos más importantes de una petición es el identificador de sesión (JSESSIONID), se comprueba si la JSESSIONID tiene el atributo HttpOnly y si no lo tiene se actualiza para que lo tenga. Este atributo evita que la JSESSIONID sea accesible a traves de scripts.

# USO EN FRAMEWORKS

| Framework utilizado                | Framework necesario                            |
|------------------------------------|------------------------------------------------|
| FW2R                               | FW2R (1.0.0)                                   |
| FW2 WEBLOGIC               | FW2 (2.6.0)             | 
| FW2  TOMCAT 7               | FW2 (2.8)             | 
| ATLAS 1                            | NO APLICA                                    |
| ATLAS 2                            | NO APLICA                                    | 

Para poder utilizar el filtro de seguridad, es necesario por supuesto tener el filtro incluido en la aplicación y configurado a través de los ficheros indicados en los apartados siguientes.

Además es necesario que la aplicación se ejecute en un servidor de aplicaciones que se inicie con una JVM 1.6 o superior y por supuesto, que la aplicación este compilada con una JVM 1.6 o superior. 

Las pruebas con el filtro de seguridad se han realizado con WL11 (jrmc-4.0.1-1.6.0) y con Tomcat7 (jdk1.8.45).

## FRAMEWORK 2

La librería esta disponible en artifactory y se puede descargar a través del siguiente enlace:
[*http://intranet.comunidad.madrid/artifactory/icm-local/org/madrid/core/lib/core-seguridad-filter-lib/2.2.0/core-seguridad-filter-lib-2.2.0.jar*](http://intranet.comunidad.madrid/artifactory/icm-local/org/madrid/core/lib/core-seguridad-filter-lib/2.2.0/core-seguridad-filter-lib-2.2.0.jar)

Si se quiere hacer debug sobre esta librería se pueden descargar los fuentes de la misma en el enlace:
[*http://intranet.comunidad.madrid/artifactory/icm-local/org/madrid/core/lib/core-seguridad-filter-lib/2.2.0/core-seguridad-filter-lib-2.2.0-sources.jar*](http://intranet.comunidad.madrid/artifactory/icm-local/org/madrid/core/lib/core-seguridad-filter-lib/2.2.0/core-seguridad-filter-lib-2.2.0-sources.jar)

## FRAMEWORK 2R

La dependencia a incluir en el fichero pom.xml en proyectos mavenizados es la siguiente
----------------------------------------------------------------------------------------------------------
  pom.xml
-------------------------------------------------------------------------------------------------
```xml
  ...
  <dependencies>
  ...
    <dependency>
      <groupId>org.madrid.core.lib</groupId>
      <artifactId>core-seguridad-filter-lib</artifactId>
      <version>2.2.0</version>
    </dependency>
  ...
  </dependencies>
  ...
```
----------------------------------------------------------------

En las aplicaciones FW2R la dependencia de esta librería esta definida en el pom padre de los proyectos web por lo que no es necesario incluir la dependencia en el pom.

**¿Como comprobar si tenemos la dependencia en nuestro proyecto?**

Se puede comprobar facilmente viendo las dependencias del proyecto con la vista DependencyHierarchy de eclipse o por linea de comandos (siempre que se tenga correctamente configurada la versión de maven e incluida la ruta de la misma en el path) ejecutando el comando mvn dependency:tree 

## CONFIGURACION 
La configuración es igual en ambas versiones del framework.

### Configuración del filtro en la aplicación (web.xml):

Para utilizar el filtro de seguridad en una aplicación hay que modificar la configuración de la aplicación incluyendo el filtro en el fichero web.xml la configuración del filtro:

----------------------------------------------------------------------------------------------------------
  web.xml
-------------------------------------------------------------------------------------------------
```xml
<?xml version="1.0" encoding="UTF-8"?>
  <web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns="http://java.sun.com/xml/ns/j2ee"
           xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee
                               http://java.sun.com/xml/ns/j2ee/web-app_2_5.xsd"
           version="2.5">
    <display-name>xxxxxx</display-name>
    <distributable/>
    ...
    <filter>
      <filter-name>seguridadFilter</filter-name>
      <filter-class>seguridad.filtros.SeguridadFilter</filter-class>
    </filter>
    ...
    <filter-mapping>
      <filter-name>seguridadFilter</filter-name>
      <url-pattern>*.icm</url-pattern>
    </filter-mapping>
    <filter-mapping>
      <filter-name>seguridadFilter</filter-name>
      <url-pattern>*.htm</url-pattern>
    </filter-mapping>
    <filter-mapping>
      <filter-name>seguridadFilter</filter-name>
      <url-pattern>/dwr/*</url-pattern>
    </filter-mapping>
    ...
  </web-app>
```
----------------------------------------------------------------------------------------------------------

En este caso el mapeo del filtro se ha configurado para analizar las peticiones de los servlets de FW2, en el caso de otras aplicaciones dependiendo de los framework que utilice el mismo se deben mapear las extensiones que representen peticiones al servidor (por ejemplo en el caso de Struts se mapearia el filtro a las peticiones .do).

###Configuración de trazas del filtro:

El filtro de seguridad esta preparado para utilizar log4j y log4j2, dependiendo del sistema de trazas que este disponible a nivel de servidor y aplicación.

#### Log4j - FRAMEWORK 2:

En aplicaciones de FW2 el servidor weblogic carga como sistema de trazas log4j, por lo tanto se debe incluir en la carpeta en la que se encuentran los fuentes de la aplicación /java/fuentes/src/ el fichero log4j.properties donde se debe realizar la configuración de las trazas para el paquete del filtro org.madrid.core.filtro.

Como en FW2 se utiliza un sistema de trazas propio no se podrán incluir las trazas del filtro de seguridad junto con las trazas de la aplicación y se debe definir como fichero de salida un fichero que se localice en la misma ruta que el fichero de log de la aplicación /usr/aplic_ICM/logs/xxxxxxxx/ donde xxxxxxxx corresponde con el nombre del módulo técnico. 

El nombre del fichero recomendado es xxxxxxx_seguridadFilter.log donde xxxxxxxx corresponde con el nombre del módulo técnico.

En local se puede activar el appender de consola para que al ejecutar el servidor desde eclipse se muestren las trazas del filtro directamente en la consola, pero para el resto de entornos NO debe estar activado este appender.

En las aplicaciones de FW2, se creará este fichero en la carpeta de fuentes como se ha indicado anteriormente y se creara una copia para cada uno de los entornos:

-   /java/ear/desarrollo/
-   /java/ear/validacion/
-   /java/ear/produccion/

De esta forma se podrá definir diferente nivel de trazas según el entorno. Es importante que en producción el nivel de trazas se deje como máximo a INFO.

A continuación se muestra el contenido de un fichero log4j.properties de ejemplo con el nombre del modulo tecnico ejpl_fw2_web:

----------------------------------------------------------------------------------------------------------
  Log4j.properties
-------------------------------------------------------------------------------------------------
  ```xml
  # Define el nivel de registro para el root logger
  log4j.rootLogger=INFO, file
  #log4j.rootLogger=INFO, stdout, file
  # Configuración del appender de consola
  #log4j.appender.stdout=org.apache.log4j.ConsoleAppender
  #log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
  #log4j.appender.stdout.layout.ConversionPattern=%d{HH:mm:ss.SSS} [%t] %-5p %c{1} - %m%n
  # Configuración del appender de archivo con rotación diaria para el filtro de seguridad.
  log4j.appender.file=org.apache.log4j.RollingFileAppender
  log4j.appender.file.File=/usr/aplic_ICM/logs/ejpl_fw2_web/ejpl_fw2_web_seguridadFilter.log
  log4j.appender.file.MaxFileSize=25MB
  log4j.appender.file.MaxBackupIndex=10
  log4j.appender.file.layout=org.apache.log4j.PatternLayout
  log4j.appender.file.layout.ConversionPattern=%d{HH:mm:ss.SSS} [%t] %-5p %c{1} - %m%n
  #log4j.appender.file.DatePattern='.'yyyy-MM-dd
  # Configuración del logger para el paquete org.madrid.core.filtro
  log4j.logger.org.madrid.filtro=DEBUG, file
```
----------------------------------------------------------------------------------------------------------

#### Log4j2 - FRAMEWORK 2R:

En las aplicaciones de FW2R los servidor Tomcat 9 de MD tiene como sistema de trazas log4j2, todas las aplicaciones de FW2R ya tienen un fichero de configuración para log4j2 (log4j2.xml), en el proceso de migración se define como debe configurarse este fichero utilizando variables que maven sustituye antes de la compilación delproyecto y creación del .war.

Debe incluirse en el fichero log4j2.xml la siguiente configuración para poder dejar las trazas del filtro junto a las trazas de la aplicación. 

La configuración en el fichero log4j2.xml debe incluir los siguientes elementos:

-----------------------------------------------------------------------------------------------------------
  Log4j2.xml
--------------------------------------------------------------------------------------------------
```xml
<?xml version="1.0" encoding="UTF-8"?>
  <Configuration status="INFO">
    <Properties>
      ...
      <Property name="Filtro">${log.filtro}</Property>
      <Property name="logdir">/usr/aplic_ICM/logs</Property>
      <Property name="moduloTecnico">${modulo.tecnico}</Property>
      ...
    </Properties>
    <Appenders>
      ...
      <RollingFile name="APP_FS"
                   fileName="${logdir}/${moduloTecnico}/${moduloTecnico}.seguridadFilter.log"
                   filePattern="${logdir}/${moduloTecnico}/${moduloTecnico}. seguridadFilter.%d{yyyy-MM-dd}.log.gz">
        <PatternLayout pattern=*"${layout}" />
        <CronTriggeringPolicy schedule=*"0 0 0 * * ?" />
        <DefaultRolloverStrategy>
          <Delete basePath="${logdir}" maxDepth="1">
            <IfFileName glob="${moduloTecnico}.filtro_seguridad.log.gz" />
            <IfAccumulatedFileCount exceeds="10" />
          </Delete>
        </DefaultRolloverStrategy>
      </RollingFile>
      ...
    </Appenders>
    <Loggers>
      ...
      <!-- FILTRO SEGURIDAD -->
      <Logger name="org.madrid.core.filtro" level="${Filtro}" additivity="false">
        <AppenderRef ref="APP_FS" level="${Filtro}" />
        <!-- ${log.local} -->
      </Logger>
      ...
    </Loggers>
  </Configuration>
```
--------------------------------------------------------------------------------------------------

Como se puede ver es necesario configurar el Appender con la ruta definida de forma general para las trazas de aplicación, con el nombre especifico que en este caso dependen del módulo técnico y añade '.seguridadFilter' antes de la extensión y configurar el logger para el paquete org.madrid.core.filtro. 

El nivel del logger se define en una variable que como se ha indicado anteriormente obtiene el valor en función del entorno sustituyendolo por el valor de la propiedad log4j.filtro del fichero environment.properties del entorno en el que se ejecute la compilación.

### Configuración adicional:

Además de la librería y la configuración de las trazas, el filtro de seguridad permite incluir configuraciones para excepcionar casos concretos en los que el filtro puede bloquear peticiones que son necesarias para el correcto funcionamiento de las aplicaciones.

Tambien se ha incluido la posibilidad de definir el comportamiento del filtro de forma que se pueda desactivar o poner en modo de traceo para ver que peticiones intercepta como posibles ataques para facilitar la configuración de las excepciones.

### Configuración para excepcionar peticiones:

En muchas aplicaciones se pasan como parámetros sentencias SQL que por norma general el filtro interpretaria como intentos de ataques de inyección SQL. Para controlar que el filtro no bloquee estas peticiones se puede incluir un fichero listaBlancaSQL.npe en el que se pueden definir las diferentes sentencias que es necesario enviar en diferentes peticiones. Este fichero contendrá una sentencia por linea y en caso de existir este fichero el filtro ignorara todas las sentencias incluidas en el al realizar el analisis de las peticiones.

Este fichero se debe incluir en el proyecto en una ruta que se resuelva a nivel de classpath de aplicación, lo que se traduce en FW2 en que debe incluirse en la carpeta /java/fuentes/src y en FW2R en la carpeta /src/main/resource/. 

--------------------------------------------------------------------------------------------------
  listaBlancaSQL.npe
--------------------------------------------------------------------------------------------------
```xml
  SELECT CDPROV FROM XXXX_PROV_EXCLUIDA
  SELECT CDMUNI FROM XXXX_MUNI_EXCLUIDO
```
--------------------------------------------------------------------------------------------------

Con el filtro de seguridad se han detectado en multitud de ocasiones como posible ataque el envio de parámetros con contenido Base 64. Para evitar que el filtro intercepte de forma erronea estas peticiones se puede incluir un fichero llamado listaBlancaB64SQL.npe.

Este fichero contiene por cada linea el Nombre de la acción que necesita el parámetro de tipo Base 64 y la lista de los campos de este tipo que recibe la acción separados los campos por â€˜,â€™ y la acción de los campos por â€˜|â€™

--------------------------------------------------------------------------------------------------
  listaBlancaB64SQL.npe
--------------------------------------------------------------------------------------------------
```xml
  GuardarBD | upB64, pdfB64, logB64
```
--------------------------------------------------------------------------------------------------

### Configuración para modificar el comportamiento del filtro:

En algunas ocasiones, aunque no es muy comun, puede ser necesario para configurar correctamente las excepciones modificar el comportamiento del filtro de seguridad, para ello, se pueden incluir otro fichero de configuración adicional que permite controlar el modo de funcionamiento del filtro, este fichero se llama aplicaciones.ctrl

Este fichero debe incluir el nombre del módulo técnico y el modo de funcionamiento. Valores posible vacio, SKIP y TRACE. 

Si el fichero no se encuentra o se encuentra con el nombre del modulo y valor vacio el filtro funciona normalmente, si el valor es SKIP, el filtro no hace nada y si el valor es TRACE el filtro realiza las comprobaciones, pinta las trazas pero no corta las peticiones.

--------------------------------------------------------------------------------------------------
  aplicaciones.ctrl
--------------------------------------------------------------------------------------------------
```xml
  fw2_web_pub
  fw2_web_pub SKIP
  fw2_web_pub TRACE
```
--------------------------------------------------------------------------------------------------
