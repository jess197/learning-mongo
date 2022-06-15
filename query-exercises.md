**1. Mostrar todos os documentos da collection produto**

**2. Pesquisar na collection produto, os documentos com os seguintes atributos:**

**a) Nome = mouse**
```  db.produto.find({nome: 'mouse'}).pretty()
{
        "_id" : 3,
        "nome" : "mouse",
        "qtd" : "30",
        "descricao" : {
                "conexao" : "USB 3.0",
                "sistema" : [
                        "Windows 10",
                        "Linux"
                ]
        },
        "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z"),
        "ts_modificado" : Timestamp(1655174378, 1)
} 
``` 

**b) Quantidade = 20 e apresentar apenas o campo nome**
```
> db.produto.find({qtd: {$eq:20}},{nome: 1}).pretty()
{ "_id" : 4, "nome" : "hd externo" }
```

**c) Quantidade <= 20 e apresentar apenas os campos nome e qtd**
```
> db.produto.find({qtd: {$lte:20}},{nome: 1},{qtd:1}).pretty()
{ "_id" : 1, "nome" : "cpu i7" }
{ "_id" : 2, "nome" : "memória ram" }
{ "_id" : 4, "nome" : "hd externo" }

```

**d) Quantidade entre 10 e 20**
`db.produto.find({qtd: {$gte: 10, $lte: 20}})`

**e) Conexão = USB e não apresentar o campo _id e qtd**
` db.produto.find({conexao: {$eq: 'USB'},{_id: 0}, {qtd: 0}})`

**f) SO que contenha “Windows” ou “Windows 10”**
`db.produto.find({'descricao.so:' {$in ["Windows","Windows 10"]}})` 