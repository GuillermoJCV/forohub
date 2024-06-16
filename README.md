# FOROHUB - ALURA Oracle Next Education

Este es el último **challenge** de Alura para Backend donde se aprende a crear una API desde cero generando distintos end points para el CRUD de el foro de forohub de Alura.

El principal reto para este challenge no es en sí el challenge si no más bien hacerlo en IDX (13/06/2024); ya que, al ser un editor de código en la nube y no tener un template para Java, hay que configurar ciertas cosas y no se puede usar una base de datos en local con los métodos traidionales. Por lo que para cualquiera que necesite crear un proyecto de java y los IDE recomendados se les hace muy pesado. Aquí dejaré una serie de instrucciones para programar java en IDX

### Configuracion del proyecto

1. Primero es ir a a [Spring Initializer](https://start.spring.io/) y crear un nuevo proyecto con sus dependencias. Como normalmente se haría.
2. Después se descarga el proyecto haciendo **click** en Generate
3. Luego de esto debemos subir los cambios a github.
    - Creamos un repositorio
    - Seguimos las instrucciones de Github
    - Subimos nuestros archivos al repositorio creado
4. Una vez ya tenemos nuestros archivos entramos a [Project IDX](https://idx.google.com/) y hacemos lo siguiente:
    - Iniciamos sesión si aún no has iniciado.
    - Damos click a **Get Started**
    - Damos click a **Import repo** y seguimos las instrucciones para iniciar sesión con github si aún no lo ha hecho
    - Después de esto nos va a pedir la URL al repositorio, y lo único que tenemos que hacer es importarlo
5. IDX nos ofrece unos paquetes por defecto para instalar; que, por recomendación, deberian descargarlos
    - Si no quieres descargar estos paquetes puedes buscar el paquete **Extension Pack for Java Auto Config** escribiendo jdk en el buscador de extensiones de project IDX
    - Una vez descargamos todas las extensiones asociadas con programacion para java entramos al archivo dev.nix
6. En el archivo dev.nix tenemos que configurar tanto el jdk como las extensiones agregadas
    - Arriba de packages nos va a aparecer la instruccion Add packages y debemos buscar el jdk que necesitamos, por ejemplo, yo necesito la version 17, por lo que voy a usar la 17 de la siguiente manera
    ```nix
        packages = [
            pkgs.jdk17
        ];
    ```

    _ Ya con esto configuramos el jdk en el workspace y lo que tendriamos que hacer es añadir las extensiones en el apartado extensions 
    ```nix
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

Solamente con esto ya podemos empezar a programar Java con Spring en este editor de código. Sin absolutamente nada más. Pero nuestro proyecto requiere de algo muy importante.

## Base de datos

Tenemos otro problema, la base de datos no se puede conectar de la manera tradicional; por el contrario, se deben utilizar otros métodos y a continuación presento los siguientes:

1. Crear la base de datos en local y conectarla con un servicio de tunneling
    - **Explicación:** Como no podemos usar el localhost desde idx ya que se ejecuta desde internet. Tenemos que utilizar nuestra IP pública y puerto para poder conectarnos a la base de datos en IDX, de esta manera podemos conectar nuestro localhost a nuestro proyecto. 
    - **Problema:** **Si esta IP se llegara a filtrar** ya sea mediante github o por cualquier descuido en general, podemos sufrir un ataque de manera remota.
    - **Solución:** Podemos conectar esta base de datos a un servicio externo de tunneling que nos cifra nuestros datos para mantenerlos seguros.
    - Algunas plataformas que ofrecen estos servicios son: [LocalXpose](https://localxpose.io/) o [Ngrok](https://ngrok.com/); sin embargo, estos dos servicios piden targeta para poder utilizar el servicio. Por lo que aquí la siguiente solución:
    - **Solución 2:** La siguiente solución requiere tener bastante cuidado, ya que vamos a exponer nuestra IP Pública, por lo que hay dos opciones: *Crear variables de entorno en el idx/dev.nix y eliminarlo agregarlo al .gitignore (recomendado)* o por el contrario *Poner la información de la conexión directo en el application.properties y agregarlo al gitignore*.

Para configurar las variables de entorno

2. Crear una base de datos en la nube:
    - **Explicación:** Podemos crear una base de datos en la nube utilizando los multiples servicios que la nube nos ofrece; por ejemplo: [Amazon RDS](https://aws.amazon.com/rds/), [Google CLoud](https://cloud.google.com/), [Oracle Cloud](https://www.oracle.com/cloud/), y existen muchos otros.
    - **Problema:** Todos estos servicios son **caros** y los que son gratuitos ofrecen una capa muy reducida. No encontré servicios de mysql que dieran una base de datos gratuita. Normalmente las bases de datos gratuitas por tiempo indefinido, ofrecen una cantidad de **GB limitados** para no exederse.
    - **Solución:** No necesariamente necesitan usar MySQL, como bien sabemos, el curso pide utilizar JPA que es un ORM que se caracteriza porque, no importa el lenguaje que utilicemos, solo tendremos que **configurar el application.properties** y con esto ya podremos usar el lenguaje que necesitemos. Por lo que a continuación voy a escribir alternativas gratuitas que ofrecen bases de datos y se pueden conectar con nuestro proyecto.

* [Vercel](https://vercel.com/) : Nos ofrece 1GB de espacio para nuestra base de datos **PostgreSQL** y aunque es para usar en aplicaciones de vercel, se pueden usar en el exterior.
* [Supabase](https://supabase.com/) : Nos ofrece 500MB de almacenamiento para nuestra base de datos **PostgreSQL**
* ~~[Turso](https://turso.tech/)~~ : Nos ofrece 9GB de espacio para nuestras bases de datos **SQLite**. Se pueden crear 500 Bases de datos pero estos 9GB son compartidos, igualmente está muy bien para ser una capa gratuita. Lo intenté y creo que no se puede.
* ~~[AstroDB](https://astro.build/db/)~~ : Nos ofrece 1GB de almacenamiento para base de datos **LibSQL** / **SQLite**. Se necesita una invitación puesto que está en su version beta.

Voy a utilizar [XAMPP](https://www.apachefriends.org/download.html) para tener una base de datos en local, por lo que debemos ir a la URL adjunta y descargarlo. Esta es una plataforma que sirve para iniciar servicios de apache y mysql.
Entre las plataformas que pueden usar:
* [MAMP](https://www.mamp.info/en/downloads/) - No lo he probado aún
* [WAMP](https://www.wampserver.com/) - Solo está en inglés y francés
* [XAMPP](https://www.apachefriends.org/download.html) - Solo está en inglés y alemán y es más ligero que WAMP


### Configuración de la base de datos

Así que lo primero que voy a hacer es configurar el entorno de desarrollo con las dependencias necesarias en build.gradle.

Lo que pueden hacer es agregar las dependencias al build.gradle y luego ejecutar el instalador de gradle para que se instalen automáticamente. Para ello nos vamos a [Maven repository](https://mvnrepository.com/) y buscamos las dependencias necesarias. Aún siendo de maven, tiene soporte para dependencias de gradle igualmente, por lo que no es necesario ir a otra página.

> [!CAUTION]
> Si ya agregaron las dependencias que se encuentran abajo, no las tienen que volver a agregar.
> Y si están usando otra base de datos, recuerden usar el driver adecuado.

Y agregamos lo siguiente en nuestras dependencias de build.gradle (Si alguien ve esto, y aún no he agregado el pom.xml porque soy muy distraído, por favor avisarme para agregarlo a mi correo memo92975@gmail.com):

```build.gradle
dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
	implementation 'org.springframework.boot:spring-boot-starter-security'
	implementation 'org.springframework.boot:spring-boot-starter-validation'
	implementation 'org.springframework.boot:spring-boot-starter-web'
	implementation 'org.flywaydb:flyway-core'
	compileOnly 'org.projectlombok:lombok'
	developmentOnly 'org.springframework.boot:spring-boot-devtools'
	annotationProcessor 'org.projectlombok:lombok'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
	testImplementation 'org.springframework.security:spring-security-test'
	testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
	runtimeOnly 'com.mysql:mysql-connector-j'
}
```
La última dependencia se trata del driver para MySQL; sin embargo, tenemos que agregar el driver que se necesite para la base de datos que utilicemos.

Y antes de configurar el application.properties necesito configurar la contraseña y nombre de mi base de datos.


### Tecnologías principales

* Java - Spring
* MySQL
* XAMPP

### Tecnologías secundarias

* Graddle
* IDX de Google

### Dependencias

* Lombok
* Spring Web
* Spring Boot DevTools
* Spring Data JPA
* Flyway Migration
* MySQL Driver
* Validation
* Spring Security
