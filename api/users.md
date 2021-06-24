# Operaciones de usuario

Las siguientes son las operaciones habilitadas para ejecutar sobre el recurso usuario.

> Es importante recordar que para hacer solicitudes al API se debe hacer uso de las llaves de acceso brindadas

## Búsqueda de usuario

| ----------- | ----------- |
| Endpoint    | `/users`    |
| Método      | `POST`      |

Para consultar un usuario se debe enviar un objeto json en el cuerpo de la petición con uno de los dos parámetros permitidos para búsquedas: correo electrónico o cédula.
````
{ 'email': ... | 'idNumber': ... }
````
| ----------- | ----------- |
| email       | Cadena de texto |
| Método      | Números         |

### Respuestas

Las respuestas del servicio pueden ser las siguientes:

| Código      | Cuerpo      | Descripción |
| ----------- | ----------- | ----------- |
| 400         |             | En caso que el cuerpo enviado no cumpla con los parámetros de consulta requeridos. |
| 404         |             | En caso que no exista un usuario que cumpla con los parámetros de búsqueda. |
| 200         | Objeto en json con la información de un usuario | En caso de que la consulta sea exitosa. |


### Ejemplo
