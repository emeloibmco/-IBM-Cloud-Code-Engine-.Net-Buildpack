# IBM Cloud Code Engine .Net Buildpack :package: :cloud:
*Code Engine* da soporte a la compilación desde un *Dockerfile* y *Cloud Native Buildpacks*. Cloud Native Buildpack utiliza *Paketo* para examinar el repositorio de origen y detectar el entorno de tiempo de ejecución en el que se basa el código y cómo se compila una imagen de contenedor desde sus orígenes. En esta guía se muestra el despliegue en *Code Engine* de una aplicación .NET que utiliza *Cloud Native Buildpacks*.
<br />

## Índice  📰
1. [Pre-Requisitos](#pre-requisitos-pencil)
2. [Configurar la aplicación ASP.NET Core con Paketo](#Configurar-la-aplicación-ASP.NET-Core-con-Paketo-wrench)
3. [Desplegar la aplicación en Code Engine](#Desplegar-la-aplicación-en-Code-Engine-arrow_double_down)
4. [Acceder a la aplicación](#Acceder-a-la-aplicación-computer)
5. [Referencias](#Referencias-book)
6. [Autores](#Autores-black_nib)

## Pre Requisitos :pencil:
* Contar con una cuenta en <a href="https://cloud.ibm.com/"> IBM Cloud</a>.
* Tener instalada la CLI de Docker.
* Tener instalado Git.
* Tener instalada la CLI de <a href="https://buildpacks.io/docs/tools/pack/">Pack</a>.
* Contar con un proyecto de Code Engine.
<br />

## Configurar la aplicación ASP.NET Core con Paketo :wrench:
Configure su [aplicación .NET Core con Paketo](https://paketo.io/docs/#build-the-app-image-from-source-code) y podrá despleglar su aplicación sin necesitada de contar con un Dockerfile. Para crear la aplicación .NET Core configurada con Paketo que se utiliza en esta guía siga estos pasos:

Nota: En caso de que no tenga instalado el comando dotnet puede clonar este repositorio en su computador (git clone https://github.com/emeloibmco/-IBM-Cloud-Code-Engine-.Net-Buildpack).

1. Cree la aplicación con el comnado dotnet:

```
dotnet new webApp -o myWebApp --no-https
```
2. Ingrese a la aplicación:

 ```
 cd myWebApp
 ```

3. Publique la aplicación para obtener una DLL autónoma:

```
dotnet publish -c Release
```

4. Usando el generador de paquete ```base``` se contruye una imagen de la aplicación como un contenedor ejecutable:

```
pack build <usuario_docker>/paketo-mywebapp --builder paketobuildpacks/builder:base
```
Espere a recibir el siguiente mensaje: Successfully built image <usuario_docker>/paketo-mywebapp.

<p align="center">
<img width="800" alt="img8" src=https://github.com/emeloibmco/-IBM-Cloud-Code-Engine-.Net-Buildpack/blob/main/Imagenes/paketo.PNG>
</p>

Y podrá visualizar la imagen en su dominio de Docker.

<p align="center">
<img width="800" alt="img8" src=https://github.com/emeloibmco/-IBM-Cloud-Code-Engine-.Net-Buildpack/blob/main/Imagenes/docker.PNG>
</p>

5. Ejecute la imagen de la aplicación con Docker:
```
docker run -d -p 8080:8080 -e PORT=8080 <usuario_docker>/paketo-mywebapp
```
6. Al ingresar a http://localhost:8080 debe evidenciar lo siguiente y la imagen estará funcionando correctamente. 

<p align="center">
<img width="800" alt="img8" src=https://github.com/emeloibmco/-IBM-Cloud-Code-Engine-.Net-Buildpack/blob/main/Imagenes/webapp.PNG>
</p>

7. Envie su aplicación al repositorio remoto (Recuerde tener la sesión activa con ```docker login```):

```
docker push <usuario_docker>/paketo-mywebapp
```
Una vez termine, su imagen estará desplegada en su repositorio remoto de docker.

## Desplegar la aplicación en Code Engine :arrow_double_down:
Para desplegar la aplicación en Code Engine mediante el código fuente es necesario tener el código en un repositorio de github o azure, si este repositorio se encuentra privado no olvide [generar la clave SSH y asociarla al repositorio](https://github.com/emeloibmco/IBM-Cloud-Code-Engine-.Net#opci%C3%B3n-3-repositorio-privado-en-github).

1. Desde el menú de navegación o menú de hamburguesa seleccione la opción ```Code Engine```.
2. De click sobre el botón de ```Proyectos/Projects``` y seleccione el proyecto en el que desea desplegar la aplicación.
3. De click sobre el botón de ```Aplicaciones/Applications``` y seleccione la opción ```Crear```.
4. En el panel de configuración, llene la información de la siguiente manera:
   * ```Nombre/Name```: Ingrese un nombre para la aplicación.
   * ```Elija el código para ejecutar/Choose the code to run```: Seleccione container image o imagen de contenedor
   * ```Referencia de la imagen/Image reference```: Ingrese la dirrección de su imagen en el repositorio docker.
```
<usuario_docker>/paketo-mywebapp:latest
```
   * Seleccione la opción ``Configurar imagen/Configure image```. Esto abrirá una nueva pestaña de configuración. Verifique que todos los campos sean correctos y de click en ```Hecho/Done```  
   * ```Puerto de escucha```: Ingrese un puerto, en caso de tener un puerto de escucha especifico para su aplicación.
   * De click en el boton de ```Crear```. Esto lo llevara a una nueva pestaña en donde deberá esperar algunos minutos hasta que la aplicación se despliegue.

<p align="center">
<img width="800" alt="img8" src=https://github.com/emeloibmco/-IBM-Cloud-Code-Engine-.Net-Buildpack/blob/main/Imagenes/buildpack.gif>
</p>

# Acceder a la aplicación :computer:
Una vez, desplegada la aplicación, debe estar en estado ```Ready/Activo```, de click en el nombre de la aplicación y encontrará una vista de las instancias desplegadas actualmente, las configuraciones de la aplicación (Puerto de escucha, variables de entorno, recursos de la instancia, etc) y en la pestaña de ```End Points/Puntos finales``` encontrará las URL de acceso a la aplicación. 

<p align="center">
<img width="800" alt="img8" src=https://github.com/emeloibmco/-IBM-Cloud-Code-Engine-.Net-Buildpack/blob/main/Imagenes/access.gif>
</p>




## Referencias :book:
* [Acerca de IBM Cloud Code Engine](https://cloud.ibm.com/docs/codeengine).

## Autores :black_nib:
Equipo IBM Cloud Tech Sales Colombia.
<br />
