**1. Criar o banco de dados com seu nome.**

`use jessica`

**2. Listar os banco de dados.**

```
> show dbs
admin    0.000GB
config   0.000GB
local    0.000GB
``` 

**3. Criar a collection produto no bd com seu nome.**

` db.createCollection('produto') `

**4. Listar os banco de dados.**
```
> show dbs
admin    0.000GB
config   0.000GB
jessica  0.000GB
local    0.000GB
test     0.000GB
```

**5. Listar as collections.**
```
> use jessica
switched to db jessica
> show collections
cliente
produto
```

**6. Inserir os seguintes documentos na collection produto:**
```
_id: 1, "nome": "cpu i5", "qtd": "15"
_id: 2, nome: "memória ram", qtd: 10, descricao: {armazenamento: "8GB", tipo:"DDR4"}
_id: 3, nome: "mouse", qtd: 50, descricao: {conexao: "USB", so: ["Windows", "Mac", "Linux"]}
_id: 4, nome: "hd externo", "qtd": 20, descricao: {conexao: "USB", armazenamento: "500GB", so: ["Windows 10", "Windows 8", "Windows 7"]}
``` 

```
db.produto.insertMany([{_id: 1, "nome": "cpu i5", "qtd": "15"}, {_id: 2, nome: "memória ram", qtd: 10, descricao: {armazenamento: "8GB", tipo:"DDR4"}}, {_id: 3, nome: "mouse", qtd: 50, descricao: {conexao: "USB", so: ["Windows", "Mac", "Linux"]}}, {_id: 4, nome: "hd externo", "qtd": 20, descricao: {conexao: "USB", armazenamento: "500GB", so: ["Windows 10", "Windows 8", "Windows 7"]}}])

```
**7. Mostrar todos os documentos.**
` db.produto.find({}).pretty() `