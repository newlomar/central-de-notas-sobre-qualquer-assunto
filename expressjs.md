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

<br>

## Nodemon

Utilizado para ficar verificando alterações no servidor em momento de desenvolvimento e não precisar ficar derrubando e subindo o servidor sempre que mudar algo no código (o Nodemon faz isso por você).

Para instá-lo:

````bash
npm install nodemon --save-dev
```
````

<br>

## req.params, req.query, req.body

Query Params => seguem o modelo de "chave=valor", por exemplo: campanha=facebook

Params => ficam no final da rota, por exemplo: /api/v1/users/123

Body => corpo da requisição

Consumindo req.params:

```js
app.get("/testes/:idUsuarios", (req, res) => {
  console.log(req.params);
  res.send("Oi");
});
```

Para usar parâmetro opcionais, colocar interrogação no final do parâmetro, possibilitando, assim, usar a rota /testes também.

```js
app.get("/testes/:idUsuarios?", (req, res) => {
  console.log(req.params);
  if (req.params.idUsuarios) {
    res.send(req.params.idUsuarios);
  }
  res.send("Sem parâmetros");
});
```

Além disso, é possível seguir com parâmetros opcionais ou obrigatórios o quanto for necessário, porém a adição de paramêtros obrigatórios após opcionais gera comportamento estranhos (testar removendo a última interrogação do endpoint abaixo.):

```js
app.get("/testes/:idUsuarios?/:parametro?", (req, res) => {
  console.log(req.params);
  res.send(req.params);
});
```

Trabalhando com query strings:

- Exemplo de utilização: http://localhost.com:3000/??nome=Newton&sobrenome=Lomar

```js
app.get("/testes/:idUsuarios?/:parametro?", (req, res) => {
  console.log(req.query);
  res.send(req.query);
});
```

Trabalhando com req.body:

Em primeiro lugar, habilitar o middlewre urlencoded com extended=true:

```js
app.use(
  express.urlencoded({
    extended: true,
  })
);
```

E a rota fica assim:

```js
app.post("/form", (req, res) => {
  console.log(req.body);
  res.send(req.body.nome);
});
```

<br>

## Routers and Controllers

Consiste em um padrão de organização de código, onde as rotas e os controllers ficam em arquivos diferentes, respeitando o princípio da separação de responsabilidades.

<br>

# Views

Usado para ter a parte visual da aplicação no modelo MVC full (todos arquivos dentro da mesma aplicação).

Deve se usar um middleware apontando para o caminho da pasta cujo as views estão armazenadas. Opcionalmente, pode-se usar a biblioteca path para passar caminhos absolutos.

Além disso, vamos usar uma "engine" para dar super poderes ao nosso HTML. O ejs, engine que vamos utilizar, permite que a gente utilize for loops e condicionais no HTML.

É necessários instalar essa engine com:

```bash
npm i ejs
```

```js
const path = require("path");

app.set("views", path.resolve(__dirname, "src", "views"));
app.set("view engine", "ejs");
```

Agora, nos nosso arquivos HTML dentro da pasta views, vamos utilizar a extensão ".ejs". Por exemplo: index.ejs

<br>

# Arquivos estáticos

Utilizado para fornecimento de arquivos estáticos, como arquivos html, css e imagens.

Pode ser possível pelo meio do middleware:

```js
app.use(express.static("./public"));
```
