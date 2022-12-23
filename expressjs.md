# ExpressJS

Criado para facilitar a criação de servidores web com NodeJs.

Substitui o módulo HTTP de criação de servidor nativo do node.

O Express facilita nossa vida.

Para instalá-lo:

```bash
npm install express
```

Para ter acesso ao framework:

```js
const express = require("express");
const app = express();
```

Acessar um site, por exemplo, https://meusite.com/ é equivalente a enviar uma requisição GET ao servidor na rota "/" (barra).

O servidor, que no caso é gerenciado pelo express, é responsável por saber o que entregar ao cliente quando ele solicitar a rota /

O código mais simples possível para rodar um servidor com express:

```js
const express = require("express");
const app = express();

app.get("/", (req, res) => {
  res.send("Hello world!");
});

app.listen(3000);
```

Um pouco mais elaborado:

```js
const express = require("express");
const app = express();

app.get("/", (req, res) => {
  res.send("Hello world!");
});

app.get("/form", (req, res) => {
  res.send(`
  <form action="/form" method="POST">
    Nome: <input type="text" name="nome">
    <button>Enviar</button>
    </form>
  `);
});

app.post("/form", (req, res) => {
  res.send("Recebi o formulário!");
});

app.get("/contato", (req, res) => {
  res.send("Obrigado por entrar em contato com a gente.");
});

app.listen(3000, () => {
  console.log("Servidor executando na porta 3000");
  console.log("Acessar http://localhost:3000");
});
```
