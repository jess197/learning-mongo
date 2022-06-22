**1. Crie o banco de dados escola**

```
show dbs
use escola
```
**2. Crie a collection alunos no banco de dados escola**

`db.createCollection('alunos')`

**3. Importe o arquivo “data-load/alunos.csv” para a collection alunos, com os seguintes atributos:**

```
id_discente: Number
nome: String
ano_ingresso: Number
nivel: String
id_curso: Number
Arquivos para Dataset
```

**4. Visualizar os valores únicos do “nivel” de cada “ano_ingresso”**

`db.alunos.aggregate({$group: { _id: "$ano_ingresso", nivel_por_ano: {$addToSet: "$nivel"}}}) `

**5. Calcular a quantidade de alunos matriculados por cada “id_curso”**

`db.alunos.aggregate({$group: { _id: "$id_curso", qtd_curso: {$sum: 1}}})` 

**6. Calcular a quantidade de alunos matriculados por “ano_ingresso” no "id_curso“: 1222**

`db.alunos.aggregate([{$match: {'id_curso': 1222}},{$group: { _id: "$ano_ingresso", qtd_curso: {$sum: 1}}}])` 

**7. Visualizar todos os documentos do “nível”: “M”**

`db.alunos.aggregate({$match: {'nivel':'M'}})` 

**8. Visualizar o último ano que teve cada curso (id_curso) dos níveis “M”**

`db.alunos.aggregate([{$match: {'nivel':'M'}}, {$group: {_id: '$id_curso', lastyear_course: {$max: "$ano_ingresso"}}}])` 

**9. Visualizar o último ano que teve cada curso (id_curso) dos níveis “M”, ordenados pelos anos mais novos de cada curso**

`db.alunos.aggregate([{$match: {'nivel':'M'}}, {$group: {_id: '$id_curso', lastyear_course: {$max: "$ano_ingresso"}}}, {$sort: {lastyear_course: -1}}])` 

**10. Visualizar o último ano que teve os 5 últimos cursos (id_curso) dos níveis “M”, ordenados pelos anos mais novos**

`db.alunos.aggregate([{$match: {'nivel':'M'}}, {$group: {_id: '$id_curso', lastyear_course: {$max: "$ano_ingresso"}}}, {$sort: {lastyear_course: -1}}, {$limit: 5}])` 