# Llaves y ambientes

[Volver al inicio](../index.md)

Alfred cuenta con dos ambientes para acceso por parte de terceros:

- **Sandbox**: Es el ambiente de pruebas, el cual puedes usar para consultar o realizar solicitudes "falsas" sobre nuestra infraestructura. Su uso se recomienda mientras se esté desarrollando la integración y haciendo pruebas en tus servidores locales o de pruebas.
- **Producción**: Es el ambiente sobre el cual se ejecutan operaciones reales.

Ambas URL's serán brindadas junto con las llaves de acceso a cada ambiente.

## Llaves

Para acceder a cada ambiente, cada usuario cuenta con un par de llaves **privadas** que deben ser tratadas como un secreto y usarlas en ambientes de backend. 

- La llave para acceder al ambiente de pruebas sigue el formato `test_<token>`, ejemplo: `test_Kw4aC0rZVgLZQn209NbEKPuXLzBD28Zx`

- La llave para acceder al ambiente de producción sigue el formato `prod_<token>`, ejemplo: `prod_Kw4aC0rZVgLZQn209NbEKPuXLzBD28Zx`

Cada llave puede ser utilizada únicamente en su ambiente y no son intercambiables.

### Uso de llaves

Para hacer uso de cada llave en su ambiente correspondiente, se debe colocar en el encabezado de la petición de la siguiente manera:

`````
Authorization: Bearer <token>
`````
Ejemplo:
`````
Authorization: Bearer prod_Kw4aC0rZVgLZQn209NbEKPuXLzBD28Zx
`````

> Las llaves pueden tener un tiempo de expiración, esto se definirá con el equipo de alfred en el momento del acuerdo.
[Volver al inicio](../index.md)
