# IBM Cloud Code Engine .Net Buildpack
*Code Engine* da soporte a la compilación desde un *Dockerfile* y *Cloud Native Buildpacks*. Cloud Native Buildpack utiliza *Paketo* para examinar el repositorio de origen y detectar el entorno de tiempo de ejecución en el que se basa el código y cómo se compila una imagen de contenedor desde sus orígenes. En esta guía se muestra el despliegue en *Code Engine* de una aplicación .NET que utiliza *Cloud Native Buildpacks*.
<br />

## Índice  📰
1. [Pre-Requisitos](#pre-requisitos-pencil)
2. [Configurar la aplicación ASP.NET Core con Paketo](#Configurar-la-aplicación-ASP.NET-Core-con-Paketo)
3. [Desplegar la aplicación en Code Engine](#Desplegar-la-aplicación-en-Code-Engine)
4. [Referencias](#Referencias-book)
5. [Autores](#Autores-black_nib)

## Pre Requisitos :pencil:
* Contar con una cuenta en <a href="https://cloud.ibm.com/"> IBM Cloud</a>.
* Tener instalada la CLI de IBM Cloud.
* Tener instalada la CLI de Docker.
* Tener instalado Git.
* Contar con un proyecto y registro de Code Engine.
<br />

## Configurar la aplicación .NET Core con Paketo
Configure su [aplicación .NET Core con Paketo](https://paketo.io/docs/howto/dotnet-core/) y podrá despleglar su aplicación sin necesitada de contar con un Dockerfile. La aplicación .NET Core configurada con Paketo que se utiliza en esta guía se encuentra pública en este [repositorio.](https://github.com/paketo-buildpacks/samples/tree/main/dotnet-core/aspnet)

## Desplegar la aplicación en Code Engine
Para desplegar la aplicación en Code Engine mediante el código fuente es necesario tener el código en un repositorio de github o azure, si este repositorio se encuentra privado no olvide [generar la clave SSH y asociarla al repositorio] (https://github.com/emeloibmco/IBM-Cloud-Code-Engine-.Net#opci%C3%B3n-3-repositorio-privado-en-github).

1. Desde el menú de navegación o menú de hamburguesa seleccione la opción ```Code Engine```.
2. De click sobre el botón de ```Proyectos/Projects``` y seleccione el proyecto en el que desea desplegar la aplicación.
3. De click sobre el botón de ```Aplicaciones/Applications``` y seleccione la opción ```Crear```.
4. En el panel de configuración, llene la información de la siguiente manera:
   * ```Nombre/Name```: Ingrese un nombre para la aplicación.
   * ```Elija el código para ejecutar/Choose the code to run```: Seleccione código fuente o source code
   * ```URL del código fuente/Source code URL```: Ingrese la URL del repositorio, en este caso ingrese
```
https://github.com/paketo-buildpacks/samples/tree/main/dotnet-core/aspnet
```
   * Seleccione la opción ```Especifique los detalles de la compilación/Specify build details```. Esto abrirá una nueva pestaña de configuración 
      * En la pestaña de ```Fuente/Source```elija el code repo access dependiento de si su repostorio es publico o privado, la rama donde sen encuentra su repositorio y de   click en siguiente.
      * En la pestaña de ```Estrategia/Strategy```seleccione Cloud Native Buildpack y deje los valores predeterminados, luego de click en siguiente.
      * En la pestaña de ```Salida/output``` seleccione el acceso de registro con el que ya cuenta e ingrese un nombre para el espacio de trabajo, la imagen y la etiqueta, los cuales se generarán automáticamente al desplegar la aplicación, finalmente de click en el botón ```Hecho/Done```.   
   * ```Puerto de escucha```: Ingrese un puerto, en caso de tener un puerto de escucha especifico para su aplicación.
   * De click en el boton de ```Crear```. Esto lo llevara a una nueva pestaña en donde deberá esperar algunos minutos hasta que la aplicación se despliegue.

<p align="center">
<img width="800" alt="img8" src=https://github.com/emeloibmco/IBM-Cloud-Code-Engine-.Net/blob/8edbcc0d5082c170fed5816112df9e7572738ecb/Imagenes/sourcecode.gif>
</p>




## Referencias :book:
* [Acerca de IBM Cloud Code Engine](https://cloud.ibm.com/docs/codeengine).

## Autores :black_nib:
Equipo IBM Cloud Tech Sales Colombia.
<br />
