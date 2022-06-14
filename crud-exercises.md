**1. Criar a collection teste no banco de dados seu nome**
```
db.createCollection('teste')
{ "ok" : 1 }
```

**2. Inserir o seguinte documento:**
```
Campo: usuario, valor: Semantix
Campo: data_acesso, valor: data atual no formato ISODate

> db.teste.insertOne({usuario: 'Semantix',data_acesso: new Date()})
{
        "acknowledged" : true,
        "insertedId" : ObjectId("62a7f98b43d3ca32bcfc80f2")
}

``` 
**3. Buscar todos os documentos do ano >= 2020**
```
> db.teste.find({data_acesso: {$gte: new Date("2020")}})
{ "_id" : ObjectId("62a7f98b43d3ca32bcfc80f2"), "usuario" : "Semantix", "data_acesso" : ISODate("2022-06-14T02:59:23.911Z") }
```
**4. Atualizar o campo “data_acesso” para timestamp com o valor da atualização do usuario Semantix**
```
> db.teste.updateOne({usuario: "Semantix"}, {$currentDate: {data_acesso: {$type: "timestamp"}}})
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
```

**5. Buscar todos os documentos**
```
db.teste.find()
{ "_id" : ObjectId("62a7f93643d3ca32bcfc80f1"), "usuario" : "Semantix", "data_acesso" : Timestamp(1655175759, 1) }
```
**6. Deletar o documento criado pelo id**
```
> db.teste.deleteOne({"_id": ObjectId("62a7f98b43d3ca32bcfc80f2")})
{ "acknowledged" : true, "deletedCount" : 1 }
```

**7. Deletar a collection**
```
> db.teste.drop()
true
```