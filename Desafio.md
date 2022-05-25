# MongoDB

1. Agregar 10 documentos con valores distintos a las colecciones mensajes y productos. El formato de los documentos debe estar en correspondencia con el que venimos utilizando en el entregable con base de datos MariaDB. 

### Mensajes

```javascript
    db.mensajes.insertMany([
    {
        name: "Juan",
        message: "Hola, ¿como estan?"
    },
    {
        name: "carlos",
        message: "Estamos bien"
    },
    {
        name: "Pedro",
        message: "Estamo todos"
    },
    {
        name: "Lucas",
        message: "Vamos a ir al cine?"
    },
    {
        name: "Mateo",
        message: "tal vez"
    },
    {
        name: "Julia",
        message: "Hola a todos"
    },
    {
        name: "Valeria",
        message: "Mensaje"
    },
    {
        name: "Alba",
        message: "Tengo que ir a un lugar"
    },
    {
        name: "Lucas",
        message: "Vamos a ir al cine?"
    },
    {
        name: "Emma",
        message: "No voy a poder ir"
    }
]);
```

2. Definir las claves de los documentos en relación a los campos de las tablas de esa base. En el caso de los productos, poner valores al campo precio entre los 100 y 5000 pesos(eligiendo valores intermedios, ej: 120, 580, 900, 1280, 1700, 2300, 2860, 3350, 4320, 4990). 

### Productos
```javascript
db.productos.insertMany([
    {
        name: "Disco Rigido",
        price: 120,
        image: "imagen-01"
    },
    {
        name: "Placa de video",
        price: 580,
        image: "image-02"
    },
    {
        name: "Prcesador",
        price: 900,
        image: "image-03"
    },
    {
        name: "Audiculares",
        price: 1280,
        imagen: "imagen-04"
    },
    {
        name: "Memoria Ram",
        price: 1700,
        imagen: "imagen-05"
    },
    {
        name: "Monitor",
        price: 2300,
        imagen: "imagen-06"
    },
    {
        name: "SSD",
        price: 2860,
        imagen: "imagen-07"
    },
    {
        name: "Placa madre",
        price: 3000,
        imagen: "imagen-07"
    },
    {
        name: "Mouse",
        price: 3300,
        image: "imagen-08"
    },
    {
        name: "Teclado",
        price: 4200,
        imagen: "imagen-09"
    },
    {
        name: "Silla Gamer",
        price: 5000,
        imagen: "imagen-10"
    }
]);
```
3. Listar todos los documentos en cada colección.

```javascript
    show collections;
```

 4. Mostrar la cantidad de documentos almacenados en cada una de ellas.
 
 ```javascript
    db.mensajes.find()
    db.productos.find()
 ```
5. Realizar un CRUD sobre la colección de productos: 
    * a) Agregar un producto más en la colección de productos
    * b) Realizar una consulta por nombre de producto específico:
        * i)    Listar los productos con precio menor a 1000 pesos.
        * ii)   Listar los productos con precio entre los 1000 a 3000 pesos.
        * iii)  Listar los productos con precio mayor a 3000 pesos.
        * iv)   Realizar una consulta que traiga sólo el nombre del tercer producto más barato.
    * c) Hacer una actualización sobre todos los productos, agregando el campo stock a todos ellos con un valor de 100.
    * d) Cambiar el stock a cero de los productos con precios mayores a 4000 pesos. 
    * e) Borrar los productos con precio menor a 1000 pesos 

5-a. 
```javascript
    db.productos.insertOne(
        {
            name: "Agregando un producto", 
            price: 6000, image: 
            "imagen-11"
        }
    )
```

* 5-b
    * i
    ```javascript
        db.productos.find({price: {$lt: 1000}})
    ```
    * ii
    ```javascript
        db.productos.find({price: {$gte: 1000, $lte: 3000}})
    ```
    * iii
    ```javascript
        db.productos.find({price: {$lte: 3000}})
    ```
    * iv
    ```javascript
        db.productos.find({}).sort({price: 1}).skip(2).limit(1)
    ```
5-c. 
```javascript
    db.productos.updateMany({}, {$set:{stock: 100}})
```
5-d.
```javascript
    db.productos.updateMany({ $and: [{"stock": 100}, {"price": {$gte: 4000}}]}, {$set:{stock: 0}})
```
5-e.
```javascript
    db.productos.deleteMany({price: {$lt: 1000}})
```