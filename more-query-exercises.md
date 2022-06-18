**1. Mostrar todos os documentos da collection produto**
```
> db.produto.find({})
{ "_id" : 1, "nome" : "cpu i7", "qtd" : 15 }
{ "_id" : 2, "nome" : "memória ram", "qtd" : 10, "descricao" : { "armazenamento" : "8GB", "tipo" : "DDR4" } }
{ "_id" : 3, "nome" : "mouse", "qtd" : "30", "descricao" : { "conexao" : "USB 3.0", "sistema" : [ "Windows 10", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z"), "ts_modificado" : Timestamp(1655174378, 1) }
{ "_id" : 4, "nome" : "hd externo", "qtd" : 20, "descricao" : { "conexao" : "USB 3.0", "armazenamento" : "500GB", "sistema" : [ "Windows 10", "Windows 8", "Windows 7", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z") }

```
**2. Realizar as seguintes pesquisas na collection produto:**

**a) Mostrar os documentos ordenados pelo nome em ordem alfabética.**

```
> db.produto.find({}).sort({nome: 1})
{ "_id" : 1, "nome" : "cpu i7", "qtd" : 15 }
{ "_id" : 4, "nome" : "hd externo", "qtd" : 20, "descricao" : { "conexao" : "USB 3.0", "armazenamento" : "500GB", "sistema" : [ "Windows 10", "Windows 8", "Windows 7", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z") }
{ "_id" : 2, "nome" : "memória ram", "qtd" : 10, "descricao" : { "armazenamento" : "8GB", "tipo" : "DDR4" } }
{ "_id" : 3, "nome" : "mouse", "qtd" : "30", "descricao" : { "conexao" : "USB 3.0", "sistema" : [ "Windows 10", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z"), "ts_modificado" : Timestamp(1655174378, 1) }
 
```

**b) Mostrar os 3 primeiros documentos ordenados por nome e quantidade.**

```
> db.produto.find({}).sort({nome: 1, qtd: 1}).limit(3)
{ "_id" : 1, "nome" : "cpu i7", "qtd" : 15 }
{ "_id" : 4, "nome" : "hd externo", "qtd" : 20, "descricao" : { "conexao" : "USB 3.0", "armazenamento" : "500GB", "sistema" : [ "Windows 10", "Windows 8", "Windows 7", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z") }
{ "_id" : 2, "nome" : "memória ram", "qtd" : 10, "descricao" : { "armazenamento" : "8GB", "tipo" : "DDR4" } }

```

**c) Mostrar apenas 1 documento que tenha o atributo Conexão = USB.**

```
> db.produto.find({"descricao.conexao": /USB/}).limit(3)
{ "_id" : 3, "nome" : "mouse", "qtd" : "30", "descricao" : { "conexao" : "USB 3.0", "sistema" : [ "Windows 10", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z"), "ts_modificado" : Timestamp(1655174378, 1) }
{ "_id" : 4, "nome" : "hd externo", "qtd" : 20, "descricao" : { "conexao" : "USB 3.0", "armazenamento" : "500GB", "sistema" : [ "Windows 10", "Windows 8", "Windows 7", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z") }

```

**d) Mostrar os documentos de tenham o atributo conexão = USB e quantidade menor que 25.**

```
> db.produto.find({"descricao.conexao": /USB/,qtd: {$lt: 25}})
{ "_id" : 4, "nome" : "hd externo", "qtd" : 20, "descricao" : { "conexao" : "USB 3.0", "armazenamento" : "500GB", "sistema" : [ "Windows 10", "Windows 8", "Windows 7", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z") }

```

**e) Mostrar os documentos de tenham o atributo conexão = USB ou quantidade menor que 25.**

```
> db.produto.find({$or: [{"descricao.conexao": /USB/}, {qtd: {$lt:25}}]})
{ "_id" : 1, "nome" : "cpu i7", "qtd" : 15 }
{ "_id" : 2, "nome" : "memória ram", "qtd" : 10, "descricao" : { "armazenamento" : "8GB", "tipo" : "DDR4" } }
{ "_id" : 3, "nome" : "mouse", "qtd" : "30", "descricao" : { "conexao" : "USB 3.0", "sistema" : [ "Windows 10", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z"), "ts_modificado" : Timestamp(1655174378, 1) }
{ "_id" : 4, "nome" : "hd externo", "qtd" : 20, "descricao" : { "conexao" : "USB 3.0", "armazenamento" : "500GB", "sistema" : [ "Windows 10", "Windows 8", "Windows 7", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z") }

```

**f) Mostrar apenas os id dos documentos de tenham o atributo conexão = USB ou quantidade menor que 25.**
```
> db.produto.find({$or: [{"descricao.conexao": /USB/}, {qtd: {$lt:25}}]},{_id:1})
{ "_id" : 1 }
{ "_id" : 2 }
{ "_id" : 3 }
{ "_id" : 4 }
```