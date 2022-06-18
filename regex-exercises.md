**1. Mostrar todos os documentos da collection produto do banco de dados seu nome**
```
db.produto.find({})
{ "_id" : 1, "nome" : "cpu i7", "qtd" : 15 }
{ "_id" : 2, "nome" : "memória ram", "qtd" : 10, "descricao" : { "armazenamento" : "8GB", "tipo" : "DDR4" } }
{ "_id" : 3, "nome" : "mouse", "qtd" : "30", "descricao" : { "conexao" : "USB 3.0", "sistema" : [ "Windows 10", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z"), "ts_modificado" : Timestamp(1655174378, 1) }
{ "_id" : 4, "nome" : "hd externo", "qtd" : 20, "descricao" : { "conexao" : "USB 3.0", "armazenamento" : "500GB", "sistema" : [ "Windows 10", "Windows 8", "Windows 7", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z") }
```

**2. Buscar os documentos com o atributo nome,  que contenham a palavra “cpu”**
```
> db.produto.find({nome: {$regex: /cpu/i}})
{ "_id" : 1, "nome" : "cpu i7", "qtd" : 15 }
```

**3. Buscar os documentos com o atributo nome, que começam por “hd” e apresentar os campos nome e qtd**

```
> db.produto.find({nome: {$regex: "^hd"}},{nome:1,qtd:1,_id:0})
{ "nome" : "hd externo", "qtd" : 20 }
```

**4. Buscar os documentos com o atributo descricao.armazenamento, que terminam com “GB” ou “gb” e apresentar os campos nome e descricao**
```
> db.produto.find({"descricao.armazenamento": {$regex: /gb$/i}},{nome:1,"descricao":1,_id:0})
{ "nome" : "memória ram", "descricao" : { "armazenamento" : "8GB", "tipo" : "DDR4" } }
{ "nome" : "hd externo", "descricao" : { "conexao" : "USB 3.0", "armazenamento" : "500GB", "sistema" : [ "Windows 10", "Windows 8", "Windows 7", "Linux" ] } }
```

**5. Buscar os documentos com o atributo nome, que contenha a palavra memória, ignorando a letra “o”**
```
> db.produto.find({nome: {$regex: /mem.ria/i}})
{ "_id" : 2, "nome" : "memória ram", "qtd" : 10, "descricao" : { "armazenamento" : "8GB", "tipo" : "DDR4" } }
```

**6. Buscar os documentos com o atributo qtd que contenham valores com letras, ao invés de números.**
```
> db.produto.find({qtd: {$regex: /[a-z]/i}})
> 
```

**7. Buscar os documentos com o atributo descricao.sistema, que tenha exatamente a palavra “Windows”**
```
> db.produto.find({"descricao.sistema": {$regex: /^Windows/}})
{ "_id" : 3, "nome" : "mouse", "qtd" : "30", "descricao" : { "conexao" : "USB 3.0", "sistema" : [ "Windows 10", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z"), "ts_modificado" : Timestamp(1655174378, 1) }
{ "_id" : 4, "nome" : "hd externo", "qtd" : 20, "descricao" : { "conexao" : "USB 3.0", "armazenamento" : "500GB", "sistema" : [ "Windows 10", "Windows 8", "Windows 7", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z") }
```