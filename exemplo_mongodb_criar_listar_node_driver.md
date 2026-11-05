# Inserir e listar a partir do Node.js

## Código de referência

```js
// Importação do MongoClient
import { MongoClient } from 'mongodb';

// Criação do objeto client
const client = new MongoClient('mongodb://localhost:27017');

// Realiza a conexão com o servidor;
await client.connect();

// Seleciona o banco desejado;
const db = client.db('api_express');

// Seleciona a coleção desejada;
const colecao = db.collection('tarefas');

// O mesmo que: db.tarefas.insertOne({ titulo: "Estudar Node", concluida: false })
// Comando para inserir um documento dentro da coleção 'tarefas'
const resultado = await colecao.insertOne({ titulo: 'Estudar Node', concluida: false });
console.log('Inserido com _id:', resultado.insertedId);

// O mesmo que: db.tarefas.find()
// Comando para listar todas as tarefas
const todas = await colecao.find().toArray();
console.log(todas);

// Encerra a conexão com o banco
await client.close();
```

Pontos de atenção:

- `insertOne` devolve `insertedId`, não o documento inteiro.
- `find()` devolve um **cursor**. `toArray()` transforma o cursor em array. Sem `toArray()`, nada é buscado de fato.
- `insertOne` e `find` retornam **Promises**: use `await`.
