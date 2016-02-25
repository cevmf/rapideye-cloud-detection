# rapideye-cloud-detection
El propósito de este repositorio es eliminar las nubes detectadas en el procesamiento de imágenes rapideye. Para lograrlo, usamos un acercamiento propio que consiste en detectar anomalías midiendo el comportamiento esperado de los valores de una banda en particular y los que ya se tienen.

## Disclosure
Este procedimiento es meramente experimental, es una propuesta, y no es bajo ninguna circunstancia un producto final. No se puede considerar como  *el algoritmo de enmascaramiento de nubes de MADMex*. 

## Como crear el enmascaramiento de nubes

Primero es necesario crear una imagen en docker:

```
docker build -t rapideye-clouds .
```

Una vez que tengamos la imagen creada, iniciamos el contenedor de docker usando tanto el directorio actual como el directorio que contiene la imagen rapideye:

```
docker run -it \
       -v <path to rapideye directory>:<path to rapideye directory inside docker> \
       -v $(pwd):/data \
       rapideye-clouds \
       python main.py <path to rapideye directory inside docker>
```
## Windows
En Windows, Docker solo permite montar archivos en ciertos directorios uno de ellos es el que se señala aquí:

```
C:\\Users
```
Nuestra carpeta de trabajo deberá estar en el directorio descrito previamente. Por ejemplo, en nuestro caso usaremos una carpeta llamada "example":

```
C:\\Users\example
```

Es importante recordar que para windows los directorios deben iniciar con "/":

```
docker run -it \
       -v /<path to rapideye directory>:<path to rapideye directory inside docker> \
       -v /$(pwd):/data \
       rapideye-clouds \
       python main.py <path to rapideye directory inside docker>
```
Por ejemplo, si nuestro directorio de trabajo es "C:\\Users\example\l3a":

```
docker run -it \
       -v /c/Users/example/l3a/:/rapideye/ \
       -v /$(pwd):/data \
       rapideye-clouds \
       python main.py /rapideye/
```

## NOTA

Puede ser el caso que la RAM no sea suficiente para este proceso, si es así, es necesario aumentar el tamaño de la memoria en la configuración de VirtualBox  se sugiere 8192Mb.
