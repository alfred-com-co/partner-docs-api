# Operaciones de usuario

Las siguientes son las operaciones habilitadas para ejecutar sobre el recurso usuario.

>> Es importante recordar que para hacer solicitudes al API se debe hacer uso de las llaves de acceso brindadas

## Búsqueda de usuario

| ----------- | ----------- |
| Endpoint    | `/users`    |
| Método      | `POST`      |
| Parámetros  | Para consultar un usuario se debe enviar un objeto json en el cuerpo de la petición con uno de los dos parámetros permitidos para búsquedas: correo electrónico o cédula.
````
{ 'email': ... | 'idNumber': ... }
````
|
| Respuestas  | 

|

### Ejemplo
