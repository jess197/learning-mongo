**1. Crie a collection cursos no banco de dados escola**
db.createCollection('cursos')

**2. Importe o arquivo “data-load\cursos.csv” para a collection cursos, com os seguintes atributos:**

I used NoSQLBooster

```
id_curso: Number
id_unidade: Number
nome: String
nivel: String
Arquivos do Dataset
``` 
```
import into "escola.cursos" start...
import into "escola.cursos" 100%, 231 docs inserted.
import into "escola.cursos" finished.

A total of 231 document(s) have been imported into 1 collection(s).
{
  "cursos": {
    "nInserted": 231,
    "nModified": 0,
    "nSkipped": 0,
    "failed": 0
  }
}
```

**3. Realizar o left outer join da collection alunos e cursos, quando o id_curso dos 2 forem o mesmo.**

```
db.alunos.aggregate({$lookup: {
       from: "cursos",
       localField: "id_curso",
       foreignField: "id_curso",
       as: "curso"
     }})
```

**4. Realizar o left outer join da collection alunos e cursos, quando o id_curso dos 2 forem o mesmo e visualizar apenas os seguintes campos**
```
Alunos: id_discente, nivel, nome
Cursos: id_curso, id_unidade, nome
```

```
db.alunos.aggregate([
    {$lookup: {
       from: "cursos",
       localField: "id_curso",
       foreignField: "id_curso",
       as: "alunos_cursos"
     },
     { $project: {"_id":0,"id_discente":1, "nivel":1, "nome":1, "alunos_cursos.id_curso":1,"alunos_cursos.id_unidade":1, "alunos_cursos.nome":1 }
     }
     ])
```