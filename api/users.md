# Operaciones de usuario

[Volver al inicio](../index.md)

Las siguientes son las operaciones habilitadas para ejecutar sobre el recurso usuario.

> Es importante recordar que para hacer solicitudes al API se debe hacer uso de las llaves de acceso brindadas. Para dudas de las llaves y ambientes puede revisar [nuestra guía](../guides/environment.md).

## Búsqueda de usuario

| Endpoint    | Método.     |
| ----------- | ----------- |
| `/users`    | `POST`      |

Para consultar un usuario se debe enviar un objeto json en el cuerpo de la petición, con alguno de los parámetros permitidos para búsquedas: correo electrónico y documento de identidad.

Nota: Si en la búsqueda se agrega el parámetro idNumber es obligatorio enviar el parámetro idType.

Esta operación hace uso del método POST para evitar enviar data sensible de los usuarios en la URL y dejar registro de la misma en el historial de herramientas de consulta o en logs de operación.

````
{ 'email': ..., 'idNumber': ..., 'idType': ... }
````

| Parámetro   | Tipo de dato    |
| ----------- | -----------     |
| email       | Cadena de texto |
| idNumber    | Cadena de texto alfanumérico |
| idType      | Cadena de texto con uno de los valores permitidos: **CC (Cédula de ciudadanía), TI (Tarjeta de identidad), CE (Cédula de extranjería), NIT (Número de identificación tributaria), PA (Pasaporte)** |

Las respuestas del servicio pueden ser las siguientes:

| Código      | Cuerpo      | Descripción |
| ----------- | ----------- | ----------- |
| 400         |             | En caso que el cuerpo enviado no cumpla con los parámetros de consulta requeridos. |
| 200         | Objeto en json con la información de los usuarios que hacen match con la búsqueda | En caso de que la consulta sea exitosa. |

En el caso de que la consulta sea exitosa la respuesta será un objeto json con la siguiente información:

````
{
    "count": 1,
    "next": "...?page=2",
    "previous": null,
    "results": [
        {
            "email": "...",
            "idNumber": "...",
            "idType": "...",
            "firstName": "...",
            "lastName": "...",
            "activeMembership": true
        },
        ...
    ]
}
````

| Campo      | Tipo      | Descripción |
| ----------- | ----------- | ----------- |
| count       | Número entero | Cantidad de elementos en la respuesta |
| next        | Cadena de caracteres | Ruta para realizar la siguiente consulta, si el número de elementos supera la paginación definida |
| previous    | Cadena de caracteres | Ruta para realizar la consulta anterior en el caso que se esté consultando los elementos de la página 2 en adelante |
| email       | Cadena de caracteres | Correo electrónico registrado por el usuario en nuestra plataforma |
| idNumber    | Cadena de texto alfanumérico | Número de identificación registrada por el usuario. *Este campo es opcional.* |
| idType      | Cadena de caracteres | Tipo de identificación del usuario en la plataforma: **CC (Cédula de ciudadanía), TI (Tarjeta de identidad), CE (Cédula de extranjería), NIT (Número de identificación tributaria), PA (Pasaporte)**. *Este campo es opcional.* |
| firstName   | Cadena de caracteres | Nombre o nombres del usuario. *Este campo es opcional.* |
| lastName    | Cadena de caracteres | Apellido o apellidos del usuario. *Este campo es opcional.* |
| activeMembership | Booleano | Indica si el usuario tiene una membresía activa en la plataforma. |

### Ejemplo

Consulta por email
````
POST
Body:
{ 
   "email": "ejemplo@prueba.com"
}
````

````
Código de respuesta: 200
Body:
{
    "count": 1,
    "next": null,
    "previous": null,
    "results": [
        {
            "email": "ejemplo@prueba.com",
            "idNumber": "1111111111",
            "idType": "CC",
            "firstName": "Ejemplo",
            "lastName": "Prueba Documentación",
            "activeMembership": true
        }
    ]
}
````

Consulta por número de identificación

````
POST
Body:
{ 
   "idNumber": "11111111",
   "idType"  : "CC"
}
````

````
Código de respuesta: 200
Body:
{
    "count": 1,
    "next": null,
    "previous": null,
    "results": [
        {  
            "email": "ejemplo2@prueba.com",
            "idNumber": "11111111",
            "idType": "CC",
            "firstName": "Ejemplo",
            "lastName": "Prueba Documentación",
            "activeMembership": false
        }
    ]
}
````
[Volver al inicio](../index.md)
