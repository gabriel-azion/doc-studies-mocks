Text: ---
schema: blog_post
title: Mejorando la gestión de datos con Edge Storage de Azion
authors:
    - src/content/authors/gabriel.franca.md
meta_tags: azion, edge storage, almacenamiento de objetos, gestión de datos, serverless, s3 api
excerpt: >-
    Descubre cómo Edge Storage de Azion simplifica la gestión de datos y mejora el rendimiento de las aplicaciones. Conoce los beneficios del almacenamiento de objetos en el edge de la red y cómo aprovecharlo utilizando la REST API, CLI y Edge Functions Storage API de Azion.
description: >-
    Este blog se adentra en Edge Storage de Azion, una solución de almacenamiento de objetos diseñada para simplificar la gestión de datos y potenciar el rendimiento de las aplicaciones. Cubre los beneficios clave, la configuración y la gestión de datos usando S3 API, REST API, Azion CLI y Edge Functions Storage API.
img_featured: >-
    /assets/blog/images/uploads/storage-image.png
categories:
    - developers
related_content:
namespace: blogpost_azion_edge_storage
date: 2024-05-09T06:00:00Z
date_updated:
resourceHub:
    flags:
        contentType: Blog
permalink: /mejorando-la-gestión-de-datos-con-edge-storage-de-azion/

---

Como desarrolladores, navegar por el complejo mundo del almacenamiento de datos a menudo puede parecer intimidante. Existe una constante necesidad de equilibrar la gestión de crecientes volúmenes de datos, garantizar un rápido acceso y mantener el rendimiento del sistema.

¿Qué pasaría si pudieras aprovechar el concepto de almacenamiento de objetos, desplegando tus datos en el edge de la red, beneficiándote de un acceso de baja latencia, escalabilidad, costos predecibles y alta disponibilidad sin tener que lidiar con las complejidades de los sistemas de almacenamiento tradicionales?

En este blog, profundizamos en Edge Storage de Azion, una solución de almacenamiento de objetos diseñada pensando en los desarrolladores, simplificando el proceso de gestión de datos y potenciando el rendimiento de las aplicaciones.

## Aprovechando el Almacenamiento de Objetos en el Edge

A través de Edge Storage de Azion, la gestión de activos tales como imágenes y archivos se puede realizar sin enredarse en las complejidades de la gestión de infraestructuras. Esto permite a los usuarios concentrarse en la construcción de aplicaciones innovadoras, evitando cualquier obstáculo de infraestructura.

Los beneficios clave incluyen:

- API Compatible con S3: esta compatibilidad facilita la migración desde otros sistemas de almacenamiento en la nube que usan la API de S3, permitiendo la transición sin la necesidad de cambiar el código de la aplicación existente.
- Escalabilidad: la escalabilidad ilimitada proporcionada por las infraestructuras edge elimina cualquier restricción en la capacidad de almacenamiento. Los usuarios pueden ajustar el almacenamiento según su necesidades.
- Fiabilidad: el edge asegura un rendimiento confiable y consistente.
- Predicción de costos: se pueden evitar costos inesperados manteniendo los gastos de transferencia de datos dentro de los presupuestos predeterminados.
- Arquitectura Serverless: la arquitectura serverless ofrece un modelo de desarrollo de aplicaciones práctico, enfocado en la simplicidad y la adaptabilidad.
- Evitar el Bloqueo de Proveedores: esta flexibilidad facilita la toma de decisiones estratégicas y promueve precios competitivos.
- No Más Cargo por Egresos: con el edge computing, el procesamiento de datos ocurre más cerca de la fuente, reduciendo considerablemente los volúmenes de transferencia de datos hacia y desde el servidor central. Como resultado, las empresas pueden evitar incurrir en altos cargos de egreso a menudo asociados con los servicios en la nube, ahorrando así en costos operativos.

## Configuración y Simplificación de la Gestión de Datos

Edge Storage gestiona datos a través de objetos. Cada objeto incluye:

- Datos que componen el objeto.
- Metadatos asociados, como el tipo de medio y el tamaño del objeto.
- Una clave de objeto como identificador único.

### S3 API

Edge Storage es compatible con la API de S3. Esta característica funciona de la siguiente manera:

1. Las credenciales pueden ser administradas a través del endpoint `/s3-credentials`. Los métodos relacionados con las credenciales incluyen:

1. GET: recupera datos de todas las credenciales S3 registradas con Azion.
2. GET por ID: recupera datos de una credencial S3 registrada con Azion.
3. POST: crea una credencial S3.
4. DELETE: elimina las credenciales S3 de la cuenta.

2. Una vez creadas las credenciales, puedes usarlas a través de:

1. S3cmd
2. S3 API a través del endpoint de la región `https://s3.use-east-005.azionstorage.net/`
3. Las bibliotecas relacionadas con el manejo de S3 para tu lenguaje de programación elegido.

Creando credenciales S3 para ser utilizadas con Edge Storage:

```
curl --location 'https://api.azion.com/v4/storage/s3-credentials \
--header 'Accept: application/json' \
--header 'Authorization: Token xxxxxxx \
--header 'Content-Type: application/json' \
--data '{
  "name": "My S3 Credential",
  "capabilities": ["listAllBucketNames", "listFiles"],
  "bucket": "my-bucket-name",
  // expiration based on the timezone defined in RTM settings
  "expiration_date": "2025-01-31T10:57:00"

}'
```

Configurando tus credenciales en S3cmd:

```
user@user ~ % s3cmd --configure
Ingresa nuevos valores o acepta los predeterminados entre paréntesis con Enter.
Consulta el manual del usuario para una descripción detallada de todas las opciones.
La Clave de Acceso y la Clave Secreta son tus identificadores para Amazon S3. Déjalas vacías para utilizar las variables del entorno.
Clave de Acceso: [your-recently-created-access-key]
Clave Secreta:  [your-recently-created-secret]
Región Predeterminada....
Endpoint S3 [s3.amazonaws.com]: https://s3.use-east-005.azionstorage.net/
```

Ahora puedes acceder y manipular objetos a través de S3cmd dependiendo de las capacidades asignadas a la credencial S3.

Subiendo un objeto usando la API S3

```
curl --location --request PUT 'https://s3.us-east-005.azionstorage.net/<bucket_name>/<object_key>' \
    --header 'Content-Type: text/plain' \
    --header 'X-Amz-Date: 20240304T125612Z' \
    --header 'Authorization: AWS4-HMAC-SHA256 Credential=<access_key>/<date>/us-east-1/execute-api/aws4_request, SignedHeaders=content-length;content-type;host;x-amz-date, Signature=<encrypted_signature>' \
    --data '<filepath>'
```

Un usuario, siempre y cuando esté asignado a un equipo con permiso para editar las credenciales de almacenamiento, puede crear credenciales que serán visibles para otros usuarios en la misma cuenta. Una vez creada una credencial, no se puede editar, y las claves secretas solo se presentarán en el momento de su creación. De esta manera, al ver una credencial después de haberla creado, se omitirán las claves.

Las credenciales se pueden asignar a un bucket específico o a todos los buckets creados por la cuenta, pero no a un grupo de buckets. Aunque es posible crear un conjunto de credenciales, estas no tendrán poderes de gestión sobre el bucket o las propias credenciales - la gestión de buckets y credenciales sólo puede llevarse a cabo a través de la REST API.

No obstante, las credenciales proporcionan un conjunto específico de posibles operaciones con respecto a los objetos en el bucket. Con las credenciales apropiadas, es posible realizar operaciones tales como listar, leer, modificar y borrar objetos, siempre y cuando el bucket tenga los permisos necesarios. Las credenciales S3 operan de forma independiente del nivel de acceso establecido para el bucket usando la REST API, definido por la propiedad `edge_access`. Por ejemplo, si se crea una credencial con la capacidad `writeFiles` para un bucket con permisos `read_only`, la credencial todavía se puede utilizar para agregar o modificar archivos en el bucket, mientras que no se puede usar la API de Azion para esa misma operación.

A pesar de que la gestión de buckets y credenciales se limita a la REST API, los propios objetos se pueden manipular con las credenciales con permiso.

---

### REST API

Azion proporciona métodos de la REST API para almacenar objetos, desde la creación y modificación de buckets y sus permisos hasta la gestión de objetos.

Digamos que deseas utilizar el almacenamiento de objetos como el origen para una aplicación edge estática. Para hacerlo, necesitas:

1. Crear un bucket.
2. Subir el archivo que contiene tu aplicación dentro de un directorio `src`. Por ejemplo:
  
```
src/index.html
```

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="styles/style.css">
</head>
<body>
    <h1>Hello world!</h1>
    <p>Soy un objeto de un bucket.</p>
</body>
</html>
```

Puedes acceder a las instrucciones paso a paso en esta [guía](https://www.azion.com/en/documentation/products/guides/upload-and-download-objects-from-bucket/) para subir y descargar objetos desde un bucket de Edge Storage de Azion.

---

### Azion CLI

Otra alternativa es inicializar y desplegar una [aplicación a través de Azion CLI](https://www.azion.com/en/documentation/devtools/cli/init/). Cuando inicializas una aplicación a través del comando `azion init` y la despliegas en el edge:

1. Se crea automáticamente un bucket con el nombre que elegiste para el proyecto.
2. Tu aplicación estática se almacena en él.

Puedes ver más información sobre [cómo desplegar una aplicación a través de la guía Azion CLI](https://www.azion.com/en/documentation/products/cli/frameworks/react/), donde se presentan los pasos para desplegar una aplicación React en la plataforma.

---

### Azion Edge Functions Storage API

El Edge Storage de Azion se puede acceder a través de [Edge Functions Storage API](https://www.azion.com/en/documentation/devtools/runtime/api-reference/storage/). Esta interfaz te permite leer y escribir datos en el almacenamiento y sus buckets asociados.

Para comenzar con Storage API, necesitas:

1. Importar las APIs dentro de tu edge function:

```
import Storage from "azion:storage";
```

2. Instanciar un nuevo objeto Storage:

```
const storage = new Storage(bucket);
```

3. Elegir e implementar los [métodos enumerados en la documentación](https://www.azion.com/en/documentation/devtools/runtime/api-reference/storage/).

---

## Conclusión

Edge Storage de Azion se presenta como una solución a los desafíos de almacenamiento y gestión de datos, transformando cómo los desarrolladores abordan el rendimiento de las aplicaciones. Al aprovechar las tecnologías de almacenamiento de objetos en el edge de la red, no solo ofrece beneficios clave como la escalabilidad, alta fiabilidad y predicción de costos, sino que también simplifica el proceso de desarrollo.

Con una gestión de datos simplificada utilizando la REST API, CLI y Edge Functions Storage API de Azion, que son amigables para el usuario, los desarrolladores pueden enfocarse en la innovación en lugar de en los desafíos organizativos. Al avanzar hacia el futuro con Edge Storage de Azion, no solo estamos superando los problemas de datos, sino también desbloqueando el tremendo potencial que yace en nuestros datos, listo para potenciar nuestras aplicaciones edge.

---

		- Traduce este texto al inglés. 
		- No cambies el contexto.
		- El formato de salida debe ser markdown.
		- Act like a fluent translator and editor to localized English, and avoid regionalisms.
		- I want you to prioritize simple verb tenses and structures, and avoid compound tenses that can increase the complexity of the translated version.
		- This content is around computing and technology, you should prioritize the use of popular and related terms.
		- Don't translate the following terms: edge computing, edge, Azion, edge application, edge function, edge firewall [TO BE COMPLETED BY THE TERM SHEET]
		- Use articles on edge computing, [TO BE COMPLETED BY THE TERM SHEET]
		- Use articles to edge [TO BE COMPLETED BY THE TERM SHEET]
		- You should always translate request as request.
		- Don't change the context of the content.
		- Always translate using second person: you and your conjugations.
- Translate this text to english. 
- Don't change the context.
- The output format must be markdown.
- Act like a fluent translator and editor to localized English, and avoid regionalisms.
- I want you to prioritize simple verb tenses and structures, and avoid compound tenses that can increase the complexity of the translated version.
- This content is around computing and technology, you should prioritize the use of popular and related terms.
- Don't translate the following terms: edge computing, edge, Azion, edge application, edge function, edge firewall [TO BE COMPLETED BY THE TERM SHEET]
- Use feminine articles for: edge computing, [TO BE COMPLETED BY THE TERM SHEET]
- Use masculine articles for: edge [TO BE COMPLETED BY THE TERM SHEET]
- You should always translate request as request.
- Don't change the context of the content.
- Always translate using second person: you and your conjugations.