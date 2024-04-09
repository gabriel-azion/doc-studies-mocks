# Desarrollo y prueba local de edge functions con Azion CLI

Azion CLI es una herramienta eficiente para configurar entornos de prueba locales para edge functions. Puedes comenzar ejecutando el comando `azion dev` para iniciar el proceso de desarrollo local.

Para escenarios con funciones de edge firewall, solo necesitas agregar la flag `--firewall` al comando. Esta funcionalidad enriquece tus capacidades para probar y analizar las funciones del firewall antes de integrarlas al producto final.

Beneficios claves:

- Prevención de errores: prueba nuevas funciones o modificaciones antes de que enviarlas a producción, reduciendo el riesgo de introducir errores en el sistema.
- Debugging mejorado: depura el código de manera más efectiva y rápida en un entorno controlado.
- Optimización del desempeño: prueba el comportamiento de la aplicación bajo diferentes cargas o escenarios únicos de usuarios.
- Seguridad reforzada: identifica y soluciona vulnerabilidades de seguridad antes de que la aplicación esté en producción.
- Desarrollo eficiente: trabaja sin conexión a Internet, promoviendo la productividad y autonomía.
- Rentable: evita fixes post-producción que consumen muchos recursos, ahorrando tiempo y dinero al abordar problemas potenciales antes de la implementación.

## Requisitos

- Azion CLI.
- Node.js >= 18.

---

## Cómo probar las funciones de Edge Application

Para iniciar un entorno de pruebas local:

1. Abre la terminal, crea un nuevo directorio, y accede a él.
2. Inicia una aplicación a través de `azion init`.
3. Define un nombre para tu aplicación o acepta la sugerencia.
4. Selecciona JavaScript como template. 
> Puedes iniciar la aplicación basada en la template que quieras. Este ejemplo usa JavaScript.
5. Inicia el desarrollo local respondiendo sí a la interacción.
6. Instala las dependencias.
7. Después de un proceso de building, Azion mostrará el puerto para acceder a la aplicación.
8. Envía solicitudes al servidor y verifica el comportamiento.

>Nota: siempre puedes detener el proceso de la terminal y usar el comando `azion dev` para ejecutar la aplicación localmente. Los cambios aplicados a la función se reconstruyen utilizando una hot reload.

El comando `azion dev` inicia un entorno local donde puedes probar y monitorizar la funcionalidad y eficiencia de tus edge functions.

Las edge functions de Azion se ejecutan en el Azion Edge Runtime y son compatibles con las Web APIs y Azion APIs.

- Edge Functions Primeros pasos.
- Web APIs.
- Lista completa de las Web APIs que el Azion Edge Runtime es compatible.

---

## Cómo probar las funciones del Edge Firewall

Si has implementado funciones de firewall en tu sistema, tendrás que considerar condiciones especiales de prueba.

Para ello, debes ejecutar el comando `azion dev` con la bandera `--firewall`. Esto informa al sistema de que estás probando una función de edge firewall. 

- Edge functions para Edge Firewall.
- Network List API.
- Metadata API.

---

## Cómo funciona el desarrollo local de la Azion CLI

### Diagrama de Flujo

- A través de la CLI, el usuario ejecuta el comando `azion dev [flags]`.
- Azion CLI invoca a Vulcan, que gestiona la construcción y el desarrollo local.
- Vulcan inicializa un servidor y este servidor instancia el runtime. Este runtime soporta una lista de Web APIs y emula el actual Azion Edge Runtime.

### Responsabilidades

*Azion CLI*: actúa como el principal punto de interacción entre el usuario y el sistema. Gestiona todo el proceso de despliegue de la aplicación, asegurando un flujo de trabajo fluido y eficiente.

*Vulcan*: el motor que impulsa la inicialización, construcción y adaptación del proyecto. Adapta de forma inteligente el proyecto basado en la plantilla seleccionada, asegurando que la aplicación esté optimamente configurada para su uso previsto. Para el desarrollo local, Vulcan:

- Inicia un servidor.
- Instancia el Edge Runtime.
- Gestiona los cambios en el código fuente, implementando la hot reload.

---

## Sobre las edge eunctions

Las edge functions de Azion se utilizan para mejorar las edge applications o para reforzar la seguridad en un edge firewall. Ambas se ejecutan en el Azion Edge Runtime, reducen la latencia y ayudan a implementar un enfoque distribuido. OK, pero ¿cuál es la diferencia entre ellas? 

La diferencia está en cómo se estructuran las funciones, vamos a profundizar en eso.

### Edge Application Functions

Primero, las edge functions para las edge applications funcionan basándose en un evento fetch. Se inicializan con la función `addEventListener`, pasando fetch como el tipo de evento, y un evento. Por ejemplo:

```js
  addEventListener('fetch', event => {
      event.respondWith(handleRequest(event.request));
    });
```

Segundo, es necesario definir el comportamiento de la función handleRequest. Esta función tiene `event.request` como la firma. Estos datos se pueden usar más adelante para implementar la lógica necesaria, como:

- Manipular cookies.
- Implementar un comportamiento basado en el método de solicitud HTTP (POST, GET, PUT, DELETE).
- Acceder a los metadatos de la solicitud.

La función `handleRequest` puede ser definida como:

```js
  const html = `<!DOCTYPE html>
  <body>
    <h1>Hola Mundo</h1>
    <p>Este marcado fue generado por Azion - Edge Functions.</p>
  </body>`

  async function handleRequest(request) {
    return new Response(html, {
      headers: {
        "content-type": "text/html;charset=UTF-8",
      },
    })
  }
```

En este ejemplo, la respuesta será el contenido HTML, declarado previamente por la const html. Los encabezados pueden ser manipulados y, en el ejemplo, se establece el tipo de contenido.

Ejemplo completo:

```js
  const html = `<!DOCTYPE html>
  <body>
    <h1>Hola Mundo</h1>
    <p>Este marcado fue generado por Azion - Edge Functions.</p>
  </body>`

  async function handleRequest(request) {
    return new Response(html, {
      headers: {
        "content-type": "text/html;charset=UTF-8",
      },
    })
  }

  addEventListener('fetch', event => {
      event.respondWith(handleRequest(event.request));
    });
```

Conoce más sobre las edge functions para edge applications.


### Edge Firewall Functions

Las edge functions para Edge Firewall operan basándose en un evento firewall. Se inicializan usando la función `addEventListener`, pasando `'firewall'` como el tipo de evento, y un evento. Por ejemplo:

```js
  addEventListener('firewall', event => {
      event.deny();
  });
```

En este caso, el sistema envía una denegación en respuesta al evento firewall que ha sido activado. Podría haber otras reacciones a eventos como `event.continue()`, y `event.drop()` dependiendo de las circunstancias específicas o la lógica deseada.

Es necesario definir los comportamientos potenciales para diferentes reacciones a eventos dentro del oyente de eventos firewall. La respuesta exacta depende de la condición que se cumpla. Por ejemplo:

- Detecta niveles de amenaza.
- Block o lista de derechos de direcciones IP.
- Implementa comportamientos basados en patrones de tráfico.

Un ejemplo donde se define y utiliza la función `event.deny`:

```js
  // Define una lista de direcciones IP bloqueadas
  const blockedIPs = ["192.0.2.0", "203.0.113.0", "198.51.100.0"]

  addEventListener('firewall', event => {
      let ip = event.request.clientIP;
      if (blockedIPs.includes(ip)) {
          event.deny();
      } else {
          event.continue();
      }
  });
```


En este ejemplo, el oyente de eventos del firewall verifica la dirección IP que activó el evento contra la lista de IPs bloqueados. Si la IP está en la lista, se niega el evento. Si la IP no está en la lista, el evento continuará procesándose. Muestra cómo podrías usar el `event.deny()`, `event.continue()`, y `event.drop()` en escenarios reales de aplicación.


Aprende más sobre las edge functions para edge firewall.

---

## Conclusión

El uso de entornos de pruebas locales mejora el proceso de desarrollo del producto. El uso de herramientas como Azion CLI facilita la construcción de soluciones de software confiables, eficientes, seguras y de alto rendimiento. Al probar las edge functions con el comando `azion dev`, y agregando opcionalmente una bandera `--firewall` cuando sea necesario, los desarrolladores pueden sortear posibles obstáculos antes de llevar su código a producción. 

		
