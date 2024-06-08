# <span style="color: red;">Django REST Framework</span>
Django REST Framework es una herramienta robusta que facilita la creación de APIs web seguras y eficientes en aplicaciones Django, permitiendo a los desarrolladores enfocarse en la lógica de negocio en lugar de en los detalles de implementación de la API.

## <span style="color: orange;">¿Qué es un framework?</span>

> Un framework (o marco de trabajo) es una plataforma de software diseñada para facilitar el desarrollo de aplicaciones y proporcionar una estructura estándar que los desarrolladores pueden seguir. Incluye un conjunto de herramientas, bibliotecas y reglas que ayudan a desarrollar software de manera más eficiente y estructurada. Los frameworks permiten reutilizar código y seguir buenas prácticas de programación, lo que puede mejorar la calidad del software y reducir el tiempo de desarrollo.

## <span style="color: orange;">Puntos clave sobre Django REST Framework</span>
1. **Serialización:** DRF facilita la conversión de datos complejos, como consultas de base de datos, a formatos de datos nativos de Python y viceversa, utilizando serializers. Esto es esencial para transformar los datos en un formato adecuado para la API (como JSON).
2. **Vistas y Viewsets:** Proporciona clases basadas en vistas y viewsets que simplifican la creación de endpoints de la API. Las vistas genéricas ayudan a realizar operaciones CRUD (Crear, Leer, Actualizar, Eliminar) de manera eficiente.
3. **Autenticación y Permisos:** Incluye soporte para múltiples esquemas de autenticación (token, sesión, OAuth) y permisos (permisos basados en roles, permisos a nivel de objeto) para controlar el acceso a la API.
4. **Paginación:** Facilita la paginación de respuestas largas, lo que es útil para manejar grandes conjuntos de datos y mejorar la eficiencia de las solicitudes.
5. **Documentación Automática:** Integra herramientas como Swagger y CoreAPI para generar automáticamente documentación interactiva para la API.
6. **Filtros y Búsqueda:** Proporciona capacidades para filtrar y buscar a través de los datos expuestos por la API, lo que permite a los usuarios recuperar datos específicos de manera eficiente.
7. **Soporte para Navegador:** Incluye una interfaz de navegación de API amigable para el desarrollador, que permite explorar y probar la API directamente desde el navegador.
8. **Integración con Django:** Se integra perfectamente con Django, aprovechando su ORM (Object-Relational Mapping), autenticación, y otros componentes.

## <span style="color: orange;">Índice</span>
- [Django REST Framework](#django-rest-framework)
  - [¿Qué es un framework?](#qué-es-un-framework)
  - [Puntos clave sobre Django REST Framework](#puntos-clave-sobre-django-rest-framework)
  - [Índice](#índice)
  - [Instalación](#instalación)
  - [Configurar de Base de Datos](#configurar-de-base-de-datos)
  - [Crear la Estructura de la Base de Datos](#crear-la-estructura-de-la-base-de-datos)
    - [Migraciones](#migraciones)
  - [Crear Serializadores](#crear-serializadores)
  - [Crear las vistas](#crear-las-vistas)
  - [Crear las rutas](#crear-las-rutas)
  - [Probar Aplicación](#probar-aplicación)
  - [Crear géneros literarios](#crear-géneros-literarios)
  - [CRUDs para el Resto de Modelos](#cruds-para-el-resto-de-modelos)
  - [Añadir Nuevos Campos a los Modelos](#añadir-nuevos-campos-a-los-modelos)
  - [Protección con JWT (JSON Web Token)](#protección-con-jwt-json-web-token)
    - [Características principales de JWT](#características-principales-de-jwt)
    - [Estructura de JWT](#estructura-de-jwt)
    - [Usos Comunes de JWT](#usos-comunes-de-jwt)
      - [Entendiendo los tokens de access y refresh](#entendiendo-los-tokens-de-access-y-refresh)
  - [Pasos para usar los tokens en Postman](#pasos-para-usar-los-tokens-en-postman)

## <span style="color: orange;">Instalación</span>
1. Abrir una terminal en Visual Studio Code: `CTRL + Ñ`.
2. Instalación de un entorno virtual. Un entorno virtual es un directorio que contiene una instalación independiente de Python y una colección de paquetes y dependencias que pueden ser utilizados por un proyecto específico. Esto permite a los desarrolladores aislar los entornos de desarrollo para diferentes proyectos, evitando conflictos de dependencias y asegurando que cada proyecto tenga acceso a las versiones específicas de las librerías que necesita:
```bash
pip install virtualenv
```

3. Crear entorno Virtual en Python. En la carpeta llamada venv📦:
```bash
python -m venv venv
```
![alt text](img/image-1.png)

4. Oprimir `F1` y escribir:
```bash
Python: Select Interpreter
```
-  Seleccionamos la opción, Python 3.12.3 ('venv':venv)...
![alt text](img/image.png)

5. Matar cualquier terminar abierta en el Visual Studio Code y abrirla nuevamente usando `CTRL + Ñ`
![alt text](img/image-2.png)
Ahora debería indicarnos que nos encontramos dentro del entorno virtual.

6. Ahora es el momento de instalar Django desde el entorno virtual:
```bash
pip install django
```
![alt text](img/image-3.png)

7. Instalar el modulo Django REST Framework
```bash
pip install djangorestframework
```
![alt text](img/image-8.png)

8. Crear un nuevo proyecto:
```bash
django-admin startproject book_store_api .
```
![alt text](img/image-4.png)

9. Ejecutar proyecto:
```bash
python manage.py runserver
```
- Apretar `CTRL + CLIC` sobre el endpoint que arroja:
![alt text](img/image-5.png)

- La acción anterior debería abrir
![alt text](img/image-6.png)

10. Lo siguiente ahora es enlazar una aplicación:
- Primero paramos la ejecución del proyecto con `CTRL + C`
- Iniciar una nueva aplicación con:
```bash
python manage.py startapp book_store
```
![alt text](img/image-10.png)
- Añadir Django REST Framework y nuestra app al archivo de configuraciones de nuestro proyecto:
![alt text](img/image-9.png)

## <span style="color: orange;">Configurar de Base de Datos</span>
1. Instalar librería para conectar con el motor:
```bash
pip install psycopg2
```
2. Modificar la configuración de base de datos en el archivo `book_store_api/settings.py`:
![alt text](img/image-11.png)

3. Ir al pgAdmin y crear una base nueva base de datos.

![alt text](img/image-12.png)
![alt text](img/image-13.png)
![alt text](img/image-14.png)

## <span style="color: orange;">Crear la Estructura de la Base de Datos</span>
![alt text](img/image-20.png)
> [!NOTE]
> En Django, un modelo es una clase de Python que representa una tabla en la base de datos. Cada atributo de la clase representa una columna en la tabla. Los modelos son una parte fundamental del framework Django, ya que proporcionan una forma de definir y manipular datos de manera estructurada y orientada a objetos.
- Ir a `book_store/models.py` y crear todos los modelos necesarios que representaran las tablas en nuestra base de datos.
![alt text](img/image-19.png)

### <span style="color: orange;">Migraciones</span>
> [!NOTE]
> Las migraciones en Django son una característica clave que permite gestionar y aplicar cambios en la estructura de la base de datos de una manera controlada y reproducible. Se utilizan para sincronizar el esquema de la base de datos con los modelos definidos en el código de Django.
- Es importante realizar las migraciones necesarias para crear las tablas en la base de datos:
```bash
python manage.py makemigrations
```
![alt text](img/image-16.png)
![alt text](img/image-17.png)

- Y ahora ejecutamos las migraciones para que se creen las tablas en nuestra base de datos.
```bash
python manage.py migrate
```
- Esto genera toda la estructura de tablas que necesitamos las 4 que definimos y otras por defecto que Django genera automáticamente.

![alt text](img/image-18.png)

## <span style="color: orange;">Crear Serializadores</span>
Los serializadores son una herramienta fundamental que permite convertir instancias de modelos Django en representaciones JSON (u otros formatos) y viceversa.
- Crear un archivo llamado `serializer.py`

![alt text](img/image-21.png)

- Escribimos los serializadores necesarios en `serializers.py`
![alt text](img/image-22.png)

## <span style="color: orange;">Crear las vistas</span>
Las `views` (vistas) son componentes que manejan las solicitudes HTTP y devuelven las respuestas HTTP adecuadas. Son fundamentales para definir cómo se procesan las solicitudes y cómo se interactúa con los datos en una API
- Ir al archivo `views.py`

![alt text](img/image-23.png)

- Crear todas las vistas necesarias
![alt text](img/image-24.png)

## <span style="color: orange;">Crear las rutas</span>
En Django, las URLs (Uniform Resource Locators) son las direcciones que los usuarios utilizan para acceder a diferentes partes de una aplicación web. En Django REST Framework (DRF), las URLs también juegan un papel crucial para definir los puntos de acceso a las API.
- Crear el archivo el archivo `urls.py` para que se expongan los servicios de la API que vamos a consumir

![alt text](img/image-25.png)

- Definir todas la rutas en este archivo.
![alt text](img/image-28.png)

- Registrar nuestras urls en la aplicación principal
![alt text](img/image-29.png)

## <span style="color: orange;">Probar Aplicación</span>
1. Abrir Postman
2. Crear una nueva colección

![alt text](img/image-30.png)

3. Nombrar la colección

![alt text](img/image-31.png)

4. Crear un nuevo request

![alt text](img/image-32.png)

4.1. Renombrar el request a `list`

![alt text](img/image-33.png)

5. Crear un en Environment

![alt text](img/image-34.png)

- Escribir todos los valores correspondientes

![alt text](img/image-35.png)

- Seleccionar nuestro environment para poder utilizarlo en nuestros request

![alt text](img/image-36.png)

6. Escribir nuestra url

![alt text](img/image-37.png)

7. Crear un nuevo folder

![alt text](img/image-38.png)

- Llamar el folder `Genre`

![alt text](img/image-39.png)

- Arrastrar el request `list` al folder `Genre`

![alt text](img/image-40.png)

8. Dentro de `Genre` crear todos los request necesarios para hacer un CRUD son 5 request en total

![alt text](img/image-41.png)

> [!NOTE]
> Para elegir un verbo HTTP según corresponda lo podemos hacerlo desde el request
>
> ![alt text](img/image-42.png)

> [!TIP]
> Para el resto de operaciones CRUD los request deben verse de esta manera:
> 
> `show` (Mostrar):
>
> ![alt text](img/image-43.png)
>
> `create` (Crear):
>
> ![alt text](img/image-44.png)
>
> `update` (Actualizar):
>
> ![alt text](img/image-45.png)
>
> `delete` (Eliminar):
>
> ![alt text](img/image-46.png)

## <span style="color: orange;">Crear géneros literarios</span>

Desde el request `create` (Crear), crear la siguiente lista de géneros literarios:

- Ciencia
- Novela negra
- Novela histórica
- Romántica
- Ciencia ficción
- Distopía
- Aventuras
- Fantasía
- Contemporáneo
- Terror
- Paranormal
- Poesía
- Juvenil
- Infantil

> [!IMPORTANT]
> Al crear un nuevo genero debemos visualizar una respuesta como esta:
>
> ![alt text](img/image-47.png)

> [!NOTE]
> Una vez creados todos lo géneros literarios al consumir el servicio `list` (Listar) se debería visualizar la siguiente respuesta en formato JSON:
>
> ![alt text](img/image-48.png)
>
> Podemos visualizar también esta información desde nuestra base de datos
>
> ![alt text](img/image-49.png)

## <span style="color: orange;">CRUDs para el Resto de Modelos</span>

- Crear el CRUD completo para el resto de modelos e insertar autores(Author), libros(Book) y sus respectivas relaciones entre autores y libros(BookAuthor).

![alt text](img/image-50.png)

## <span style="color: orange;">Añadir Nuevos Campos a los Modelos</span>

Agregar nuevas columnas a una base de datos usando Django REST Framework (DRF) es generalmente más sencillo y eficiente en comparación con otros frameworks de desarrollo backend.

Django proporciona una poderosa herramienta de migraciones automáticas que facilita la creación, modificación y eliminación de columnas en la base de datos sin necesidad de escribir SQL manualmente. Con comandos simples como makemigrations y migrate, las migraciones son generadas y aplicadas de manera eficiente.

Para agregar un nuevo campo al modelo `Book` para la URL de una imagen y permitir la carga de imágenes en Django REST framework, vamos a seguir estos pasos:

1. Pillow, es una biblioteca de Python para la manipulación de imágenes. Necesitamos instalar esta biblioteca para poder manejar archivos de imagen en la aplicación Django.

- Abrir terminal `CTRL + Ñ`.

- Ejecutar el siguiente comando:
```bash
pip install Pillow
```

- Verificar que Pillow esté instalado ejecutando el siguiente comando:
```bash
pip show Pillow
```

2. Modificar el modelo `Book` para agregar el campo de URL de la imagen:
Abrir el archivo `book_store/models.py` y agregar un nuevo campo llamado image_url:

![alt text](img/image-51.png)

3. Crear y aplicar la migración para el nuevo campo:
Ejecutar los siguientes comandos en la terminal (Abrirla con `CTRL + Ñ`):

Primero:
```bash
python manage.py makemigrations
```

Segundo:
```bash
python manage.py migrate
```

4. Configurar los settings de Django para manejar archivos estáticos y multimedia:
Asegurarse de tener configuradas las rutas para archivos multimedia en el archivo `book_store_api/settings.py`.

![alt text](img/image-52.png)

5. Actualizar el serializer para manejar la imagen:
Abrir el archivo `book_store/serializer.py`.

- Importar las configuraciones

![alt text](img/image-53.png)

- Actualizar el serializer para el modelo `Book`.

![alt text](img/image-54.png)

6. Configurar las URL para servir archivos multimedia:
Abre el archivo `book_store_api/urls.py` y configura las rutas para servir archivos multimedia durante el desarrollo.

![alt text](img/image-55.png)

7. Crear un nuevo libro desde Postman:

- Agregar al request el campo image y fijarlo como un campo de tipo archivo

![alt text](img/image-56.png)

- Seleccionar el archivo de tipo imagen desde el computador

![alt text](img/image-57.png)

- Enviar la petición para crear un nuevo libro

![alt text](img/image-58.png)

- Si vamos al navegador y pegamos la url completa de la imagen base_url + image_url (http://127.0.0.1:8000/media/images/7_mundo_demonios.jpg), obtendremos la imagen que acabamos de subir

![alt text](img/image-59.png)

- Podemos visualizar esta imagen en la carpeta `media/images` del proyecto:

![alt text](img/image-60.png)

> [!IMPORTANT]
> Hacer que los autores también puedan recibir y guardar imágenes.

## <span style="color: orange;">Protección con JWT (JSON Web Token)</span>

JWT, o JSON Web Token, es un estándar abierto (RFC 7519) que define una forma compacta y autónoma de transmitir información de forma segura entre dos partes como un objeto JSON. Esta información puede ser verificada y confiable porque está firmada digitalmente.

### Características principales de JWT
1. Compacto:
- JWT está diseñado para ser compacto, lo que lo hace adecuado para ser transmitido en la URL, en el cuerpo de una solicitud POST, o dentro de una cabecera HTTP.

2. Autónomo:
- Un token JWT contiene toda la información necesaria sobre el usuario y sus permisos, lo que lo hace autónomo y evita la necesidad de una sesión del servidor para la autenticación.

3. Seguro:
- JWT puede ser firmado usando un secreto (con el algoritmo HMAC) o un par de claves pública/privada usando RSA o ECDSA. Esto asegura que el contenido del token no ha sido alterado después de ser emitido.

### Estructura de JWT
Un JWT se compone de tres partes separadas por puntos ('.'):

1. Header (Encabezado):
- Generalmente consta de dos partes: el tipo de token, que es JWT, y el algoritmo de firma que se está utilizando, como HMAC SHA256 o RSA.

```json
{
    "alg": "HS256",
    "typ": "JWT"
}
```

Después, esta estructura se codifica en Base64Url.

2. Payload (Cuerpo):
- El cuerpo del token, llamado carga útil, contiene las afirmaciones (claims). Las afirmaciones son declaraciones sobre una entidad (generalmente, el usuario) y datos adicionales. Hay tres tipos de afirmaciones: registradas, públicas y privadas.

Ejemplo de payload:
```json
{
    "sub": "1234567890",
    "name": "John Doe",
    "admin": true
}
```
Este JSON también se codifica en Base64Url.

3. Signature (Firma):
- Para crear la firma se toma el encabezado codificado, el payload codificado, un secreto, y el algoritmo especificado en el encabezado, y se firma. Por ejemplo, usando el algoritmo HMAC SHA256, la firma sería:

```scss
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```

La firma se usa para verificar que el emisor del JWT es quien dice ser y para asegurar que el mensaje no ha sido alterado.

Ejemplo de JWT
Un JWT completo se ve algo así:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

### Usos Comunes de JWT
- Autenticación:
  - Después de que el usuario se loguea, cada solicitud posterior incluirá el JWT, permitiendo al usuario acceder a rutas, servicios y recursos permitidos con ese token.
- Intercambio de Información:
  - JWT se puede usar para intercambiar información de manera segura entre dos partes. Dado que los tokens pueden ser firmados, los receptores pueden estar seguros de que los emisores son quienes dicen ser.

![alt text](img/token.jpeg)

Para agregar autenticación con JWT (JSON Web Tokens) en Django REST Framework, se puede usar la biblioteca [djangorestframework-simplejwt](https://pypi.org/project/djangorestframework-simplejwt/). A continuación, se muestran los pasos necesarios para configurarla:

1. Instalar las dependencias:

- Primero abrimos la consola con `CTRL + Ñ` e instalamos la biblioteca djangorestframework-simplejwt y su dependencia PyJWT.

```bash
pip install djangorestframework-simplejwt
```

2. Actualizar el archivo `book_store_api/settings.py`
- Configurar el sistema de autenticación para usar JWT:

![alt text](img/image-61.png)

![alt text](img/image-62.png)

3. Configurar URLs para obtener y refrescar tokens:
- En el archivo `book_store_api/urls.py`, configuramos las rutas para obtener y refrescar tokens JWT.

![alt text](img/image-63.png)

4. Proteger las vistas con JWT:

- Es importante asegurarse que las vistas estén protegidas por `JWT`. Para permitir que las vistas de `listado` y de `detalle` no requieran autenticación, se puede aplicar diferentes permisos a diferentes vistas. Podemos usar el método `get_permissions` para especificar qué permisos aplicar a cada acción (como listar, mostrar, crear, actualizar, etc.).
- Para hacerlo debemos modificar el archivo `book_store/views.py`:

![alt text](img/image-64.png)

> [!IMPORTANT]
> Hacer lo anterior con las otras tres vistas que tenemos (`AuthorViewSet`, `BookViewSet`, `BookAuthorViewSet`)

5. Ahora necesitamos probar que nuestro sistema de autenticación funcione correctamente, para esto primero necesitamos crear un usuario y una contraseña, la forma más fácil y rápida de hacerlo es a traves de la consola `CTRL + Ñ`

```bash
python manage.py createsuperuser
```

- Llenar los datos que nos piden:

![alt text](img/image-65.png)

- Podemos ver en nuestra base de datos que se guardo un registro con todos los datos de nuestro usuario:

![alt text](img/image-66.png)

6. Si ejecutamos nuestra aplicación...
```bash
python manage.py runserver
```
- ...y vamos a crear un nuevo género literario en el Postman nos damos cuenta que se nos retorna un código HTTP 401 que nos indica que no estamos autorizados para realizar esta acción, porque no se proporcionaron las credenciales de autenticación.

![alt text](img/image-67.png)

7. En el Postman vamos a construir un nuevo folder y nuevo request que nos va permitir obtener nuestro `JWT`, seguimos los pasos descritos a continuación:

![alt text](img/image-68.png)

#### Entendiendo los tokens de access y refresh
1. Access Token (Token de acceso):
- **Propósito:** El token de acceso se usa para autenticar y autorizar solicitudes a las APIs protegidas. Es lo que envías en el encabezado de autorización `(Authorization: Bearer <access_token>)` en las solicitudes subsecuentes para acceder a los recursos protegidos.
- **Vida útil:** Generalmente tiene una vida útil corta (por ejemplo, 5-15 minutos) para limitar la exposición en caso de que sea comprometido.
2. Refresh Token (Token de refresco):
- **Propósito:** El token de refresco se usa para obtener un nuevo token de acceso sin necesidad de que el usuario vuelva a autenticarse. Esto mejora la experiencia del usuario al evitar que tenga que ingresar sus credenciales repetidamente.
- **Vida útil:** Tiene una vida útil más larga (por ejemplo, 1 día o más). Sin embargo, debe ser almacenado y manejado de manera segura.

## <span style="color: orange;">Pasos para usar los tokens en Postman</span>
1. Crear dos nuevas variables de entorno.
- Vamos a editar nuestro Environment

![alt text](img/image-69.png)

- Creamos dos nuevas variables de entorno `access_token` y `refresh_token`

![alt text](img/image-70.png)

2. Agregar script en la sección Scripts:
- Ir a nuestro request `api/token/`
- Agregar el siguiente script para guardar los tokens en variables de entorno:

![alt text](img/image-71.png)

- Cuando le damos clic a `Send` y miramos nuestras variables de entorno, vemos que los valores de `access` y `refresh` se insertaron correctamente.

![alt text](img/image-72.png)

3. Creemos un nuevo request para el refresh.

- Como podemos ver estamos usando en el campo `refresh` que se le envía a la `API` nuestra variable de entorno. Esto nos permite automatizar el profeso y no tener que copiar el `refresh` manualmente cada vez que necesitemos refrescar nuestro token de acceso.

![alt text](img/image-73.png)

- En los scripts añadimos nuestro código para que se actualice el `access_token` automáticamente.

![alt text](img/image-74.png)

4. Para todos los `create`, `update` y `delete`, se debe actualizar el encabezado de autorización, ya que estas son solicitudes protegidas.

![alt text](img/image-75.png)

- En cada una de las solicitudes mencionadas anteriormente agregar el encabezado de autorización:

![alt text](img/image-76.png)

> [!IMPORTANT]
> Todos lo métodos `create`, `update` y `delete` para todos los folders `Genre`, `Author`, `Book` y `BookAuthor`, deben quedar funcionando correctamente.

> [!TIP]
> La página [jwt.io](https://jwt.io/) es una herramienta poderosa y versátil para trabajar con JWT. Puedes usarla para decodificar, verificar y generar tokens, así como para aprender más sobre su funcionamiento. Es especialmente útil en el desarrollo y depuración de aplicaciones que utilizan JWT para autenticación y autorización.
> ![alt text](img/image-77.png)