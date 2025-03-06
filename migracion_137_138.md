# Intrucciones de migracion de ATLAS 1.3.7 A ATLAS 1.3.8

## Subir la versión del arquetipo padre de 1.3.7 a 1.3.8
Se deben subir la versión en los pom.xml donde aparezca el parent: atlasfrm-arquetipos-padre o atlasfrm-arquetipos-padre-xxxx

```xml
Ejemplo de migración

<parent>
    <artifactId>atlasfrm-arquetipos-padre-web</artifactId>
    <groupId>atlasfrm</groupId>
    <version>1.3.7</version>
    <relativePath></relativePath>
</parent>

cambiar la versión a 1.3.8

<parent>
    <artifactId>atlasfrm-arquetipos-padre-web</artifactId>
    <groupId>atlasfrm</groupId>
    <version>1.3.8</version>
    <relativePath></relativePath>
</parent>
```

## Eliminar las versiones de tipo FIX de las librerias de ATLAS
REvisar los pom.xml del proyecto para eliminar la versión de tipo FIX de 1.3.7, un ejemplo de versión fixeada sería: 

```xml
En este ejemplo eliminamos la versión 1.3.7.4 y lo dejamos sin ella

<dependency>
    <groupId>atlasfrm</groupId>
    <artifactId>atlasfrm-comunes-lib</artifactId>
    <version>1.3.7.4</version>
</dependency>

Eliminamos la versión y debe quedar así:

<dependency>
    <groupId>atlasfrm</groupId>
    <artifactId>atlasfrm-comunes-lib</artifactId>
</dependency>
```
**NOTA:** si la librería ya se utiliza a través de otras librerias del ATLAS, se debería eliminar la dependencia, es decir si se utiliza de forma transitiva, para limpiar el proyecto lo mejor es eliminar esa dependencia.

## Revisar el fichero context.xml del proyecto, si lo tuviera para eliminar las exclusiones
Si tenemos alguna libreria de atlasfrm-xxxx, incluida dentro del atributo **libreriasExcluidas** se debe eliminar.

```xml
En este ejemplo eliminamos el atributo **libreriasExcluidas** porque tenemos librerías de atlas excluidas

<Loader className="atlas.tomcat.AtlasTomcatClassLoader"
        atlasVersion="${atlasfrm-comunes-dependencias-compartidas.version}"
        libreriasExcluidas="atlasfrm-comunes-lib-1.3.7.jar,atlasfrm-seguridad-lib-1.3.7.jar"
        searchVirtualFirst="false" />

Debe quedar así:

<Loader className="atlas.tomcat.AtlasTomcatClassLoader"
        atlasVersion="${atlasfrm-comunes-dependencias-compartidas.version}" 
        searchVirtualFirst="false" />
```

**NOTA:** si después de eliminar todas las libreria de tipoo atlasfrm-xxxxx, quedará alguna otra en el atributo libreriasExcluidas, no se debería eliminar el atributo.

## Revisar y alinear las versiones de CORE.
Si tenemos una librería de CORE con una versión, deberemos de eliminar la **version** y cambiar el **groupid**  de **org.madrid.core** a **org.madrid.core.lib**

```xml
Si tuvieramos una dependencia en nuestro proyecto con el **groupId** del tipo **org.madrid.core** tenemos que cambiar el groupid y eliminar la versión, un ejemplo

<dependency>
    <groupId>org.madrid.core</groupId>
    <artifactId>core-cliente-rest-lib</artifactId>
    <version>2.0.5</version>
</dependency>

debería quedar de la siguiente manera:
<dependency>
    <groupId>org.madrid.core.lib</groupId>
    <artifactId>core-cliente-rest-lib</artifactId>
</dependency>
```