# Intrucciones de migracion de FW2 2.6.X A 3.0

## Antes de iniciar la migraci�n a sistemas-3.0, debe comprobarse que la versi�n de sistemas es como m�nimo una 2.6.X, en caso contrario, debe seguirse previamente el manual de migraci�n a sistemas 2.6 (https://intranet.comunidad.madrid/arquitecturasw/index.php/component/jdownloads/send/378-manuales/3259-fw2-migracion-sistemas-2-6-0)

## Informaci�n general de la versi�n 3.0:
La versi�n 3.0 de la librer�a de sistemas esta preparada para el uso de Autologin 3.

Esta versi�n permite el uso de las integraciones CORE al tener las versiones de las librer�as de terceros alineadas con estas librer�as.


## Actualizar librer�as en WEB-INF\\lib
    1. Se debe descargar la librer�a de sistemas de artifactory (http://intranet.comunidad.madrid/artifactory/local-fw2/org/madrid/fw2/sistemas/3.0/sistemas-3.0.jar) y actualizarla en la carpeta /java/fuentes/web/WEB-INF/lib/ del proyecto.

    2. Se debe eliminar la versi�n anterior de la librer�a de sistemas.

## Actualizar otras librer�as del proyecto:

Dependiendo del entorno tecnol�gico en el que se despliegue la aplicaci�n los cambios en las librer�as se realizan de diferente forma:

En versiones anteriores de la librer�a de sistemas las dependencias de esta eran las siguientes:

|            **Versi�n 2.6.X**            |
|-----------------------------------------|
| activation-1.0.1.jar                    |
| apache-mime4j-core-0.7.2.jar            |
| axiom-api-1.2.15.jar                    |
| axiom-compat-1.2.15.jar                 |
| axiom-impl-1.2.15.jar                   |
| axis-1.4.jar                            |
| axis2-adb-1.6.4.jar                     |
| axis2-kernel-1.6.4.jar                  |
| axis2-transport-http-1.6.4.jar          |
| axis2-transport-local-1.6.4.jar         |
| commons-codec-1.2.jar                   |
| commons-fileupload-1.3.1.jar            |
| commons-httpclient-3.1.jar              |
| commons-io-2.2.jar                      |
| commons-lang-2.1.jar                    |
| commons-logging-1.1.1.jar               |
| geronimo-activation_1.1_spec-1.0.2.jar  |
| geronimo-jta_1.1_spec-1.1.jar           |
| geronimo-stax-api_1.0_spec-1.0.1.jar    |
| geronimo-ws-metadata_2.0_spec-1.1.2.jar |
| httpcore-4.2.1.jar                      |
| jaxen-1.1.6.jar                         |
| jfactory-4.2.jar                        |
| jsr311-api-1.1.1.jar                    |
| jstl-1.2.jar                            |
| log4j-1.2.8.jar                         |
| mail-1.2.jar                            |
| neethi-3.0.2.jar                        |
| serializer-2.7.1.jar                    |
| stax2-api-3.1.1.jar                     |
| woden-api-1.0M9.jar                     |
| woden-impl-commons-1.0M9.jar            |
| woden-impl-dom-1.0M9.jar                |
| woodstox-core-asl-4.2.0.jar             |
| wsdl4j-1.6.2.jar                        |
| xalan-2.7.1.jar                         |
| xercesImpl-2.9.1.jar                    |
| xml-apis-1.3.04.jar                     |
| XmlSchema-1.4.7.jar                     |

En la �ltima versi�n de la librer�a de sistemas las dependencias son las siguientes:

|            **Versi�n 3.0**              |
|-----------------------------------------|
| apache-mime4j-core-0.7.2.jar            |
| axiom-api-1.2.15.jar                    |
| axiom-compat-1.2.15.jar                 |
| axiom-dom-1.2.13.jar                    |
| axiom-impl-1.2.15.jar                   |
| axis2-adb-1.6.4.jar                     |
| axis2-kernel-1.6.4.jar                  |
| axis2-metadata-1.6.2.jar                |
| axis2-mtompolicy-1.6.2.jar              |
| axis2-saaj-1.6.2.jar                    |
| axis2-transport-http-1.6.4.jar          |
| axis2-transport-local-1.6.4.jar         |
| commons-codec-1.6.jar                   |
| commons-fileupload-1.3.1.jar            |
| commons-httpclient-3.1.jar              |
| commons-io-2.4.jar                      |
| commons-lang-2.1.jar                    |
| commons-lang3-3.1.jar                   |
| commons-logging-1.1.1.jar               |
| core-anotaciones-lib-2.2.0.jar          |
| core-autologin-cliente-lib-2.2.0.jar    |
| core-autologin-filter-lib-2.2.0.jar     |
| core-autologin-lib-2.2.0.jar            |
| core-cache-lib-2.2.0.jar                |
| core-certificados-lib-2.2.0.jar         |
| core-cliente-rest-lib-2.2.0.jar         |
| core-cliente-ws-lib-2.2.0.jar           |
| core-context-lib-2.2.0.jar              |
| core-criptografia-lib-2.2.0.jar         |
| core-search-lib-2.2.0.jar               |
| core-seguridad-lib-2.2.0.jar            |
| core-seguridad-token-lib-2.2.0.jar      |
| core-util-lib-2.2.0.jar                 |
| geronimo-activation_1.1_spec-1.0.2.jar  |
| geronimo-javamail_1.4_spec-1.7.1.jar    |
| geronimo-jaxws_2.2_spec-1.0.jar         |
| geronimo-jta_1.1_spec-1.1.jar           |
| geronimo-stax-api_1.0_spec-1.0.1.jar    |
| geronimo-ws-metadata_2.0_spec-1.1.2.jar |
| gson-2.8.2.jar                          |
| guava-11.0.2.jar                        |
| httpclient-4.5.2.jar                    |
| httpcore-4.0.jar                        |
| httpmime-4.5.2.jar                      |
| jackson-annotations-2.8.0.jar           |
| jackson-core-2.8.9.jar                  |
| jackson-databind-2.7.9.7.jar            |
| jaxb_icm-1.3.jar                        |
| jaxen-1.1.6.jar                         |
| jjwt-0.8.0.jar                          |
| joda-time-2.8.1.jar                     |
| jsr305-1.3.9.jar                        |
| jsr311-api-1.1.1.jar                    |
| jstl-1.2.jar                            |
| librer�aspdf18-18.jar                   |
| mail-1.2.jar                            |
| neethi-3.0.2.jar                        |
| org.apache.xerces-xercesImpl-2.9.1.jar  |
| serializer-2.7.1.jar                    |
| slf4j-api-1.7.25.jar                    |
| stax2-api-3.1.1.jar                     |
| woden-api-1.0M9.jar                     |
| woden-impl-commons-1.0M9.jar            |
| woden-impl-dom-1.0M9.jar                |
| woodstox-core-asl-4.2.0.jar             |
| wsdl4j-1.6.2.jar                        |
| xalan-2.7.1.jar                         |
| xerces-xercesImpl-2.9.1.jar             |
| xml-apis-1.3.04.jar                     |
| XmlSchema-1.4.7.jar                     |

**NOTA:** Se recomienda revisar las librer�as de la aplicaci�n y limpiar en la m�dida de lo posible aquellas librer�as que no se utilicen en la aplicaci�n.
La librer�as indicadas son las incluidas en la librer�a compartida de weblogic. por lo que en caso de ser necesarias para la compilaci�n del proyecto deben incluirse solo en el directorio java/lib/, nunca en el java/fuentes/web/WEB-INF/lib/


### 1. WEBLOGIC 11

En el caso de que el entorno tecnol�gico se Weblogic 11, se deben actualizar las librer�as compartidas.

## Actualizar la librer�a compartida de FW2 del proyecto

Se debe actualizar el fichero /java/fuentes/web/WEB-INF/weblogic.xml para utilizar la librer�a compartidade la versi�n 3.0.0.0:

```xml
	<library-ref>
		<library-name>fw2-dependencias-FW2</library-name>
		<specification-version>X.X.X.X</specification-version>
		<implementation-version>X.X.X.X</implementation-version>
		<exact-match>true</exact-match>
	</library-ref>
```

Se cambiara por:

```xml
    <library-ref>
		<library-name>fw2-dependencias-FW2</library-name>
		<specification-version>3.0.0.0</specification-version>
		<implementation-version>3.0.0.0</implementation-version>
		<exact-match>true</exact-match>
	</library-ref>
```

Para poder ejecutar en local la librer�a comparida debe descargarse (http://intranet.comunidad.madrid/artifactory/fw2-local/fw2/fw2-dependencias-FW2/3.0.0.0/fw2-dependencias-FW2-3.0.0.0.war) y desplegarse en el entorno local


### 2. TOMCAT 7

En las aplicaciones de FW2 desplegadas en Tomcat 7 no hay librer�as compartidas, por lo que deben actualizarse las librer�as en el directorio java/fuentes/web/WEB-INF/lib. Para actualizarlas, se deben comprobar las librer�as que incluye la aplicaci�n de una en una realizando las siguientes comprobaciones:
 1. Si se encuentra en la lista de dependencias de la versi�n anterior y se encuentran en las de la nueva versi�n: se debe dejar la librer�a.
 2. Si se encuentra en la lista de dependencias de la versi�n anterior, pero no se encuentra entre las de la nueva, se debe eliminar salvo que sea una librer�aa de terceros necesaria para una funcionalidad especifica de la aplicaci�n, para comprobar esto, se puede mover la librer�a y si deja de compilar alguna de las clases del proyecto se debe volver a dejar donde estaba.
 3. Todas las librer�as que se encuentran en la lista de las dependencias de la nueva versi�n se deben incluir.

 Para incluir las nuevas librer�as que hagan falta, se buscaran por el nombre completo y la versi�n en artifactory y se descargaran desde ah�. Si alguna librer�a no se encuentra en artifactory debe comunicarse via mantis.


## Actualizaci�n el filtro de seguridad

Se actualizar� al mismo tiempo la librer�a del filtro de seguridad. Esta librer�a se encontraba normalmente a nivel de entorno, pero en esta nueva versi�n se incluira en el directorio /java/fuentes/web/WEB-INF/lib/. La librer�a a incluir es core-seguridad-filter-lib-2.2.0.jar (http://intranet.comunidad.madrid/artifactory/local-fw2/org/madrid/core/core-seguridad-filter/2.2.0/core-seguridad-filter-2.2.0.jar):

Para completar la actualizaci�n del filtro de seguridad debe actualizarse el mapeo del filtro en el fichero /java/fuentes/web/WEB-INF/web.xml

```xml
  <filter>
    <filter-name>seguridadFilter</filter-name>
 	<filter-class>seguridad.filtros.SeguridadFilter</filter-class>
  </filter>
  <filter-mapping>
    <filter-name>seguridadFilter</filter-name>
    <url-pattern>*</url-pattern>
  </filter-mapping>
```
Cambiamos el filtro y debe quedar as�:
```xml
	<filter>
		<filter-name>seguridadFilter</filter-name>
		<filter-class>org.madrid.core.filtro.SeguridadFilter</filter-class>
	</filter>

	<filter-mapping>
		<filter-name>seguridadFilter</filter-name>
		<url-pattern>*.icm</url-pattern>
	</filter-mapping>

	<filter-mapping>
		<filter-name>seguridadFilter</filter-name>
		<url-pattern>*.htm</url-pattern>
	</filter-mapping>
```

Si la aplicaci�n utiliza dwr se debe incluir adicionalmente:

```xml
	<filter-mapping>
		<filter-name>seguridadFilter</filter-name>
		<url-pattern>/dwr/*</url-pattern>
	</filter-mapping>
```

## Configuraci�n de trazas para librer�as CORE y filtro de seguridad:
Con la actualizaci�n del filtro de seguridad y con el fin de que cada aplicaci�n pueda obtener las trazas del filtro de seguridad mediante MULO, es necesario incluir en las aplicaciones el fichero /java/fuentes/src/log4j.properties.
En este fichero se configurar� un apender general que aplicar� a todas las librer�as que utilicen log4j o slf4.
Se configura tambien un fichero solo para las trazas del filtro de seguridad.

```xml
# Configuraci�n del appender General para todas las librer�as que utilicen log4/slf4j.
log4j.appender.file=org.apache.log4j.RollingFileAppender
log4j.appender.file.File=/usr/aplic_ICM/logs/xxx_xxxx_xxx/xxx_xxxx_xxx_log4j.log
log4j.appender.file.MaxFileSize=25MB
log4j.appender.file.MaxBackupIndex=10
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=%d{HH:mm:ss.SSS} [%t] %-5p %c{1} - %m%n

# Configuraci�n del appender de archivo con rotaci�n diaria para el filtro de seguridad.
log4j.appender.file1=org.apache.log4j.RollingFileAppender
log4j.appender.file1.File=/usr/aplic_ICM/logs/xxx_xxxx_xxx/xxx_xxxx_xxx_seguridadFilter.log
log4j.appender.file1.MaxFileSize=25MB
log4j.appender.file1.MaxBackupIndex=10
log4j.appender.file1.layout=org.apache.log4j.PatternLayout
log4j.appender.file1.layout.ConversionPattern=%d{HH:mm:ss.SSS} [%t] %-5p %c{1} - %m%n

# Define el nivel de registro para el root logger
log4j.rootLogger=DEBUG, file

# Configuraci�n del logger para el paquete org.madrid.filtro
log4j.logger.org.madrid.filtro=DEBUG, file1

```
**NOTA:** Se debe sustituir xxx_xxxx_xxx por el nombre del m�dulo t�cnico.
Se pueden configurar tantos Appenders y Loggers adicionales como sea necesario para separar las trazas de diferentes librer�as, esta tarea se realizar� por parte del equipo de mantenimiento de la aplicaci�n seg�n las necesidades de cada una de las aplicaciones.

Por ejemplo, si la aplicaci�n utiliza AutoLogin 3.0 se debe incluir adem�s un Appender adicional para que las trazas de AutoLogin se muestern en un fichero independiente:

```xml
# Configuraci�n del appender de archivo con rotaci�n diaria para el filtro de seguridad.
log4j.appender.file3=org.apache.log4j.RollingFileAppender
log4j.appender.file3.File=/usr/aplic_ICM/logs/ejpl_autologin_fw2_pub/AutoLoginFilter.log
log4j.appender.file3.MaxFileSize=25MB
log4j.appender.file3.MaxBackupIndex=10
log4j.appender.file3.layout=org.apache.log4j.PatternLayout
log4j.appender.file3.layout.ConversionPattern=%d{HH:mm:ss.SSS} [%t] %-5p %c{1} - %m%n
```
Y el logger correspondiente para utilizar este apender solo para AutoLogin.

```xml
# Configuraci�n del logger para el paquete org.madrid.core.auto
log4j.logger.org.madrid.core.autologin=DEBUG, file3
```

**NOTA:** El nivel definido en este fichero aplica a todos los entornos ya que no se define para cada uno de ellos, por lo que es recomendable que antes de pasar a producci�n se cambie los niveles de DEBUG por INFO o WARN para evitar la generaci�n de una cantidad de trazas excesiva en el entorno de producci�n.

## Acciones adicionales dependientes de cada aplicaci�n:

### Aplicaciones que utilizan remotescripting.
Las clases de remotescripting se han eliminado de la librer�a de sistemas ya que es una tecnolog�a totalmente obsoleta y no se va a seguir dando ningun tipo de soporte sobre la misma, en caso de tener acciones de este tipo, deben extraerse las clases de la versi�n actual de la librer�a de sistemas anterior e incluirse como clases del propio proyecto, de manera que si se produce un problema con estas clases se pueda resolver de forma local al proyecto sin necesidad de que se genere una nueva versi�n de la librer�a de sistemas por parte de Arquitectura de Software.

### Aplicaciones que utilizan las clases del ImpresorPDZ de sistemas.
La clase sistemas.framework.acciones.comunes.impresorpdz.AbreActiveXPDZ se ha eliminado de la librer�a de sistemas, ya que es de tipo Acci�n y realiza la carga de datos para una vista en la que se devuelve un objeto con el ActiveX IcmXImpresorPDZ. Si alguna aplicaci�n utiliza esta clase, debe replicarla en la propia aplicci�n.

### Aplicaciones que utilizan las clases de USUI de sistemas.
Las clases de gesti�n de usuarios de USUI sistemas.framework.acciones.comunes.usui.* se han eliminado de la librer�a de sistemas ya que desde hace mucho tiempo no esta permitido realizar ning�n tipo de gesti�n de usuarios en las aplicaciones. Si la aplicaci�n esta haciendo uso de estas clases, debe eliminar la funcionalidad que las utiliza (normalmente se hace uso de estas clases en las jsp�s antiguas que permitian incluir, eliminar y modificar usuarios de una aplicaci�n USUI).

### Aplicaciones que utilizan el Controlados USUSSL.
Este controlador es una soluci�n muy antigua para aplicaciones que accedian por https cuando la mayoria de los dominios de MD no eran seguros. Este controlador utilizaba un servicio que ya no esta activo en entornos previos, por lo que no deber�a haber ninguna aplicaci�n que lo utilice, aun asi, por si alguna aplicaci�n lleva mucho tiempo sin probarse en entornos previos y pudiera estar utilizandolo, este controlador debe actualizarse por el controlador ControladorPrivadoIntranet.

### Aplicaciones que utilizan parseadores de certificados incluidos en la librer�a de sistemas (CamefirmaCommonNameParser / CeresCommonNameParser).
Se han eliminado las clases especificas de parseo de certificados de Camefirma y Ceres ya que el parseo de certificados se centraliza en USigner. Cualquier parseo de certificado debe realizarse utilizando USigner a trav�s de AFC.

### Aplicaciones que utilizan el Cliente de envio de SMS de sistemas.
Las aplicaciones que esten utilizando el cliente de envio de SMS deben sustituir su c�digo para hacer uso de la integraci�n de CORE con SMS.

### Otros errores producidos por el cambio de versi�n:
Si se produce cualquier otro error de compilaci�n al actualizar la versi�n de la librer�a de sistemas y todas las librer�as que dependen de esta se debe comunicar via Mantis.
