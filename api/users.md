# Operaciones de usuario

Las siguientes son las operaciones habilitadas para ejecutar sobre el recurso usuario.

> Es importante recordar que para hacer solicitudes al API se debe hacer uso de las llaves de acceso brindadas

## Búsqueda de usuario

| Endpoint    | Método.     |
| ----------- | ----------- |
| `/users`    | `POST`      |

Para consultar un usuario se debe enviar un objeto json en el cuerpo de la petición con uno de los dos parámetros permitidos para búsquedas: correo electrónico o cédula.

Esta operación hace uso del método POST para evitar enviar data sensible de los usuarios en la URL y dejar registro de la misma en el historial de herramientas de consulta o en logs de operación.
````
{ 'email': ... | 'idNumber': ... }
````
| Parámetro   | Tipo de dato    |
| ----------- | -----------     |
| email       | Cadena de texto |
| Método      | Números enteros sin puntos |

Las respuestas del servicio pueden ser las siguientes:

| Código      | Cuerpo      | Descripción |
| ----------- | ----------- | ----------- |
| 400         |             | En caso que el cuerpo enviado no cumpla con los parámetros de consulta requeridos. |
| 404         |             | En caso que no exista un usuario que cumpla con los parámetros de búsqueda. |
| 200         | Objeto en json con la información de un usuario | En caso de que la consulta sea exitosa. |

En el caso de que la consulta sea exitosa la respuesta será un objeto json con la siguiente información:
````
{ 
    "email": "...",
    "idNumber": ...,
    "idType": "...",
    "firstName": "...",
    "lastName": "...",
    "activeMembership": true
}
````
| Campo      | Tipo      | Descripción |
| ----------- | ----------- | ----------- |
| email       | Cadena de caracteres | Correo electrónico registrado por el usuario en nuestra plataforma |
| idNumber    | Número entero | Número de indentificación registrada por el usuario. *Este campo es opcional.* |
| idType      | Cadena de caracteres | Tipo de identificación del usuario en la plataforma: CC (cédula de ciudadanía), CE (cédula de extranjería), NIT (número identificación tributario. *Este campo es opcional.* |
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
    "email": "ejemplo@prueba.com",
    "idNumber": 1111111111,
    "idType": "CC",
    "firstName": "Ejemplo",
    "lastName": "Prueba Documentación",
    "activeMembership": true
}
````

Consulta por número de identificación
````
POST
Body:
{ 
   "idNumber": 11111111
}
````

````
Código de respuesta: 200
Body:
{ 
    "email": "ejemplo2@prueba.com",
    "idNumber": 11111111,
    "idType": "CC",
    "firstName": "Ejemplo",
    "lastName": "Prueba Documentación",
    "activeMembership": false
}
````

