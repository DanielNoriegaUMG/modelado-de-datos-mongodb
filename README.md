# MongoDB

## Relaciones embedidas o referenciadas?

Es dependiendo de la necesidad, por ejemplo si tu consulta se se quiere hacer en conjunto, se recomienda una **EMBEBIDA** esto quiere decir que se encuentre un subdocumento dentro de nuestro documento por ejempplo:

```js
db.products.insertOne({
    name: "PS5",
    description: "Consola de videojuegos de Sony",
    image: "https://ps.com"
    category: {
        name: "Home",
        image: "https//:home.com"
    }
});
```

ahora si tu consulta es por partes, se recomienda hacerla por partes, **REFERENCIADA**, por ejemplo:

```js
db.customers.insertOne({
    _id: ObjectId,
    name: string
    last_name: string
});

db.order.insertOne({
    _id: ObjectId
    date: Date,
    customer_id: Object_id
});
```

En el 90% de los casos, cuando es una relacion 1:1 suele ser una consulta **EMBEBIDA**, pero uno de los casos donde se usa la relacion **REFERENCIADA**, es cuando el documento ya es muy grande, cerca del limite de 16 mb y ejor se saca informacion para mejorar el rendimiento. También se pueden usar combinados, si usas el ObjectId, para referenciar el total de datos y agregar los 2 o 3 campos de los más comunes que se usan juntas para evitar la consulta a la segunda colección.