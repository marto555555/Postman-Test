Books API

Esta API nos permite reservar un libro.


## Endpoints ##

## Status ##
GET `/status`

Devuelve el status de la API.

## Listado de Libros ## 
GET `/books`

Devuelve listado de libros .

Query parameters opcionales :

- type: fiction o non-fiction
- limit: un número entre 1 and 20.

## Obtener un libro ##
GET `/books/:bookId`

Obtenemos informacion detallada de un libro.

## Realizar un pedido ##
POST `/orders`

Permite realizar un nuevo pedido. Requiere autentificación.

La "request body" debe ser en formato JSON e incluir las siguientes propiedades:

- `bookId` - Integer - Requerido
- `customerName` - String - Requerido

Ejemplo:
```
POST `/orders/`
Authorization: Bearer <YOUR TOKEN>

{
  "bookId": 1,
  "customerName": "John"
}
```
La respuesta del body contiene el order Id.

## Obtener todos los pedidos ##
GET `/orders`

Permite ver todas los pedidos. Requiere authentication.

## Obtener un pedido. ##
GET `/orders/:orderId`

Nos permite ver todas un pedido existente. Requiere authentication.

## Actualizar un pedido. ##
PATCH `/orders/:orderId`

Actualizar un pedido existente. Requiere authentication.

El "request body" debe ser en formato JSON y nos permite editar las siguientes propiedades:

- `customerName` - String

Ejemplo:
```
PATCH /orders/PF6MflPDcuhWobZcgmJy5
Authorization: Bearer <YOUR TOKEN>

{
  "customerName": "John"
}
```

## Eliminar un pedido. ##
DELETE `/orders/:orderId`

Elimina un pedido existente. Requiere authentication.

El "request body" debe estar vacío.

Ejemplo:
```
DELETE /orders/PF6MflPDcuhWobZcgmJy5
Authorization: Bearer <YOUR TOKEN>
```

## API Authentication ##
Para realizar o ver un pedido, debemos registrar nuestra API client.

POST `/api-clients/`

El "request body" debe ser en formato JSON e incluir las siguientes propiedades:

- `clientName` - String
- `clientEmail` - String

Ejemplo:
```
{
   "clientName": "Postman",
   "clientEmail": "jalvariza@ejemplo.com"
}
```
La respuesta del "body" contiene el "access token". Este token es válido por 7 dias.

**Posibles errores:**

Status code 409 - "API client already registered." Posible solución sería cambiar los valores en "clientName" y "ClientEmail".
