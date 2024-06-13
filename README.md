# FOROHUB - ALURA Oracle Next Education

Este es el último **challenge** de Alura para Backend donde se aprende a crear una API desde cero generando distintos end points para el CRUD de el foro de forohub de Alura.

El principal reto para este challenge no es en sí el challenge si no más bien hacerlo en IDX; ya que, al ser un editor de código en la nube y no tener un template para Java, hay que configurar ciertas cosas. Por lo que para cualquiera que necesite crear un proyecto de java y los IDE recomendados se les hace muy pesado. Aquí dejaré una serie de instrucciones para programar java en IDX

1. Primero es ir a a [Spring Initializer](https://start.spring.io/) y crear un nuevo proyecto con sus dependencias. Como normalmente se haría.
2. Después se descarga el proyecto haciendo **click** en Generate
3. Luego de esto debemos subir los cambios a github.
    _ Creamos un repositorio
    _ Seguimos las instrucciones de Github
    _ Subimos nuestros archivos al repositorio creado
4. Una vez ya tenemos nuestros archivos entramos a [Project IDX](https://idx.google.com/) y hacemos lo siguiente:
    _ Iniciamos sesión si aún no has iniciado.
    _ Damos click a **Get Started**
    _ Damos click a **Import repo** y seguimos las instrucciones para iniciar sesión con github si aún no lo ha hecho
    _ Después de esto nos va a pedir la URL al repositorio, y lo único que tenemos que hacer es importarlo
5. IDX nos ofrece unos paquetes por defecto para instalar; que, por recomendación, deberian descargarlos
    _ Si no quieres descargar estos paquetes puedes buscar el paquete **Extension Pack for Java Auto Config** escribiendo jdk en el buscador de extensiones de project IDX
    _ Una vez descargamos todas las extensiones asociadas con programacion para java entramos al archivo dev.nix
6. En el archivo dev.nix tenemos que configurar tanto el jdk como las extensiones agregadas
    _ Arriba de packages nos va a aparecer la instruccion Add packages y debemos buscar el jdk que necesitamos, por ejemplo, yo necesito la version 17, por lo que voy a usar la 17 de la siguiente manera. ```nix
  packages = [
    pkgs.jdk17
  ];

```
    _ Ya con esto configuramos el jdk en el workspace y lo que tendriamos que hacer es añadir las extensiones en el apartado extensions ```nix
        extensions = [
            "redhat.java"
            "vscjava.vscode-java-debug"
            "vscjava.vscode-java-dependency"
            "vscjava.vscode-java-pack"
            "vscjava.vscode-java-test"
            "vscjava.vscode-maven"
        ];
    ```
7. Una vez terminamos de configurar nuestro dev.nix, solamente debemos dar click en **Rebuild environment**

Solamente con esto ya podemos empezar a programar Java con Spring en este editor de código.

### Tecnologías principales

* Java - Spring
* MySQL

### Tecnologías secundarias

* Graddle
* IDX de Google