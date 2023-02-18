# API Rest 

# Conhecendo o Fastify 

- É um micro framework do node assim como o express e são bem semelhantes 
trazem toda essa parte tradicional do node como lidar com rotas,  parametros
plugins, headers, requisições em JSON, essas coisas podem ser construidas 
na mão porém não vale a pena fazer do zero em todo projeto e é por isso 
que utilizamos libs como essas. 

## Motivos de escoher o Fastify

- É bem mais mantido que o Express , existem muito mais updates, equipe melhor dando manutenção.
- É uma das opções mais populares dentro do Node e sua API é extremamente semelhante a do Express
- Além de mais performático está mais pronto para lidar com novas funcionalidades do JavaScript
Como por exemplo o TypeScript no qual ele já possue uma integração direta.  
- Está mais pronto para trabalhar com assincronismo mais moderno como promises async await 
- Hoje é a melhor opção quando comparado com outros. 

## Criando o package.json
- Eu utilizo o comando npm init -y  para criar o package.json.

## Entendendo o TypeScript / Criando o Projeto 

- É um super Set que é um adicional ao JavaScript onde conseguimos trabalhar com 
tipagem estática.
- O Ts trás mais inteligência ao nosso código quando escrevemos a aplicação 
isso evita que alguns erros vão para produção.

- O node não entende TypeScript por padrão por isso é necessário converter o código 
para JavaScript. 

- Instalamos o TypeScript como dependencia de Desenvolvimento rodando o comando  
   npm i -D typescript  

- Depois de instalar o TypeScript é necessário criar um arquivo de configurações do 
TypeScript para isso eu vou utilizar o comando npx o npx serve para executar binários
ou seja códigos executáveis das bibliotecas que instalamos no projeto. eu executo o 
comando      npx tsc --init 

- Depois de rodar esse comando vai ser criado o arquivo tsconfig.json que tem 
vários comandos comuns de serem utilizados em aplicações TypeScript.

- Para converter um arquivo eu rodo o comando npx tsc src/nome_do_arquivo 

# Criando aplicação 

- Eu criei a pasta src e um arquivo chamado server.ts 
- Para instalar o Fastity rodar o comando     npm i fastify 
- Eu importei o fastify para dentro do meu arquivo server e em seguida crio uma const 
app chamando a função fastify() isso vai criar a base da aplicação. 

import fastify from "fastify";

const app = fastify()

- Com isso a partir do  app dá para fazer todas as funcionalidades simples que uma 
aplicação web tem principalmente a parte de rotas, a partir de app eu também tenho 
acesso a todos os metodos como GET PUT POST DELETE , vamos supor que temos a seguinte
rota localhost:333/hello  eu posso utilizar app passando a função get e no primeiro 
paramtro eu envio o recurso que no exemplo é /hello que é o que vem depois do endereço
o segundo parametro é uma função que devolve uma resposta. 

app.get('/hello', () => {
    return 'Hello World'
}) 

- Eu vou utilizar o app.listem() para fazer a aplicação ouvir uma porta. Eu passo 
para o listen um objeto passando a porta que quero ouvir. No final é necesário 
utilizar o .then() por que o listen retorna uma promese do JavaScript, quando essa 
promise termina de ser executada posso dar um log com HTTP Server Running.

app.listen({
    port: 3333,
}).then(() => {
    console.log('HTTP Server Running!')
})

## Executando o Código 

- É necessário converter o código de Ts para Js rodando o comando abaixo: 
    npx tsc src/server.ts  

- Note que ao rodar o comando vai ser criado o arquivo Js porém vai apontar 
uma série de erros no terminal isso acontece por que o node foi construido para
JavaScript e quando utilizamos o node com o TypeScript é necessário instalar também 
o pacote @types do node e para isso rode o comando abaixo: 
    npm install -D @types/node  

- Após isso quando for executado o comando npx a cima ele vai gerar o arquivo sem 
nenhum problema. 

- Em seguida para executar meu servior eu rodo o seguinte comando abaixo 
    node src/server.js

- Ao abrir meu navegador e acessar a rota vai está sendo executado. 

## Automatizando com o Tsx 

- existem formas de automatizar esse processo podemos instalar o tsx rodando 
o comando   npm install tsx -D 
- O Tsx faz o processo de converter o código TypeScript para JavaScript 
e executa o node no Js de forma automatizada.

- Executando o comando  npx tsx src/server.ts  ele já irá executar a aplicação. 

- Essa ferramenta só é recomendavel utilizar em ambiente de desenvolvimento e não 
em ambiente de produção. Em produção é melhor fazer da forma que foi feita 
anteriormente gerando o arquivo Js e executando ele. 

- Eu posso ir dentro do arquivo de package.json e dentro de scripts eu posso 
automatizar o tsx , posso criar o seguinte script:

  "scripts": {
    "dev": "tsx src/server.ts"
  },

- Com isso basta executar npm run dev para rodar a aplicação.
- Eu posso acrescentar o watch dentro do meu script para ele ficar monitorando 
e reiniciar de forma automatica toda vez que uma alteração for feita.

"scripts": {
    "dev": "tsx watch src/server.ts"
  },

  
# Estratégias de acesso ao banco 

## sqlite

- É um banco Sql, um banco relacional, esse tipo de banco de dados é cerca de 90% das 
aplicações, uma das vantegens de utilizar o sqlite é que não é necessário subir 
nenhum banco para a máquina, esse banco da para usar sem precisar instalar nada na 
máquina, todos os dados do sqlite são salvos em arquivos físicos que ficam dentro do 
projeto. 

- Boa parte das querys que forem serem escritas dentro do sqlite para fazer as buscas
dentro do banco de dados, é muito semelhante ao Mysql, postgress e qualquer outro 
banco relacional que utiliza Sql. Isso é interessante por que caso queira migrar 
para outro banco não será necessário fazer ateração no código pois esta escrito em sql

- Existem formas diferentes de se comunicar com banco de dados, as 3 formas mais 
comuns são: 

- Drivers Nativos --> São ferramentas, bibliotecas de baixo nível que permitem a 
a comunicação com o banco de uma maneira não abstrata ou seja ela tem que ser escrita
de forma bem crua ou seja é o nível mais baixo de se comunicar com banco de dados. 

- Query Builder ----> É uma forma de evitar ter que aprender muito Sql e poder focar
mais na linguagem que está sendo trabalhada, dentro do Node.js o mais famoso é o 
Knex.js, um Query Builder é um construtor de Query e ele facilita a escrita do 
código Sql com código JavaScript, ele mistura código Js com código do banco. Essa 
Sintaxe de código escrita com Query Builder pode ser aproveitada em qualquer banco 
que ele suporte.

- Orms --> É uma outra forma que utiliza menos ainda Sql. 







