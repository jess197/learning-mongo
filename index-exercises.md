**1. Mostrar todos os documentos da collection produto do banco de dados seu nome**

```
> db.produto.find({})
{ "_id" : 1, "nome" : "cpu i7", "qtd" : 15 }
{ "_id" : 2, "nome" : "memória ram", "qtd" : 10, "descricao" : { "armazenamento" : "8GB", "tipo" : "DDR4" } }
{ "_id" : 3, "nome" : "mouse", "qtd" : "30", "descricao" : { "conexao" : "USB 3.0", "sistema" : [ "Windows 10", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z"), "ts_modificado" : Timestamp(1655174378, 1) }
{ "_id" : 4, "nome" : "hd externo", "qtd" : 20, "descricao" : { "conexao" : "USB 3.0", "armazenamento" : "500GB", "sistema" : [ "Windows 10", "Windows 8", "Windows 7", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z") }
```

**2. Criar o index “query_produto” para pesquisar o campo nome do produto em ordem alfabética**

```
> db.produto.createIndex({nome: 1},{name: "query_produto"})
{
        "numIndexesBefore" : 1,
        "numIndexesAfter" : 2,
        "createdCollectionAutomatically" : false,
        "ok" : 1
}

```

**3. Pesquisar todos os índices da collection produto**

```
> db.produto.getIndexes()
[
        {
                "v" : 2,
                "key" : {
                        "_id" : 1
                },
                "name" : "_id_"
        },
        {
                "v" : 2,
                "key" : {
                        "nome" : 1
                },
                "name" : "query_produto"
        }
]


```

**4. Pesquisar todos os documentos da collection produto**

```
> db.produto.find({})
{ "_id" : 1, "nome" : "cpu i7", "qtd" : 15 }
{ "_id" : 2, "nome" : "memória ram", "qtd" : 10, "descricao" : { "armazenamento" : "8GB", "tipo" : "DDR4" } }
{ "_id" : 3, "nome" : "mouse", "qtd" : "30", "descricao" : { "conexao" : "USB 3.0", "sistema" : [ "Windows 10", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z"), "ts_modificado" : Timestamp(1655174378, 1) }
{ "_id" : 4, "nome" : "hd externo", "qtd" : 20, "descricao" : { "conexao" : "USB 3.0", "armazenamento" : "500GB", "sistema" : [ "Windows 10", "Windows 8", "Windows 7", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z") }


```

**5. Visualizar o plano de execução do exercício 4**
```
"queryPlanner" : {
                "namespace" : "jessica.produto",
                "indexFilterSet" : false,
                "winningPlan" : {
                        "stage" : "COLLSCAN",
                        "direction" : "forward"
                }, 

```

**6. Pesquisar todos os documentos da collection produto, com uso da index “query_produto”**

```
> db.produto.find().hint({nome: 1})
{ "_id" : 1, "nome" : "cpu i7", "qtd" : 15 }
{ "_id" : 4, "nome" : "hd externo", "qtd" : 20, "descricao" : { "conexao" : "USB 3.0", "armazenamento" : "500GB", "sistema" : [ "Windows 10", "Windows 8", "Windows 7", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z") }
{ "_id" : 2, "nome" : "memória ram", "qtd" : 10, "descricao" : { "armazenamento" : "8GB", "tipo" : "DDR4" } }
{ "_id" : 3, "nome" : "mouse", "qtd" : "30", "descricao" : { "conexao" : "USB 3.0", "sistema" : [ "Windows 10", "Linux" ] }, "data_modificacao" : ISODate("2022-06-14T02:32:22.370Z"), "ts_modificado" : Timestamp(1655174378, 1) }

```

**7. Visualizar o plano de execução do exercício 7**

```
> db.produto.find().hint({nome: 1}).explain()
{
        "explainVersion" : "1",
        "queryPlanner" : {
                "namespace" : "jessica.produto",
                "indexFilterSet" : false,
                "parsedQuery" : {

                },
                "winningPlan" : {
                        "stage" : "FETCH",
                        "inputStage" : {
                                "stage" : "IXSCAN",
                                "keyPattern" : {
                                        "nome" : 1
                                },
                                "indexName" : "query_produto",
                                "isMultiKey" : false,
                                "multiKeyPaths" : {
                                        "nome" : [ ]
                                },
                                "isUnique" : false,
                                "isSparse" : false,
                                "isPartial" : false,
                                "indexVersion" : 2,
                                "direction" : "forward",
                                "indexBounds" : {
                                        "nome" : [
                                                "[MinKey, MaxKey]"
                                        ]
                                }
                        }
                },
                "rejectedPlans" : [ ]
        },
        "ok" : 1
}

```


**8. Remover o index “query_produto”**

```
> db.produto.dropIndex({nome: 1})
{ "nIndexesWas" : 2, "ok" : 1 }
```

**9. Pesquisar todos os índices da collection produto**

```
> db.produto.getIndexes()
[ { "v" : 2, "key" : { "_id" : 1 }, "name" : "_id_" } ]
```