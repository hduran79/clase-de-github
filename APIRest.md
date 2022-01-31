# ¿Qué es la arquitectura REST?
REST es una arquitectura de desarrollo web que puede ser utilizada en cualquier cliente HTTP. Además, es mucho más simple que otras arquitecturas ya existentes, como pueden ser XML-RPC o SOAP. Esta simplicidad se consigue porque emplea una interfaz web que usa hipermedios para la representación y transición de la información.

Esta arquitectura fue definida por Roy Fielding en el año 2000, que además es unos de los principales artífices de la especificación del protocolo HTTP.

La principal ventaja de esta arquitectura es que ha aportado a la web una mayor escalabilidad, es decir, dan soporte a un mayor número de componentes y las interacciones entre ellos. 

## Características que presenta la arquitectura REST:
* Es un protocolo sin estado, debido a que no se guarda la información en el servidor. Es decir, toda la información será enviada por el cliente en cada mensaje HTTP, consiguiendo un ahorro en variables de sesión y almacenamiento interno del servidor.
* Presenta un conjunto de operaciones bien definidas, como GET, POST, PUT y DELETE, que se emplea en todos los recursos.
* Utiliza URIs únicas siguiendo una sintaxis universal.
* Emplea hipermedios para representar la información, que suelen ser HTML, XML o JSON.


# SEGURIDAD EN SERVICIOS REST

1.  **Utilizar HTTPS** => La información viaja de manera mas segura porque va cifrada (let's encrypt permite obtener certificados de manera gratis)

2.  **Poner autenticación y autorización en los endpoints** => **_Autenticación_** El usuario se debe de identificar de alguna forma y enviar un token de sesión sino no puede acceder al endpoint y **_autorización_** Verificar si el usuario tiene permiso para ejecutar el endpoint.
    **Nota**: No basta con solo tener una autenticación.

3.  **Utilizar Json Web Tokens (JWT)** => Cuando el usuario se autentique en la APP se debe generar un JWT es uan practica que funciona muy bien y son seguros, una alternativa es utilizar **_API Keys_** la desventaja es que estas API Keys son estáticas a no ser que se cambie manualmente, a diferencia de JWT tienen un tiempo de vida.
    **Nota**: Existe una plataforma **_OAth0_** que nos permite añadir elementos de seguridad como iniciar session a un sistema y este se encarga de la generación del JWT.

    JWT es un estándar de código abierto basado en JSON para crear tokens de acceso que nos permiten securizar las comunicaciones entre cliente y servidor

4.  **No poner información sensible en la URL** => Es un problema porque hay servidores que guardan información de las URLs en sus logs.
    **_Recomendación_** enviar información sensible por los **headers**, por ejemplo los tokens de session.

5.  **Validar los parámetros de entrada** => Esto evita la inyección de código.


# DISEÑAR BIEN API REST

¿Para qué sirve API Rest? Recuperar información de una página.


## Consejo # 1 - Representar recursos y no acciones
Las URI recibirán nombres que no deben implicar una acción, es decir, se debe evitar colocar verbos en ellas. Esto se debe a que se pone énfasis a los sustantivos.

Deben ser únicas, no debemos tener más de una URI para identificar un mismo recurso.

Deben ser independiente de formato, es decir, no debe representar ninguna extensión.

Deben mantener una jerarquía lógica. La jerarquía es el criterio por el que se ordena los elementos.

Los filtrados de información de un recurso no se hacen en la URI.

* POST: crear un recurso nuevo.
* PUT: modificar un recurso existente.
* GET: consultar información de un recurso.
* DELETE: eliminar un recurso determinado.
* PATCH: modificar solamente un atributo de un recurso.

```javascript
Bad
GET /deleteproduct/123  =>  De esta forma estamos mostrando acciones que queremos ejecutar.
GET /fotos/12/borrar => utiliza un verbo
GET /fotos/12/usuario/231 => foto 12 tiene usuario 231, situación poco lógica
GET /fotos/fecha/octubre => filtrar datos con el mes de octubre.

Good
DELETE /product/123  =>  Esta es la forma correcta para ejecutar la acción de borrar. 
GET /fotos/12 => Obtiene los datos de la foto con el id 12
GET /clientes/231/proyectos/ => debe volver a la lista de proyectos del cliente 231.
GET /clientes/231/proyectos/4 => debe volver al proyecto nº 4 del cliente 231.
GET /usuario/231/fotos/12 => usuario 231 tiene foto 12, algo que suena más lógico.
GET /fotos?fecha=octubre => filtrar datos con el mes de octubre.

```

## Consejo # 2 -  Definir los recursos

* Colecciones-c => Representan conjuntos de datos (Listado de productos)

Ejemplo: 

```javascript
> /products
```
  * Documentos-d => Son instancias dentro de la colección (El producto 123 es documento dentro de la colección de productos)

Ejemplo:
```javascript
/products/1 
/products/pencil
```

* Store-s => Recursos manejados por el cliente, la convención debe ser en (plural)

Ejemplo:
```javascript
/users/1/favorites
```

## Consejo # 3 - No devolver siempre 200 Ok

ES una mala practica devolver 200 para todo

Ejemplo: Vamos a guardar un cliente y el api me devuelve:

```java
Request
POST /customers

Response
HTTP/1.1 200 OK
Date: Fri, 28 Enero 2022 19:03:01 GMT
Content-Type: application/json
{
    "error": true,
    "message": "Invalid ID"
}

```
> Nota: En el cuerpo de la respuesta nos envía un json indicando que hubo un error pero el httpCode llega un 200, las API-Rest están diseñadas para tener significado a partir de los métodos y códigos de respuesta, el deber ser es que llega el código http de lo que realmente esta pasando.

> Solución: Utilizar códigos  HTTP para dar significado a las respuestas
- 200 OK. Respuesta estándar para peticiones correctas.
- 201 -> Created. La petición ha sido completada.
- 202 -> Accepted. En procesamiento (asíncronos), pero no ha sido completado, se pueden hacer otros llamados para verificar si el proceso ya termino.
- 204 -> Solicitud exitosa, Respuesta sin contenido. (Borrar un producto pero no devuelve nada en el cuerpo de la respuesta)
- 400 -> Bad Request. La solicitud contiene sintaxis errónea.
- 401 -> No autorizado (usuario no autenticado)
- 403 -> Forbidden. La solicitud fue legal, No tiene los privilegios. (hay usuarios que pueden listar productos pero no pueden eliminar)
- 404 -> Not Found. Recurso no encontrado. Intenta hacer un GET pero el método es un POST.
- 500 -> Internal Server Error. Son situaciones de error ajenas a la naturaleza del servidor web (TimeOut).

## Consejo # 4 - No hacer todo con POST

Se deben de utilizar los métodos HTTP para indicar la intención. 

* GET: Para Obtener datos (select)
* POST: Crear nuevos recuros (insert)
* PUT: Para actualizar recuros (update) -> Desventaja se debe pasar el recurso completo asi se quiera cambiar un solo campo.
* DELETE: Para eliminar un recurso (delete)
* PATCH: Es la versión mejorada de PUT,  solo se pasan los campos que se quieran cambiar, Muchos frameworks de programación REST todavía no lo soportan
 
## Consejo # 5 - Asegurar las APIs
Métodos de autenticación
* Api Key
* Bearer token
* Basic Auth
* Digest Auth
* OAuth 1.0
* OAuth 2.0
* AWS Signature
* Akami EdgeGrid

**Nota**: Se recomienda que las APIs tengan un método de autenticación para evitar ataques informáticos.

## Consejo # 6 - Versionar las APIs
* Las APIs cambian con el tiempo.
* Se debe dar tiempo a los clientes que se actualicen a la nueva versión
* No se recomienda hacer cambios a las APIs y dejarlos así porque pueden causar problemas de compatibilidad.

```javascript
https://mydominio/rest/v3/products
```

## Consejo # 7 - Usa JSON, pero úsalo bien

```java
bad -> esto no es formato json.
ya quedo bien

good -> formato json correcto.
{
    "error": true,
    "message": "Invalid ID"
}
```

## NOTAS    
* JSON es el estándar por defecto en REST.
* Se debe retornar un JSON válido.
* No existe un estándar oficial de REST.


# Reglas de una arquitectura REST

1. Interfaz uniforme
* La interfaz de basa en recursos (por ejemplo el recurso Empleado (Id, Nombre, Apellido, Puesto, Sueldo)
* El servidor retornado los datos en algún formato (html, json, xml...)
* El recurso solicitado se suele enviar un parámetro o un objeto en el cuerpo.
* Usar las características del protocolo http para mejorar la semántica
    * HTTP Verbs => /product/123
    * HTTP Status Codes => 200, 401
    * HTTP Authentication => Auth Basic

2. Peticiones sin estado
* Es un protocolo sin estado, debido a que no se guarda la información en el servidor. 
* Toda la información será enviada por el cliente en cada mensaje HTTP, consiguiendo un ahorro en variables de sesión y almacenamiento interno del servidor.
* http es un protocolo sin estado -> mayor rendimiento

3. Cacheable
* En la web los clientes pueden cachear las respuestas del servidor.
* Las respuestas se deben marcar de forma implícita o explícita como cacheables o no.
* En futuras peticiones, el cliente sabrá si puede reutilizar o no los datos que ya ha obtenido.
* Si ahorramos peticiones, mejoraremos la escabilidad de la aplicación y el rendimiento en cliente (evitamos principalmente la latencia).

4. Separación de cliente y servidor
* El cliente y servidor están separados, su unión es mediante el protocolo HTTP (interfaz uniforme).
* Los desarrollos en frontend y backend se hacen por separado, teniendo en cuenta la API.
* Mientras la interfaz no cambie, podremos cambiar el cliente o el servidor sin problemas.

5. Sistema de Capas
* El cliente puede estar conectado mediante la interfaz al servidor o a un intermediario, para el es irrelevante y desconocido.
* Al cliente solo le preocupa que la API REST funcione como debe: no importa el COMO sino el QUE
* El uso de capas o servidores intermedios puede servir para aumentar la escalabilidad (sistemas de balanceo de carga, cachés) o para implementar políticas de seguridad


6. CORS
* En el 2008 se publicó la primera versión de la especificación XMLHttpRequest Level 2.
* CORS es el acrónimo de Cross-origin resource sharing.
* Debemos tener presente, que los navegadores antiguos no soportan CORS.
* Esta nueva especificación, añade funcionalidades nuevas a las peticiones AJAX como las peticiones entre dominios (cross-site), eventos de progreso y envio de datos binarios.
* CORS requiere configuraciones en el servidor o a nivel de desarrollo.