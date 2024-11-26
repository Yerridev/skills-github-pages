---
title: Cookies, Sesiones y Autenticación
author: Yerridev
description: Aprendiendo php
---

Seguimiento a tus usuarios.
- Si no ofreces inicios de sesión y contraseñas.
    - Almacenar -> Detalles sobre *sesion e curso de un usuario*
    - Reconocer cuando regrese a tu sitio.
- Tecnologías que ofrecen este tipo de interacción:
    - Simples cookies del navegador.
    - Gestión de sesiones y autenticación HTTP.
    - Configurar tu sitio segun:
        - Preferencias de usuarios.


### Uso de cookies en PHP
##### Cookie
>[!Cookie]
>Es un elemento de datos que un servidor web guarda en el disco duro de tu ordenar a través de un navegador web.
- Guarda cualquier información alfanumérica
    - *menor a 4KB*
- Puede:
    - Recuperarse de tu ordenar y ser devuelto por el servidor.
###### Usos:
- Seguimiento de sesiones
- Mantenimiento de datos de visitas.
- La conservación del contenido del carrito de compras.
- Almacenamiento de los datos de inicio de sesión.

###### Privacidad:
- Solo se puede leer desde el sitio web de la empresa que las ha emitido.
- Evita que otros sitios web accedan a datos para los que no están autorizados.

###### Transferencias:
- Se intercambia durante la transferencia de encabezamiento
    - Antes de que se envié el HTML actual de una página web.
- Es imposible enviar una cookie una vez que se ha envidado cualquier código HTML.
- Importante:
    - Planificar cuidadosamente el uso de cookies.

Grafico -> Cuadro de diálogo típico de solicitud y respuesta entre un navegador web y un servidor web que pasa las cookies.
![[Pasted image 20240924024648.png]]
Diálogo con cookies *pregunta/respuesta* entre *navegador/servidor*
- Este intercambio muestra un navegador que recibe dos páginas:
    1. Navegador *emite* una solicitud para recoger la página principal `index.html` del sitio web `https://name.com` El primer encabezamiento especifica el archivo y segundo especifica el servidor.
    2. Cuando servidor web *recibe* encabezamientos, devuelve algunos de los suyos. El segundo encabezamiento define el tipo de contenido a enviar *(text/html)* y el tercero envía una cookie con el nomb[...]
    3. Cuando navegador solita la página web, también devuelve la coolie name con el valor value.
    4. No tiene que reenviarse la cookie, sino que simplemente devuelve la página solicitada.
###### Mejor uso:
- Almacenar datos como el *idioma*
- Configuración de la moneda.

#### Configuración de cookies
- Siempre y cuando no se haya transferido ningún HTML.
- Llamando a la función `setcookie()` 
 `{php icon title:'configuracion cookie'} setcookie(name, value, expire, path, domain, secure, httponly);`

- *name* -> Nombre de cookie.
    - Acceder al servidor en futuras solicitudes del navegador. 
    - Ejemplo:`location`
- *value* -> Valor cookie.
    - Los contenidos, puede tener 4 KB.
    - Ejemplo: `USA`
- *expire* (opcional) -> Fecha de caducación.
    - Si no se indica, la cookie expira cuando el navegador se cierra.
    - Ejemplo: `time() + segundos`
- *path* (opcional) -> La ruta de la cookie en el servidor. `/`
- *domain* (opcional) -> El dominio Internet de la cookie.
- *secure* (opcional) -> Si debe usar una conexión segura. 
- *httponly* (opcional) -> Si se debe usar protocolo HTTP.
###### Ejemplo:
 `{php icon title:'ejemplo cookie'} setcookie('location', 'USA', time() + 60 + 60 * 24 * 7 , '/');`
#### Acceso a cookies
- Tiene matriz para acceder a los datos  -> `$_COOKIE`
 `{php icon title:'Acceso cookies'} if(isset($_COOKIE['location'])) $location = $_COOKIE['location'];`

#### Eliminación de cookies
 `{php icon title:'Eliminación de cookies'} setcookie('location', 'USA', time() - 2592000, '/');`
### Autenticación HTTP

 - Utiliza el servidor web para la gestión de los usuarios y las contraseñas de la aplicación.

## Uso de Sesiones
- Querrás rastrear lo que un usuario esta haciendo de una página web a otra.
    - Lo puedes hacer configurando campos ocultos en los formularios.
- Pero solución más potente y sencilla:
    - *sesiones*
        - Son -> Grupos de variables almacenan en el servidor.
            - Solo se refiere al usuario actual.
        - Para -> Que las variables adecuadas se apliquen a los usuarios correctos.
        - PHP - *cookie*:
            - Guarda una cookie en los navegadores de los *usuarios* para identificarlos de manera única.
            - Esta cookie:
                - Solo tiene significado para el servidor web

## Inicio de Sesión
- Para iniciar una sesión se requiere:
    - Llamar a la función PHP -> `session_start`
        - Antes de que se haya generado cualquier HTML
        - Forma similar a como se envía las cookies.
- Guardar variables se sesión:
    - Asignar como parte de la matriz *$_SESSION*
      `{php icon title:'variable session'} $_SESSION['variable'] = $value;`
      - Después se puede volver a leer con la misma facilidad en posteriores ejecuciones de programa, como este caso:
       `{php icon title:'leer'} $variable = $_SESSION['variable'];`
