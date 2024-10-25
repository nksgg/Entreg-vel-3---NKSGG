# Exercício Express
Neste tutorial, vamos explorar como implementar uma requisição do tipo POST em uma aplicação Node.js utilizando o framework Express. O método POST é amplamente utilizado para enviar dados ao servidor, como informações de formulários ou dados em formato JSON. Para facilitar o teste da nossa implementação, utilizaremos o Postman, uma ferramenta popular para testar APIs. Ao final deste tutorial, você será capaz de criar uma rota que manipula requisições POST e entenderá como verificar a resposta do servidor. Vamos começar!
## 1º Passo: Criar um Novo Projeto
Para iniciar, vamos criar um novo projeto Node.js. Siga os passos abaixo:

1. Abra o terminal e navegue até o diretório onde deseja criar seu projeto.
2. Inicie um novo projeto executando o seguinte comando: `npm init -y`.
   
Esse comando cria um arquivo `package.json` com as configurações padrão.

3. Instale o Express como dependência do projeto: `npm install express`
4. **Crie um arquivo para a aplicação.** Vamos nomeá-lo como `app.js`.
5. Abra o arquivo `app.js` em seu editor de código preferido e adicione o seguinte código básico para configurar o servidor Express:

```javascript
const express = require('express'); // Importa o módulo express neste arquivo
const app = express(); // Iniciando o Express
const port = 3000;

app.get('/', function(req, res) {
  res.send('Oi, mundo :-)');
});

app.listen(port, function(erro) { // Cria a aplicação na porta 3000
    if (erro) {
      console.log("Erro ao Iniciar.");
    } else {
      console.log(`Servidor Iniciado. Acesse usando http://localhost:${port}`);  }
  });
```
**Não esqueça de salvar o arquivo.**

6. Teste a execução do servidor abrindo novamente o terminal e navegue até o diretório do seu projeto! Feito isso execute o comando a seguir para abrir o novo site criado. `node app.js` e abra o seu navegador na url `http://localhost:3000`.
7. Após a verificação feche seu servidor utiliznado `Ctrl + C`.

Agora você tem um projeto básico configurado com o Express! No próximo passo, vamos implementar uma biblioteca para tornar mais claro o entendimento dos dados enviados via POST.

## 2º Passo: Instalar a Biblioteca Body-Parser
Para facilitar a leitura dos dados enviados via POST, vamos instalar a biblioteca `body-parser`. Essa biblioteca ajuda a processar os dados do corpo da requisição de forma mais eficiente.

1. Instale o body-parser executando o seguinte comando no terminal: `npm install body-parser`
2. Após instalado, atualize o arquivo `app.js` da seguinte forma, acrescentando as seguintes linhas de código:
```javascript
const express = require('express'); // Importa o módulo express neste arquivo
const app = express(); // Iniciando o Express
var bodyParser = require('body-parser'); // Importa o body-parser
app.use(bodyParser.json());
const port = 3000;
```

Com o `body-parser` instalado e configurado, estamos prontos para implementar uma rota para a requisição POST.

## 3º Passo: Implementar a Rota para Requisição POST
Agora que você tem seu servidor Express configurado, vamos adicionar uma rota que responderá a uma requisição POST, utilizando uma função predefinida de soma. No seu arquivo `app.js`, adicione o seguinte código:
```javascript
app.post('/soma', function (req, res) {
  // Capturando o corpo da requisição
  var body = req.body;

  // Verificando se os números foram enviados
  if (body.num1 && body.num2) {
    // Convertendo para números e realizando a soma
    const resultado = Number(body.num1) + Number(body.num2);
    
    // Enviando a resposta com o resultado
    res.send(`Resultado da soma: ${resultado}`);
  } else {
    // Enviando uma mensagem de erro caso os números não sejam fornecidos
    res.status(400).send('Por favor, envie num1 e num2 no corpo da requisição.');
  }
});
```
### Explicação do Código da Rota POST:
Nesta explicação, vou detalhar cada parte do código para que você possa replicá-lo e compreendê-lo.
```javascript
app.post('/soma', function (req, res) {
  // Capturando o corpo da requisição
  var body = req.body;
```
1. Definição da Rota

    `app.post('/soma', ...)`: Estamos definindo uma rota que responde a requisições do tipo POST.

2. Capturando o Corpo da Requisição

    `var body = req.body;`: Aqui, estamos capturando o corpo da requisição.

   O `req.body` contém os dados que foram enviados pelo cliente. Por isso, precisamos ter o `body-parser` configurado para que os dados sejam processados corretamente. (Préviamente configurado no passo 2.)

```javascript
  // Verificando se os números foram enviados
  if (body.num1 && body.num2) ...
```
3. Validação dos Dados

    `if (body.num1 && body.num2)`: Estamos verificando se `num1` e `num2` estão presentes no corpo da requisição. Essa validação é crucial para garantir que temos os dados necessários para realizar a operação.

```javascript
    // Convertendo para números e realizando a soma
    const resultado = Number(body.num1) + Number(body.num2);
```
4. Conversão e Cálculo

   Utilizamos `Number(body.num1)` e `Number(body.num2)` para converter os valores recebidos em números. Isso é importante porque os dados recebidos do corpo da requisição são sempre tratados como strings, e precisamos garantir que estamos trabalhando com números para realizar a soma. A operação de soma é realizada e o resultado é armazenado na variável `resultado`.

```javascript
    // Enviando a resposta com o resultado
    res.send(`Resultado da soma: ${resultado}`);
```
5. Enviando a Resposta

    Após calcular o resultado, enviamos uma resposta ao cliente utilizando `res.send()`. 

```javascript
   else {
    // Enviando uma mensagem de erro caso os números não sejam fornecidos
    res.status(400).send('Por favor, envie num1 e num2 no corpo da requisição.');
  }
});
```

6. Tratamento de Erros

    `else { ... }`: Se a condição de validação falhar (ou seja, se num1 ou num2 não forem fornecidos), o código dentro deste bloco será executado.
   
    `res.status(400).send(...)`: Retornamos uma resposta de erro com status 400 (Bad Request) e uma mensagem clara que informa ao usuário que ele precisa enviar os números no corpo da requisição. Isso ajuda a identificar o que deu errado.

Com a rota POST implementada e explicada detalhadamente, agora você pode testar essa funcionalidade usando o Postman. Vamos para o próximo passo!

## 4º Passo: Testar a Rota POST via Postman
Agora, vamos descobrir quem é o Postman. Veja o vídeo a seguir e siga os passos para executar o seu teste.

Terminou? Repita os passos para outras três operações matemáticas, boa sorte ;-).
