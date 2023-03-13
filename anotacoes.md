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

# Configurando o Knex 

- podemos acessar a documentação do Knex.js   https://knexjs.org  

- Temos o comando para fazer a instalação rode o comando abaixo: 
        npm install knex --save  

- Além do knex tesmo algumas opções de drivers dos bancos de dados que queremos 
como vamos utilizar o sqlite vamos instalar o sqlite3 
        npm install sqlite3   

- posso resumir tudo com o comando:  npm instal knex sqlite3   

- O proximo passo é criar dentro da pasta src um aqruivo para a minha base de dados 
database.ts é nesse arquivo que fazemos a conexão com o banco de dados. 

- Eu importo a função knex do proprio knex , eu crio uma constante na qual chamei de 
knex para chamar minha constante assim eu preciso renomear a importação pois tem 
também o nome de knex, dentro dessa função eu passo algumas informações obrigatórias 
como client que é qual banco de dados vou utilizar, outra opção obrigatória é a 
connection essa propriedade precisa ter informaçoes sobre a nossa conexão 
informações como host, port, user, senha e o nome do banco de dados. Cada banco vai
ter uma exigencia especifica para connection o sqlite mesmo só exige o filename que 
é o nome do arquivo onde o banco de dados será salvo.

- Vou criar uma pasta chamada tmp e dentro dela vou criar meu arquivo app.db, tmp é 
temporario por que a idéia de utilizar o arquivo app.db é só em ambiente de 
desenvolvimento, não será utilizado em produção.

import { knex as setupKnex } from "knex";

export const knex = setupKnex({
    client: 'sqlite',
    connection: {
        filename: './tmp/app.db',
    },
})

- Para testar se o banco de dados está funcionando eu vou dentro de server e dentro da
minha rota get, vou transformar ela em uma async e cou criar uma constante tables na 
quando vou escrever uma query, como ainda não temos uma tabela vamos utilizar uma 
tabela universal que tem em todos os bancos de dados sqlite que é a sqlite_schema 
eu vou dá um select * para buscar todos os dados dessa tabela e testar se meu banco 
está funcionando. 

app.get('/hello', async () => {
    const tables = await knex('sqlite_schema').select('*')

    return tables 
}) 

## Git ignore

- Quando se utiliza versionamento com git é legal criar um arquivo chamado 
.gitignore e posso passar arquivos que serão ignorados na hora de subir o código 
para o repositório.

# Criando a primeira migration 

- Agora é necessário criar as tabelas do banco de dados, colunas, chaves primárias, 
chaves estrangeiras, relacionamentos e outras configurações dentro do banco de dados.

## Migrations 

- É um controle de versão dentro do banco de dados, as migrations é um histórico de 
todas as mudanças que foram feitas dentro do banco de dados, essas mudanças são 
registradas sempre com a data e o horario em que foram criadas, da para criar toda 
uma linha do tempo de como o banco de dados mudou ao longo do tempo. 

- Com as Migrations temos uma tabela criada com ela de forma automatica, chamada 
migrations onde o banco de dados registra nessa tabela quais itens do histórico do
banco de dados ele já teve. 

- Para utilizar é necessário fazer algumas configurações dentro do package.json 
por padrão o Knex foi desenvolvido para executar com Js e não com Ts , dentro da
pasta node_modulesn na pasta .bin tem um arquivo chamado knex que é uma cli do knex 
dá para criar e executar algumas coisas. 

- Quando se executa npx knex -h ele vai mostrar uma série de comando do knex varios 
desses comandos iniciam com migrate e o migrate:make serve para criar a migrate.

- Eu utilizo o comando npx knex migrate:make nome-da-tabela geralmenete o nome da 
migration tem que simbolizar qual alteração queremos que sejam feitas no banco de 
dados. 

- Se apenas todar esse comando dessa forma vai retornar um erro por que o knex 
precisa saber as inoformações do banco de dados que está sendo utilizado, para 
que isso seja feito existe uma convenção de criar um arquivo na raiz do projeto
chamado knexfile.ts  dentro desse arquivo eu apenas importo as configurações do meu 
banco que estão em database. 
Como eu apenas quero passar as configurações eu separo ela em uma variavel isolada 
chamada config.

export const config = {
    client: 'sqlite',
    connection: {
        filename: './tmp/app.db',
    },
    useNullAsDefault: true,
}

export const knex = setupKnex(config)

- Dentro do arquivo knexfile eu impoto apenas a config e exporto elas como 
padrão. 

import { config } from "./src/database"

export default config

- Se rodar novamente o comando para cria a migration ele vai gerar novamente um erro
porém de typeScript que é necessário instalar algumas bibliotecas para o knex. 

- Dentro do pachage.json euvou criar um script para o node utilizar o tsx para 
o knex. Por isso nesse script eu tbm indico o caminho do arquivo knex.

"knex": "node --no-warnings --loader tsx ./node_modules/knex/bin/cli.js"

- Executando o comando npm run knex -- -h  e ele vai trazer novamente todos os 
comandos em seguida eu voi rodar o comando abaixo para criar a migration

- Agora vou criar a migrate com o seguinte comando abaixo: 
    npm run knex -- migrate:make create-nome-da-migrate 

- Após rodar o comando a cima ele vai criar automaticamete uma pasta chamada 
migrations e dentro um arquivo TypeScript pode podemos escrever toda a parte de 
criação da tabela. Note que ele vai criar o arquivo na raiz do projeto e podemos 
mudar essa localização, dentro do arquivo de database podemos configurar algumas
coisas especificas para migrations, antes eu importo de dentro do knex o Knex só 
que com o K maiúsculo esse Knex que estamos importando é uma interface, eu devo 
passar que nossa config deve passar Knex.Config com isso nossa variavel de config 
irá ter todas as configurações do knex. Eu passei migrations e dentro eu configurei 
a extension que será usada nas migrations, a outra é o directory  onde quero que
seja salva as migrations. A pasta tmp foi renomeada para db e vou passar a sua 
localização para dentro de directory  e salvar dentro dela as migrations. 

# Criando Tabela de transações 

- Uma grande vantagem de se usar o knex é que depois podemos facilmente trocar de 
banco de dados sem mudar o código, Por isso quando criamos as tabelas no banco de 
dados utlizamos uma sintaxe especifica do knex para fazer a criação das tabelas, 
quando criamos a migration o arquivo gerado tem a data mês e hora em seguida do 
nome da migrate, a migration  já vem com dois metodos up e down.

- up ==> É o que que a migration vai fazer no banco de dados, criar uma tabela ou 
adicionar um campo , remover uma tabela ou um campo ou qualquer outra coisa do tipo.

- down ==> Esse método deve fazer o oposto que o método up fez, ele serve para 
quando algo dá errado e for necessário voltar atrás, fazer um ralback. 

- Dentro dessa migration que foi criada no metodo up eu criei uma tabela chamada
transactions e como sengundo paramtro eu passo uma function essa function recebe 
um parametro chamado table e ele vai me dar acesso a todos os tipos de colunas 
que podemos ter em um banco de dados. 

- Não é recomendado utilizar chaves primarias por inteiros, na maioria das aplicações 
vale mais a pena utilizar uma chave primaria com um valor aleatorio e dificil de 
ser descoberto por isso utilizamos um campo chamado uuid (universal unique id)  
dentro eu passo o nome do campo da tabela, será o id e por ser a chave primaria 
eu devo utilizar o primary(), em seguida criei meu sengundo campo na tabela do 
tipo text que chamei de title passei o notNullable() para que ele não possa 
ficar vazio.

export async function up(knex: Knex): Promise<void> {
    await knex.schema.createTable('transactions', (table) => {
        table.uuid('id').primary()
        table.text('title').notNullable()
    })
}

- No metodo down eu vou desfazer a minha tabela utilizando um dropTable passando 
o nome da tabela. 

export async function down(knex: Knex): Promise<void> {
    await knex.schema.dropTable('transactions')
}

- Em seguida para executar o código que foi criado no banco de dados rodamos o 
comando abaixo:
    npm run knex -- migrate:latest

- Posso validar isso abrindo a rota no navagdor na porta em que o projeto está sendo 
executado.

## Importante edições em Migrations

- Quando uma migration é enviada para produção ou enviada para o time de dev, ela 
nunca mais pode ser editada, não tem como editar uma migration, em casos de erro 
caso a migration já tenha sido enviada, deve ser corrigido ou editado através de 
uma nova migration.

- Se caso a migration ainda não foi enviada podemos editar executando o comando: 
        npm run knex -- migrate:rollback  
- Esse comando defaz a migration que foi executada antes de executar deve parar o 
servidor. 

- Eu criei mais um campo para a tabela do tipo timestamp com o nome de create_at 
a função desse campo é anotar a data em que cada registro foi criado, o defaultTo 
dele vamos utilizar uma função do proprio knex por que a idéia é esse código 
ficar compativel com qualquer banco de dados, essa função é a fn.now que é uma forma 
de retornar a data atual. Esse campo não pode ser nulo e por isso passei o notNullable

- Em seguida eu executo  novamente a migration e a tabela vai atualizar com os novos 
campos. 

- Eu posso ter migrations que adicionam ou alteram um campo, eu criei uma nova migration
chamada add-session-id-to-transaction note que o nome da migration não é mais um nome
de criar uma tabela e sim adicionando um campo chamado session id na tabela de 
transactions.

- Dentro eu vou utilizar o alterTable passando o nome da tabela que quero alterar 
reebendo table como paramtro na segunda função, dentro eu adicionei um novo campo do 
tipo uuid dei para esse campo  o  nome de session_idutilizei o metodo after indicar 
que esse campo fique após o campo que passei dentro de after que foi o id, vale 
ressaltar que não são todos os bancos que suportam isso, passei também um index() 
para que ele crie um indice nesse campo da tabela. 

PS -indice é uma forma de informar ao banco de dados que serão feitas muitas buscas 
em transações especificas de um id de uma sessão, significa que esse campo será muito 
utilizado e isso deixa a busca muito mais rapida por que o banco de dados vai criar 
um tipo de cache de qual session_id possue quais transactions. 

- No campo down como eu desfaço o que fiz em up eu apenas dei um dropColumn na coluna 
que criei. 

export async function up(knex: Knex): Promise<void> {
    await knex.schema.alterTable('transactions', (table) => {
        table.uuid('session_id').after('id').index()
    })
}


export async function down(knex: Knex): Promise<void> {
    await knex.schema.alterTable('transactions', (table) => {
        table.dropColumn('session_id')
    })
}

- Em seguida rodo novamente o migrate:latest para o código ser executado.

# Realizando queries com Knex 

- Aqui testamos algumas operações que são feitas em banco de dados dentro do 
arquivo de server.ts dentro da rota hello eu inserir uma nova transação no 
banco de dados , eu passo o knex com o nome da tabela e utilizei o metodo 
insert para fazer uma inserção no banco de dados, dentro desse insert eu passei 
o id que gera numeros e letras aleatoreas porém eu  posso utilizar o modulo 
crypto do node passando o metodo randomUUID() isso vai gerar um valor válido 
para o id, tive que passar um titulo para a transação, e o amount com um valor.

- Antes de retornar transaction eu devo utilizar .returning('*') para que meu banco 
de dados retorne todas as informações que foram inseridas.

- Eu chamando a rota no navegador posso ver os dados da informação que foi inserida 
no banco de dados.

app.get('/hello', async () => {
    const transaction = await knex('transactions').insert({
       id: crypto.randomUUID(),
       title: 'Transação de teste',
       amount: 1000, 
    })
    .returning('*')

    return transaction
}) 

- Agora posso fazer outro teste fazendo uma busca com um select e ele vai buscar 
todas as inserções que foram feitas na tabela.

app.get('/hello', async () => {
    const transaction = await knex('transactions').select('*')

    return transaction
}) 

## importante

- As Rotas da aplicação vão fazendo diferentes operações no banco de dados 
a maioria das API´s que desenvolvemos são rotas que são portas de entrada 
para o usuário poder trabalhar com o banco de dados, anexado a várias regras 
de negócios. 

# Variáveis de ambiente 

- São informações que podem ser diferentes a cada ambiente em que a aplicação for 
executada. 

- Criamos um arquivo chamado .env para se trabalhar com esse arquivo é importante 
instalar uma extenção chamada DotENV essa extenção entende a sintaxe do arquivo env
 dentro desse arquivo .env todas as configurações serão variaveis e valores. 

- É necessário ler esse arquivo dentro do node e para isso instalamos o dotenv 
com o comando    npm i dotenv 

- Quando eu for utilizar a variavel de ambiente eu importo ela no topo do  arquivo
onde vou uriliza-la, importo de dotenv/config esse arquivo expõe do arquivo .env
na raiz da aplicação todos os valores ali dentro e colocar dentro da variavel 
global chamada  process.env eu posso chamar a varivale de ambiente criada a partir 
dessa global. 

connection: {
        filename: process.env.DATABASE_URL,
    },

- O TypeScript garou um erro informando que se o DATABASE_URL tiver undefined todo 
o código vai gerar um erro, isso por que ele não sabe que o DATABASE_URL está 
preenchido, uma das formas de resolver é escreber um if se DATABASE_URL não for 
informado vou disparar um erro utilizando um throw e nenhum código abaixo sera 
executado. 

_ Geralmente as variáveis de ambientes são utilizadas para colocar dados sensiveis 
chaves de API, por isso é interessante colocar esse arquivo dentro do arquivo 
.gitignore para que ele não suba ao respositorio publico e fique visivel. 

- Quando é necessário compartilhar essas variaveis podemos criar um arquivo chamado 
.env.example e dentro dele colocamos as variaveis porém sem colocar valores 
principalmente quando se tem dados sensiveis, só deixamos valores apenas quando não 
se trata de dados sensiveis, Dados como chaves de api só colocamos o nome sem o valor.  Por isso esse arquivo pode subir no git.

# Tratando env com Zod 

- Existe uma forma meçhor de se trabalhar com variaveis de ambientes obrigatórias 
sem ter a necessidade de ta criando blocos if o tempo todo. 

- Algo interessante é utilizar uma lib especifica para a validação de dados, elas 
validam o formato dos dados, é necessário validar além da presença os valores o 
formato, isso é necessário por que a aplicação não pode executar com as variaveis
de ambiente informadas de forma incoerreta. 

- Dentro da pasta src eu crio uma pasta chamada env com um arquivo index.ts dentro 
é necessário instalar a lib Zod que a lib que utilizamos para a validação de dados. 
basta rodar o comando     npm i zod  

- Essa biblioteca pode ser utilizada para validação de qualquer tipo de dado dentro 
da aplicação.

- Eu peguei a importação do  import 'dotenv/config'; e movi ela para dentro do novo 
arquivo index que criei, em seguida eu importo de dentro do zod o z que serve para
criar um Schema e dentro dele eu devo informar o formato que vou receber de dados 
das variaveis de ambiente, e fazemos para todas as variaveis de ambiente um único 
Schema, eu defino que meu Schema é um objeto passando z.object e dentro eu passo o 
objeto, nesse objeto deve ser informado as variaveis que temos dentro da aplicação
utilizo o z e seto o tipo da variavel se ela puder ter um valor vazio eu posso 
utilizar o nullable. 

import 'dotenv/config';
import { z } from 'zod';

const envSchema = z.object({
    DATABASE_URL: z.string(),
})

- Em seguida eu crio uma constante env eu utilizei o método parse para pegar o 
schema passando para ele os dados que vem de process.env e o zod de forma automatica
faz uma validação. Eu devo exportar essa const.

export const env = envSchema.parse(process.env) 

- Dentro do meu database sempre que for necessário uma variavel de ambiente ao invés 
de acessa-la de process.env eu vou acessar diretamente de env e para isso eu devo 
importar o env.

import { env } from "./env";

connection: {
    filename: env.DATABASE_URL,
},

- Algo interessante que que nessa validação ele já traz os dados tipados. 

- Eu posso fazer a mesma coisa dentro do server com a PORT 

app.listen({
    port: env.PORT,
}).then(() => {
    console.log('HTTP Server Running!')
})

- Outra coisa bem comum de se ter dentro das variaveis de ambiente é o NODE_ENV 
que informa em qual ambiente a aplicação roda development, test, production 
eu passo com o z e vou utilizar um enum para informar que essa variavel pode ser
qualquer um dod 3 ambientes e caso ela não esteja posso passar um default que é 
production isso significa que quando a aplicação estiver executando sem informar a
NODE_ENV irá ser utilizado production por padrão.

const envSchema = z.object({
    NODE_ENV: z.enum(['development', 'test', 'production']).default('production'),
    DATABASE_URL: z.string(),
    PORT: z.number().default(3333),
})

- Dentro do arquivo .env eu devo informar a variavel NODE_ENV com development
no arquivo .env.exemple eu devo colocar a mesma coisa.

- Note que se comentar-mos a variavel de ambiente DATABASE_URL e fazer um teste 
rodando novamente oprojeto, vai dar um erro por que o zod fez a tratativa porém a 
mensagem de erro não é tão clara, podemos melhorar no lugar do parse o safeParse 
que também faz a validação assim como o parse porém ele não dispara um erro caso 
a validação falhe, em seguida eu crio um if com a seguinte condição caso  
env.sucess seja falso isso significa que ele falhou a verificação por que existe 
alguma variavel ambiente que não está informada da maneira correta, e com isso 
criamos o nosso proprio erro  console.error('Invalid enviroment variables!', _env.
error.format()), para o código não continuar executando eu utiizo um throw new Error
em seguida caso ele passe utilizamos ==>  export const env = _env.data 

const _env = envSchema.safeParse(process.env)

if (_env.success == false) {
    console.error('Invalid enviroment variables!', _env.error.format())

    throw new Error('Invalid enviroment variables.')
}

export const env = _env.data

- Note que ao rodar novamente o projeto o erro já mudou e teremos lá a informação de
Invalid enviroment variables. 

# Implementando as rotas 

# Requisitos da aplicação

- É importante pensar antes a aplicação antes de colocar a mão na massa, é importante 
pensar em 3 coisas dentro da engenharia de software que são RF(Requisitos funcionais)
RN(Regras de negócio) e RNF(Requisitos não funcionais). 

- É muito importante pensar antes nessas coisas antes de sair criando as rotas 



## RF 
- Quais são as funcionalidades da aplicação o que o usuário pode ou não fazer 
dentro da aplicação.

- O usuário deve poder criar uma nova transação;
- O usuário deve poder obter um resumo da sua conta;
- O usuário deve poder listar todas as transações que já ocorreram;
- O usuário deve poder visualizar uma transação única;

## RN 
- Podemos colocar condicionais coisas que podem acontecer e que a aplicação 
vai validar 

- A transação pode ser do tipo crédito que somará ao valor total, ou débito diminui;
- Deve ser possível identificarmos o usuário entre as requisições;
- O usuário só pode visualizar transações o qual ele criou;

## RNF 
- Como vamos atingir os demais requisitos, quais tecnologias, estratégias. 

# Plugins do Fastify 

- A funcionalidade de plugins do Fastify é bem interessante, essa é uma forma de 
separar pequenos pedaçõs da aplicação em mais arquivos. 

- Eu criei uma pasta dentro de src chamada routes e dentro eu crio arquivos para 
as minhas rotas, dentro do meu arquivo eu exporto uma função para minha rota aqui 
chamei de transactionsRoutes esa função recebe como paramtro o app que é a variavel,
devo importar nesse arquivo o knex. É obrigatório que seja uma função asyncrona.

import knex from "knex";

export async function transactionsRoutes(app) {
    app.get('/hello', async () => {
        const transaction = await knex('transactions')
        .where('amount', 1000)
        .select('*')
    
        return transaction
    }) 
}

- dentro de server chamamos app.register() com o nome do plugin que criamos.

import { transactionsRoutes } from './routes/transactions';

app.register(transactionsRoutes)

- Se testarmos rodando o projeto e verificando o localhost a rota vai está sendo 
enviada, significa que funcionou o plugim criado.

- Vai dar um erro de TypeScript por ele não reconhecer o formato de app podemos tipar
o app passando : FastifyInstance que é a instancia da aplicação.

import { FastifyInstance } from "fastify";
import  { knex } from "../database";

export async function transactionsRoutes(app: FastifyInstance) {
    app.get('/hello', async () => {
        const transaction = await knex('transactions')
        .where('amount', 1000)
        .select('*')
    
        return transaction
    }) 
}

## Ordem dos plugins 

- A ordem que definimos os plugins é a ordem em que o Fastify irá executar , por isso
se tem algum plugin que modifica algo importante na aplicação e for necessário rodar
antes dos outros é importante colocar antes dos outros. 

# Criação de transações

- Dentro do server eu consigo na importação do register passar um segundo paramtro 
com algumas configurações e uma delas é o prefix que é o prefixo da url para que 
esse plugin seja ativo com isso todas as rotas que tiverem esse prefixo vão cair 
nesse plugin. 

- Para criar uma nova transação utilizamos o body da requisição que é de onde vem
os dados da transação, dentro do paramtro da função async recebemos request que é 
a requisição dentro dessa request temos varias informações que podemos buscar, aqui 
vamos utilizar o body, o request body é de onde vem as informações que geralmente 
são encriptadas com protocolo HTTPs essas informações servem para criar ou editar 
algum recurso. 

- Dentro desse Request body queremos receber algumas informações como titulo, valor 
e o tipo da transação se é credito ou debito. 

- Utilizamos o zod para validar o body da requisição e também fazer a validação de 
tipos de forma automatica, igual fizemos com as variaveis de ambiente.  

- Em seguida foi criado uma nova transaction utilizando o metodo insert para inserir 
informações no banco de dados, no id eu vou utiizar a função randomUUID(), no amount
eu estebeleci a seguinte condição se for do tipo credito eu utilizo o amount normal
se não for eu pego o amount e multiplico por -1 , eu não preciso armazenar esse 
insert dentro de uma variavel e nem retornar nada.

- Eu também posso utilizar o replay ou response para enviar um status code e o send 
vai enviar uma resposta que pode conter uma mensagem ou até mesmo ficar vazia.

import { randomUUID } from "node:crypto";
import { FastifyInstance } from "fastify";
import { z } from "zod";
import { knex } from "../database";

export async function transactionsRoutes(app: FastifyInstance) {
    app.post('/', async (request, replay) => {

        const createTransactionBodySchema = z.object({
            title: z.string(),
            amount: z.number(),
            type: z.enum(['credit', 'debit']),
        })

        const { title, amount, type } = createTransactionBodySchema.parse(
            request.body,
        )

        await knex('transactions').insert({
            id: randomUUID(),
            title,
            amount: type == 'credit' ? amount : amount * -1,
        })

        return replay.status(201).send()
    })
}

## Insomnia 

- É um RESTclient é uma aplicação que permite fazer chamadas HTTP dentro da nossa 
maquina para dentro de alguma API, pode ser baixado de forma totalmente gratuita. 

- Abrindo o insomnia eu crio uma nova request collection em Create New Request 
Collection, chamei de Ignite Node.js API REST , eu crio uma pasta em New Folder 
e vou chamar essa pasta de Transactions, Dentro dessa pasta eu criei minha 
primeira requisição do tipo POST e vou passar para ela a rota http://localhost:3333/
transactions , Renomeei essa requisição para Create transaction, dentro do body eu 
vou mudar para JSON, e dentro eu envio os dados da transação. 

{
	"title": "Freelancer",
	"amount": 8000,
	"type": "credit"
}

- Após isso eu clico em Send e podemos ver o status code da requisição, ele mostrou 
201 informando que foi criado.

# Tipagem no Knex 

- Uma das coisas que podemos verificar no Knex é que ele não consegue identificar 
quais campos e tabelas existem dentro do banco de dados de forma automatica 
ele não possue uma inteligencia de sugerir quais campos existem no banco, quais 
são opcionais, essa é uma limitação da maior parte dos Query Builders. 

- Existe uma forma de conseguir informar ao Knex de forma mais manual quais são 
as tabelas do banco para que o código fique mais inteligente. 

- Para fazer isso eu crio uma pasta dentro de src chamada @types essa pasta vai servir 
para sobrescrever tipagens de outras bibliotecas, dentro eu criei um arquivo que 
chamei de knex.d.ts é importante ressaltar que esse arquivo precisa ter a extenção 
.d.ts isso significa que esse arquivo vem de definição de tipos, esse tipo de arquivo 
não possue código JavaScript dentro dele, apenas código TypeScript. 

- Dentro desse arquivo para sobrescrever um tipo que vem de dentro de uma biblioteca
eu importo a biblioteca, nesse caso importamos o knex, isso significa que vou 
reaproveitar todos os tipos que vem de dentro do knex e nesse arquivo iriei adicionar 
alguns novos tipos. 

- Dentro desse arquivo eu declaro um modulo e crio uma interface passando as 
informações. 

import { Knex } from "knex";

declare module 'knex/types/tables' {
    export interface Tables {
        transactions: {
            id: string
            title: string
            amount: number
            create_at: string
            session_id?: string
        }
    }
}

- Isso vai deixar o código mais inteligente , ele não vai deixar por ex alguém passar
um campo que não exista, mostrar os campos existentes, isso vai deixar o código 
mais fácil de dar manuntenção.

# Listagem das transações 

- Aqui criamos uma rota de listagem de todas as transações e para isso é utilizado 
o metodo get, o request e reply só utilizamos se for necessário caso não seja não 
precisa colocar, nessa requisição em que chamei de transactions eu utilizo o knex 
dando um select o * é opcional , se colocar apenas o select vai dar certo também, 
eu retorno transactions.

 app.get('/', async () => {
        const transactions = await knex('transactions').select()

        return transactions 
    })

- No insomnia eu posso duplicar a requisição que eu tinha feito e mudar para GET 
posso tirar o body e testar dando um Send.

- É interessante retornar o transactions como objeto por que caso seja necessário 
retornar no futuro alguma informação a mais como o o total por ex , é interessante 
trabalhar com objetos tanto no retorno quando no envio de informações de um lado 
para o outro por que se torna mais fácilde adicionar ou remover informações futuramente

app.get('/', async () => {
        const transactions = await knex('transactions').select()

        return {
            transactions
        }
    })

- Aqui também criamos a rota que busca detalhes de uma transação unica, eu utilizo 
/:id por que eu quero receber um parametro da rota que vai identificar a transação 
vou utilizar o request e acessar o params que são os parametros nomeados que temos 
na url, vou utilizar o zod para fazer a validação. eu utilizo o first no final por que 
é esperado que se tenha apenas uma transação com esse id e caso esse metodo first não 
seja utilizado ele irá retornar esse método com um array , esse método informa que só 
se tem um resultado que é o primeiro resultado. No final eu retorno transaction como 
objeto. 

app.get('/:id', async (request) => {
        const getTransactionParamsSchema = z.object({
            id: z.string().uuid(),
        })

        const { id } = getTransactionParamsSchema.parse(request.params)

        const transaction = await knex('transactions').where('id', id).first()

        return { transaction }
    })

    - Em seguida eu volto no insomnia e crio uma nova rota chamada Get transaction, na 
    url eu preciso colocar um id de uma transação valida para testar. 


# Resumo de transações 

- Aqui criamos uma nova rota para retornar o resumo, essa rota vou chamar de summary,
essa rota simplismente faz uma querie para o banco de dados. Eu vou utilizar o metodo 
de agregção sum que pode ser utilizado em qualquer banco sql, esse método soma todos os
valores de uma coluna, eu passo para o metodo o nome da coluna que quero somar, como 
eu só espero um único valor eu não preciso retornar um array, por isso eu utilizei um 
first(), no segundo parametro de sum eu posso passar algumas configurações para o 
amount, aqui eu utilizei o { as: } que é o nome que quero dar para essa coluna.

 app.get('/summary', async () => {
        const summary = await knex('transactions')
            .sum('amount',  { as: 'amount' })
            .first()

        return { summary }
    })

# Utilizando cookies no Fastify 

- Quando dois usuarios utilizarem a aplicação todas as transações criadas por ambos 
fiquem especificas para cada um deles.

- Quando o usuario criar a sua primeira transação eu anoto na sua máquina um id 
e esse id ele irá utilizar em todas as transações, requisições que for fazer a diante
para identificar que esse usuário é o mesmo que criou essa transação inicialmente. 

## Cookies 

- São formas de manter contexto entre requisições, são bastante utilizados em sites e 
redes sociais, com isso não é necessário está logado para que o site ou rede social 
saiba quem é o usuario no contexto entre todas as requições que for feita. 

## LGPD e Cookies

- Hoje é Obrigado pela LGPD o site perguntar se o usúario aceita esses cookies,
muitas vezes o site caso queira monitorar o usuário  ele salva alguma informação 
como o id dentro do navegador de uma forma que o usuário não percebe muitas vezes 
esse id mesmo que a pessoa não esteja logado é uma forma do site conseguir validar 
que o mesmo usuário baseado nesse id que fica salvo nos cookies fez tais requisições 
e tais processos dentro da aplicação. 

- Toda vez que o usuário loga na aplicação todo esse histórico de coisas feitas mesmo 
antes de está logado são salvos na conta do usuário ou seja o usuário não precisa está 
logado na aplicação mas ela coletar tudo que o usuário faz. 

- Utilizamos aqui a estratégia de cookies para conseguir saber que o mesmo usuário 
que está cadastrando transações é o usuário que está listando as transações. 

- Foi por isso que dentro da tabela transactions no nosso db colocamos um campo 
chamado session_id  

## Fluxo na aplicação 

- A partir do momento que o usuário criar a primeira transação  vai ser anotado para
esse usuário um session_id, quando esse usuário for listar alguma transação podemos 
sempre validar apenas transações daquele mesmo session_id 

- Para trabalhar com Cookies dentro do fastify rodamos o comando abaixo: 
        npm i @fastify/cookie 
Vai facilitar para trabalhar com cookies. 

- Em seguida dentro do server antes das rotas e lembre que a ordem é IMPORTANTE 
isso por que se queremos trabalhar com cookies dentro das rotas de transactions é 
importante que o cadastro do modulo de cookies aconteça antes , eu importo o cookie 
e vou utilizar a função register() e como ele é um plugim eu apenas importo ele dentro 
da função register(cookie)  

import cookie from "@fastify/cookie";

app.register(cookie) 

- Em seguida dentro do arquivo de transactions no app.post que é o inicio de tudo 
eu vou utilizar uma variavel que pode mudar seu valor , vou chamar de sessionId 
e eu vou procurar dentrro de cookies da minha requisição que é o request se já 
existe uma sessionId  ==>  let sessionId = request.cookies.sessionId   
se ela já existe eu passo ela dentro do meu insert ==> session_id: sessionId 
eu também vou estabelecer a seguinte condição, se não existir uma sessionId eu crio 
uma nova sessionId utilizando o randomUUID() que gera um id único e vou utilizar 
o replay para salvar nos cookies uma informação chamada sessionId com o valor desse
id que foi criado.

  let sessionId = request.cookies.sessionId

        if (!sessionId) {
            sessionId = randomUUID()

            reply.cookie('sessionId', sessionId)
        }

        await knex('transactions').insert({
            id: randomUUID(),
            title,
            amount: type == 'credit' ? amount : amount * -1,
            session_id: sessionId,
        })

- Da para passar configurações para esses cookies, dessas informações as mais 
importantes são o path que serão quais endereços esses cookie vai está disponivel 
ou seja quais rotas do back end vai poder acessar esse cookie, colocando / eu estou 
dizendo que qualquer rota do back end pode acessar esse cookie, sobre a parte de 
expiração do cookie isso por que todo cookie que salvamos no navegador do usuário 
precisa expirar em algum momento, podemos utilizar o expires dessa forma é necessário 
passar o objeto Date com a data em que o cookie irá expirar, temos também uma outra 
opção bastante utilizada chamada maxAge que podemos passar em milisegundos o tempo 
que esse cookie deve durar no navegador do usuário. 

reply.cookie('sessionId', sessionId, {
    path: '/',
    maxAge: 1000 * 60 * 60 * 24 * 7, // 7 days 
})

## Trabalhando com milisegundos

- 1 segundo equivale a 1000 milisegundos, para 1 minuto eu pego esse valor e 
multiplico por 60 ==> 1000 * 60 para 1 hora eu multiplico por mais 60  ===> 
1000 * 60 * 60 para 1 dia eu multiplico por mais 24 ==> 1000 * 60 * 60 * 24 
e para 7 dias eu multiplico por mais 7 ===> 1000 * 60 * 60 * 24 * 7 

## Clean code 

- Foi muito mais legivel calcular dessa forma do que colocar o valor todo em
milesegundos ==> 604.800.000, o código ficou muito mais legivel, também comentar a 
quantidade de dias ao lado torna ainda mais fácil de entender. 

- Se eu apenas tovesse calculado e colocado  604.800.000 funcionaria porém isso 
deixaria o código ilegivel. Ninguém entenderia essa poha depois. 

## Testando os Cookies 

- Dentro do insomnia eu vou na minha rota post para criar minha primeira transação 
e testo utilizando o Send, a aba de Cookies vai identificar e mostrar o sessionId 
caso tudo esteja certo.

- Note que se utilizamos a rota de listar nossas transações essa nova transação que
foi criada agora vai possuir um valor no session_id diferente das antigas que 
listava como null 

{
	"id": "a871bd2d-8a52-4239-8041-9e8aa239a891",
	"title": "Freelancer",
	"amount": 8000,
	"create_at": "2023-03-01 19:06:41",
	"session_id": "02b0fb02-b9f6-45e5-912a-b76794dae138"
}

# Validando existência do cookie 

- Nas rotas de listagem é necessário buscar apenas as transações daquela sessão 
daquele usuário, so sessionId que identifica o usuário, Eu preciso utilizar request 
para acessar cookies e pegar o sessionId e escrevo a seguinte condição se a sessionId
não existir dentro dos cookies eu posso retornar de dentro uma resposta reply de erro 
eu posso utilizar o status nessa resposta passando o status code de não autorizado por 
ex e posso utilizar um send passando uma mensagem de error. veja como ficou a rota 
após essa modificação: 

app.get('/', async (request, reply) => {
        const sessionId = request.cookies.sessionId

        if (!sessionId) {
            return reply.status(401).send({
                error: 'Unauthorized.',
            })
        }

        const transactions = await knex('transactions').select()

        return {
            transactions
        }
    })

- PS Dentro da minha requisição de listar do insonmia tem uma parte de cookies que me 
leva para Manage Cookies com as informações do meu cookie, eu posso excluir meu  
cookie dentro dessa opção. 

- Para testar eu deleto meu cookie no insonmia e chammo novamente a rota de listar 
as transações e note que vai mostrar a mensagem error: 'Unauthorized.',
Criando novamente uma transação ele vai criar um novo cookie e isso faz com que 
eu consiga novamente listar as transações.

- dentro da parte em que eu utilizo as querie de banco de dados em transactions nessa
rota eu vou adicionar um where para listar transações apenas onde o session_Id seja 
igual a sessionId 

app.get('/', async (request, reply) => {
        const sessionId = request.cookies.sessionId

        if (!sessionId) {
            return reply.status(401).send({
                error: 'Unauthorized.',
            })
        }

        const transactions = await knex('transactions')
        .where('session_id', sessionId)
        .select()

        return {
            transactions
        }
    })

- Testando a listagem no isnsonima note que ele vai trazer apenas a transação que 
foi criada com session_id a partir do cookie que foi criado.

- Note que algmas das rotas vão precisar desse mesmo código que valida que o cookie 
está presente, para não ter que ficar repetindo o mesmo código  vamos criar um 
middleware. 

# Middleware 

- É a criação de interceptadores na nas rotas e reaproveita-los esses interceptadores
executam antes das 3 rotas, eles recebem os mesmo parametros request e reply e eles
podem fazer verificações dentro das rotas

- Eu criei uma pasta chamada Middlewares e dentro um arquivo chamado 
check-session-id-exists.ts, dentro desse arquivo eu crio e exporto 
uma função na qual chamei de checkSessionIdExists() e dentro dela eu 
vou colocar a validação que criei dentro da minha rota.

- Note que vai dar um erro de tipagem e para isso é necessário tipar importando 
o FastifyReply e FastifyRequest e tipando de forma manual. 

import { FastifyReply, FastifyRequest } from "fastify"

export async function checkSessionIdExists(
    request: FastifyRequest,
    reply: FastifyReply
) {
    const sessionId = request.cookies.sessionId

    if (!sessionId) {
        return reply.status(401).send({
            error: 'Unauthorized.',
        })
    }
}

## preHandler 

- São formas de compartilhar regras de negócio entre várias rotas.

- Dentro da rota vai dar um erro no sessionId e para corrigir eu posso desestruturar 
sessionId de dentro de request.cookies ==> const { sessionId } = request.cookies 

- Dentro da minha rota eu vou colocar como segundo parametro antes da função async 
um objeto que me dá acesso a várias configurações a que vou utilizar aqui é a 
preHandler e dentro dele eu coloco um array com a função checkSessionIdExists, 
geralmente utilizamos array por que dentro desse preHandler podemos colocar varias 
funções. 

app.get(
    '/',
    {
        preHandler: [checkSessionIdExists],
    },
    async (request, reply) => {
        const { sessionId } = request.cookies

        const transactions = await knex('transactions')
            .where('session_id', sessionId)
            .select()

         return {
            transactions
        }
    })

- Com isso quando o usuário acessar a rota raiz '/'  antes ele executar o Handler que
é a função async ele iá executar a função checkSessionIdExists, essa função valida 
se a sessionId existe se ela não existe vai retornar um erro e o código nem continua
se a sessionId existir o código continua executando.

- Podemos testar novamente no insonmia da mesma forma que fizemos anteriormente.

- Podemos reaproveitar isso em outras rotas caso seja necessário.

# Testes Automatizados

# Entendendo testes automatizados

- Uma das coisas mais importante em uma aplicação desde o inicio pricipalmente 
em uma aplicação back end são os testes automatizados. 

- Testes automatizados são formas de manter a confiança na hora de dar manutenção 
no código a longo prazo. Não tem haver com a aplicação está ou não funcionando mas
o proposito é que testes automatizados dão confiança para se trabalhar no código 
principalmente quando o código está ficando mais complexo. 

- Qual é o problema de não utilizar testes automatizados, muitas vezes se mexe em uma 
parte do código, e uma outra parte que ninguém nem imaginava quebra e dá algum tipo 
de bug ou mau funcionamento, os testes automatizados garantem que podemos mexer em
partes do código e executar esses testes automatizados vão garantir que todas as 
partes do código vão funcionar normalmente sem problemas. 

## Tipos de testes 

- Existem vários tipos vamos focar nos 3 mais famosos. 

- Unitários ==> Vão testar de forma exclusiva uma únidade da aplicação ou seja uma 
pequena parte de forma totalmente isolada, geralmente é o tipo de teste que mais 
temos na aplicação.

- Integração ==> É quando se testa a comunicação entre duas ou mais unidades ou seja 
quando se testa como vários pedaços menores da aplicação funcionam quando estão 
trabalhando juntos temos um teste de integração.

- e2e - ponta a ponta ==> end 2 end são testes que simulam um usuário operando na 
aplicaçaão lembre que o usuario do back end é o fornt end e por isso esse teste faz 
tudo que o front end faria, chamadas HTTP, websockets, esse tipo de teste vai 
verificar se as portas de entradas do back end estão funcionando de ponta a ponta 
desde a rota até o banco de dados.

## Pirâmide de testes 

- É umestudo que explica a importância de cada tipo de testes, qual teste fazer 
primeiro, cada teste possue algumas exigências que são necessário seguir na 
aplicação, para que seja possivel fazer o teste. 

- O primeiro teste que é importante aprender e utilizar é o teste E2E por que 
por que esse tipo de teste não depende de nenhuma tecnologia, não dependem de 
arquitetura de software e não dependem de nada qualquer pessoa pode escrever 
esse tipo de teste. PS - Nessa aplicação vamos utilizar esse tipo de teste. 

- O teste E2E é um teste que vai testar a aplicação de ponta a ponta, rotas, 
vai bater no banco de dados e é um pouco mais demorado que os outros, em back 
ends grandes por ex pode ser mais demorado. por isso existem também os outros 
tipos de testes. 

- O ideal é ter poucos testes E2E, mais testes de integração e muitos testes 
unitários. 

Pirâmide ====>(Base) Unitarios ====> (Meio) Integração ====> (Topo) E2E 

# Criando primeiro teste 

- Geralmente para criar testes em JavaSCript utilizamos alguma ferramenta terceira 
para escrever os testes, essa biblioteca a sintaxe dos testes é a mesma para quando 
for escrever testes em qualquer outra aplicação JS front end ou back, a ferramenta 
mais famosa de testes hoje é o Jest que é uma ferramanta incrivel para escrever testes

- Nessa aplicação não utilizamos o jest, vamos utilizar o Vitest que é um Framework 
de testes assim como o jest, essa ferramenta vai trazer tudo que for necessário 
dentro do ecossistema de testes, o mais importante dessa ferramenta quando comparamos 
com o Jest é que por baixo dos panos o Vitest usa uma ferramenta chamada esbuild que 
facilita de se trabalhar com TypeScript de forma automatica diferente do Jest que é 
necessário utilizar o babel. 

- O Vitest é compativel com o Jest ou seja se pegar projetos escritos com Jest 
vai dar para conseguir fazer por que o código é igual, o que difere um do outro 
é o que acontece por tras em que o Vitest é muito mais rapido que o Jest. 

## Vitest 

site: https://vitest.dev

- Para instalar o Vitest rode o comando abaixo:
    npm i vitest -D 

- Em seguida eu crio uma pasta chamada test e dentro vou criar um arquivo para meu 
primeiro teste, em testes utilizamos a extenção .test.ts. ou  .spec.ts 

- Dentro desse arquivo eu importo de dentro de vitest a função test, executo a função 
dando um nome ao teste como primeiro parametro dessa função, note que o nome tem que 
descrever o que o teste faz, em seguida no segundo parametro eu escrevo uma função 
para com o teste. 

- O teste é composto de 3 coisas importantes ==> o Enunciado que é o que o teste vai 
fazer, a operação que é o que o teste irá fazer e por ultimo a validação que é como 
vou vaidar que o teste foi bem sucessido e para fazer isso é utilizado o expect() que 
é o que se espera que o código faça, ou seja é o que eu espero que aconteça para que 
o teste seja válido. 

- Depois de escrever o meu teste eu executo ele rodando o comando abaixo: 
        npx vitest 

- Ele vai identificar o test e verificar se vão passar ou encontrar algum problema.

 ✓ test/example.test.ts (1)

 Test Files  1 passed (1)
      Tests  1 passed (1)
   Start at  15:10:09
   Duration  1.53s (transform 235ms, setup 0ms, collect 161ms, tests 5ms)


 PASS  Waiting for file changes...
       press h to show help, press q to quit

PS - Podemos utilizar a tecla A e ele roda o teste novamente de forma bem rápida.

## Criando Script 

- Para não ter que rodar sempre sesse comando, dentro do package.json eu criei 
um script para rodar meu teste. 

"test": "vitest" 

- Assim basta rodar npm run test ou npm test que já vai rodar o teste.

# Testando criação de transação

- Aqui foi feito o primeiro teste da aplicação, que faz uma chamada HTTP , 
cria uma nova transação e vai validar se essa requisição retornou um StatusCode 
de sucesso como um 201.


## SuperTest 
- Para fazer meu teste e evitar tempo colocando rodando o servidor novamente para 
fazer esse teste, existe uma ferramenta chamada supertest para instalar eu rodo o 
comando ====> npm i supertest -D   e  npm i -D @types/supertest  
 
- É importante instalar esse tipo de ferramenta como dependencia de desenvolvimento 
por que os testes nunca vão rodar em produção. 

- Com essa ferramenta dá para fazer requisição na aplicação sem ter que colocar a 
aplicação no ar sem ter que utilizar o metodo listen em meu arquivo de testes. 

- Para fazer isso eu separo a meu server em dois arquivos o app.ts e o server.ts
o arquivo app vou colocar todo o código que está antes do app.listen e dentro 
desse arquivo eu exporto o app , dentro do server.ts eu importo o app e as variaveis 
de ambiente e fazer apenas o listen. Rodando o projeto vai executar tudo normalmente.

- Agora no meu teste eu vou rodar apenas o app e não vou precisar fazer o listen 
com isso quando eu importar o app dentro do meu arquivo de teste eu vou ter acesso 
a minha aplicação sem precisar subir um servidor para ela. 

- Eu importo o supertest como request, eu vou utilizar o await e chamar o request 
passando app.server para ele receber o servidor do node, em seguida da para utiliza 
os metodos https, eu utilizei o metodo post e passei a minha rota, e depois utilzei 
o send em que envio um objeto com os dados que quero enviar, eu posso armazenar isso 
em um response, para validar eu utilizei o expect informando que eu quero que o 
responde.statusCode seja igual ao 201 ==> expect(response.statusCode).toEqual(201)

import { expect, test } from "vitest";
import { app } from  "../src/app";
import request from "supertest";

test('o usuário consegue criar uma nova transação', async () => {
    const response = await request(app.server).post('/transactions').send({
        title: 'New transaction',
        amount: 5000,
        type: 'credit',
    })

    expect(response.statusCode).toEqual(201)
})

- Note que o teste não vai passar e vai retornar um erro 404 isso aconteceu por que 
os plugins que utilizamos utilizam funções async e o erro aconteceu por que a  
aplicação ainda não terminou de cadastrar todos os plugins, é necessário antes de 
executar os testes, assegurar que a aplicação já terminou de cadastrar todos os 
plugins, ja terminou de fazer todas as operações assincronas que ela precisava. 

- Para resolver isso eu posso importar de dentro do vitest uma função chamada 
beforeAll, colocamos essa função no arquivo de teste, dentro dessa função dá 
para executar algum código antes que todos os testes executem, essa função 
executa uma única vez antes de todos os testes, se fosse antes de cada teste 
poderiamos utilizar a função beforeEach. 

- Dentro do beforeAll eu passaei uma função async e escrevo que antes de todos 
os testes quero aguardar e por isso utilizo um await, aguardar que o app 
esteja pronto e por isso utilizo a função ready() do fastify ela vai resolver 
de forma automatica um valor válido ao await quando o fastify terminar de cadastrar
os plugins.

- Em seguida eu utilizo um afterAll para que depois que todos os testes executarem 
eu fechar a aplicação. 

beforeAll(async () => {
    await app.ready()
})

afterAll(async () => {
    await app.close()
})

- Após salvar esse código o meu teste automaticamente vai passar. 

# Categorizando os testes 

- Podemos separar os testes por categoria dentro de arquivos separados, no 
teste que foi feito testamos rotas das transações  por isso  criamos uma 
categoria especifica para ele. 

- Eu importei de dentro do vitest o describe que é uma forma de categorizar 
eu chamo o describe() passando o nome da categoria que eu quero criar 
e depois eu passo uma função com meus testes. 

- Note que ao fazer isso se um teste falhar ele irá informar qual categoria 
e qual teste falhou. Também é possivel criar subcategorias criando categorias 
dentro de uma categoria.

- A função it faz a mesma coisa que a função test. 

# Testando listagem de transações 

- Escrevi o teste para listar as transações, porém para fazer esse teste é necessário
ter a sessionId que deve ser enviado nos cookies porém esse sessionId é criado no 
momento em que a transação é criada, eu poderia fazer isso a partir do teste anterior 
porém jamais pode ser escrito um teste que depende de outro. 

- Eu devo criar um teste partindo do princípio de que os outros testes não existem.

- Para conseguir fazer esse teste eu devo escrever novamente o post do teste anterior 
dentro desse, para criar uma transação na hora do teste, isso por que para listar 
alguma transação é obrigatório ter cadastrado uma transação antes, em seguida eu 
crio uma constante que acessa meus cookies através de Set-Cookie,  em seguida eu 
fiz uma nova requisição para o servidor para a rota get de listagem, utilizo também
o set que é utilizado para setar uma informação da requisição um cabeçalho e aqui
passamos o cabeçalho de cookie com os cookies, em seguida eu utilizo o expect 
passando 200 que é o  que eu espero desse teste.

- Eu armazenei essa requisição em uma variavel que chame de listTransactionsResponse 
isso para poder validar se o corpo da requisição está retornando os dados que eu 
espero que retorne, para fazer isso ==> eu espero que o corpo da minha listagem de 
transações seja igual a um array e dentro desse array eu espero que exista um objeto 
contendo objectContaining e eu passo as informações que eu quero. 

- Se eu rodar dessa forma o teste não passa por que ele espera retornar um objeto 
antes do array para resolver isso eu passo também no expect transactions.

 test('should be able to list all transactions', async () => {
        const createTransactionResponse = await request(app.server)
        .post('/transactions')
        .send({
            title: 'New transaction',
            amount: 5000,
            type: 'credit',
        })

        const cookies = createTransactionResponse.get('Set-Cookie')

        const listTransactionsResponse = await request(app.server)
            .get('/transactions')
            .set('Cookie', cookies)
            .expect(200) 

        expect(listTransactionsResponse.body.transactions).toEqual([
            expect.objectContaining({
                title: 'New transaction',
                amount: 5000,
            })
        ])
    })

# Configurando banco de testes 

- Pode ser um pouco problempatico em algumas situações rodar os testes em ambiente 
com informações, pode haver algum conflito de informações dependendo do teste, 
o ideal é rodar os testes em uma ambiente zarado e isso serve tbm para o banco de 
dados. 

- Eu criei na raiz da aplicação um arquivo chamado .env.test esse arquivo também foi 
adicionado ao .gitignore, dentro desse novo arquivo env eu vou colocar variavéis de 
ambientes que só quero que sejam chamadas em ambiente de testes, e vou colocar as 
mesmas variaveis do primeiro arquivo env porém vou modificar para teste.

NODE_ENV=test
DATABASE_URL="./db/test.db"

- como os arquivos que estão em gitignore não sobem ao repositorio do github eu 
criei tambémum arquivo .env.test.example com um exemplo para a pessoa pegar. 

NODE_ENV=development
DATABASE_URL="./db/app.db"

- Dentro de src na pasta env no arquivo index, eu  possuo o import import 'dotenv/
config'; sempre vai carregar exclusivamente o arquivo .env porém é possivel que de
dentro de dotenv importar o config 

- A variavel NODE_ENV quando estamos executando alguma ferramenta de testes como 
i Vitest ela é preenchida automaticamente, e por isso eu posso tirar ela do meu 
arquivo .env.test 

- Com isso eu posso fazer o seguinte teste se o NODE_ENV for igual a test eu executo 
o metodo config passando para ele que no nome do arquivo o path que contém as 
variaveis de ambiente da aplicação é nesse caso o .env.test se não  eu executo o 
config sem passar nenhuma opção ou seja ele irá executar o arquivo .env normal

import { config } from 'dotenv';

if (process.env.NODE_ENV == 'test') {
    config({ path: '.env.test'})
} else {
    config()
}

- Eu possuo dois arquivos de variaveis de ambiente diferentes para cada tipo de 
contexto utilizado, desenvolvimento, testes, produção. 

- Note que ao rodar novamente os testes ele já vai criar um novo arquivo no meu banco 
chamado test.db isso significa que ele criou um banco de dados separado para testes.

- Note que ao executar os testes o teste vai falhar apontando que a tabela 
transactions não existe, isso acontece por que criamos o banco mas a tabela
é criada a partir dos migrations, por isso como foi criado umnovo banco de 
testes as migrations não foram executadas nesse banco de testes. 

- Para resolver isso vamos dentro de testes, utilizamos um beforeEach para que
antes de cada um dos testes, eu importei uma função de dentro de node:child_process 
chamada execSync apartir dessa função da para executar comandos no terminal, por 
dentro da aplicação node, vou escrever um comando para zerar as migrations e outro 
para rodar novamente as migrations, assim toda vez que eu rodar os testes vou ter
um banco zerado, ou seja com isso a cada teste o banco é apagado e criado novamente.

# Finalizando testes da aplicação

- Aqui testamos as outras rotas da aplicação as outras portas de entrada, aqui quando
buscamos alguma transação especifica, buscamos pelo id dela, aqui a única forma de 
obter o id da transação é pela listagem, eu pego listTransactionsResponse pegando do
body e primeira transação pegando o id dela, vou armazenar isso em  transactionId

const transactionId = listTransactionsResponse.body.transactions[0].id

- Abaixo disso foi feita uma nova requisição na qual chamei de getTransactionResponse
no get eu fiz uma interpolação passando também o transactionId, em seguida eu espero 
que getTransactionResponse pegando o body e transaction e não utilizei array nesse 
espect por que ele vai retornar diratemente um objeto.

test('should be able to get a specific transaction', async () => {
        const createTransactionResponse = await request(app.server)
        .post('/transactions')
        .send({
            title: 'New transaction',
            amount: 5000,
            type: 'credit',
        })

        const cookies = createTransactionResponse.get('Set-Cookie')

        const listTransactionsResponse = await request(app.server)
            .get('/transactions')
            .set('Cookie', cookies)
            .expect(200) 

        const transactionId = listTransactionsResponse.body.transactions[0].id

        const getTransactionResponse = await request(app.server)
        .get(`/transactions/${transactionId}`)
        .set('Cookie', cookies)
        .expect(200) 

        expect(getTransactionResponse.body.transaction).toEqual(
            expect.objectContaining({
                title: 'New transaction',
                amount: 5000,
            })
        )
    })


- O Ultimo teste testamos a rota de resumo, criamos duas transaçães, copiei a 
primeira e utilizei também o Cookie, a segunda chamei de Debit transaction, 
com isso eu tenho a transação de credito e debito nesse teste, podemos verificar 
se o resumo está resumindo da forma correta, eu crio o summaryResponse e dentro 
do expect vou setar sumary, o meu toEqual espero que seja amount: 3000 que é o 
valor que esepro do meu calculo.

test('should be able to get the summary', async () => {
        const createTransactionResponse = await request(app.server)
            .post('/transactions')
            .send({
                title: 'New transaction',
                amount: 5000,
                type: 'credit',
            })

        const cookies = createTransactionResponse.get('Set-Cookie')

        await request(app.server)
            .post('/transactions')
            .set('Cookie', cookies)
            .send({
                title: 'Debit transaction',
                amount: 2000,
                type: 'credit',
            })

        const summaryResponse = await request(app.server)
            .get('/transactions/summary')
            .set('Cookie', cookies)
            .expect(200)

        expect(summaryResponse.body.summary).toEqual({
            amount: 3000,
        })
    })

# Preparando a app para deploy 

- Aqui configuramos o projeto para fazer o processo de deploy, existem muitas 
arquiteturas de deploy, nada mais são do que formas de subir o projeto para 
produção, aqui utilizamos uma forma de deploy bem simples que é um serviço 
gerenciado, é um tipo de serviço que automatiza mais as coisas.

- O primeiro passo é endende que o código está em TypeScript, nunhuma plataforma 
de deploy em node vai entender codigos Ts, por isso é importante antes do deploy 
converter o código para JavaScript. 

- Quando utilizamos o tsc como fizemos nesse projeto, dá para usa-lo para fazer a
compilação desse código para Js, dentro das configurações do tsconfig.json na 
opção "rootDir" passamos o diretorio em que está o código, e na opção "outDir" 
que é a opção onde vai sair o código compilado eu coloco ./build , após isso eu 
rodo o comando npx tsc ele irá rodar o compilador e vai criar a pasta buid com todo
o código compilado, porém esse processo é um pouco lento principalmente em grandes 
bases de códigos, e existem outras ferramentas melhores para fazer a build do projeto.

## Build

- Eu instaleu uma ferramenta chamada tsup rodando o comando abaixo 
    npm i tsup -D  

    https://tsup.egoist.dev

- Essa é mais uma ferramenta para trabalhar com TypeScript porém para fazer
o processo de build do projeto, Assim como o tsx que estamos utilizando para
executar o código e o vitest que estamos executando os testes, o tsup utiliza 
por debaixo dos panos o esbuild assim como essas outras ferramentas. 

- No arquivo package.json eu criei um script que chamei de build e ele irá executar 
tsup na pasta src  ==>   "build": "tsup src"  

- Em seguida executo a build rodando npm run build 

- Note que ele gerou a build muito rapido e criou a pasta dist que tem todo o 
código da aplicação compilado, para escolher o nome da pasta que ele gera 
basta dentro do nosso script utilizar --out-dir nome-da-pasta. 
    "build": "tsup src --out-dir build"

- Posso fazer um teste rodando o arquivo server da minha build utilizando o comando 
node build/server.js 
Se o servidor rodar normalmente é por que está tudo certo com am build. 

- A pasta build te que ir no gitignore 

# Deploy do app no Render 

- Temos algumas opções gratuitas para testar as aplicações back end algumas boas 
opções são: 

render.com  ==> muito interessante, com um bom painel de administração, serve para 
deploy desde sites staticos, web services, aplicações que rodam sem segundo plano,
bancos de dados, serviços privados. 

fly.io ==> Também interessante, da para hospedar varios tipos de aplicações e varias 
linguagens. 

railway.app ==> Também interessante 

- No projeto utilizamos o render para fazer a hospedagem. 

- Primeiro passo é criar uma conta 

- O segundo passo é criar o banco de dados na aplicação utilizamos um query builder 
e isso já facilita a criação do banco de dados no deploy, com isso a aplicação deve
funcionar com outros tipos de bancos, no render é utilizado o PostgreSQL como a 
maior perte dos serviços de hospedagem.

- Para que o deploy possa ser feito é necessário fazer algumas alterações na 
aplicação, a aplicação precisa suportar o sqlite e o Postgres e para isso foi 
criada dentro do index na pasta env uma nova variavel de ambiente, eu passar 
uma variavel DATABASE_CLIENT passando um enum informando que pode ser tanto sqlite 
quando pg de postgres: 

const envSchema = z.object({
    NODE_ENV: z.enum(['development', 'test', 'production']).default('production'),
    DATABASE_CLIENT: z.enum(['sqlite', 'pg']),
    DATABASE_URL: z.string(),
    PORT: z.number().default(3333),
})

- Agora que a aplicação aceita o pg eu posso instalar os drivers desse banco sem ser
como dependencia de desenvolvimento pois ele vai para produção.
        npm i pg 

- No arquivo .env foi colocada a variável de ambiente   DATABASE_CLIENT=sqlite  
também foi adicionado em todos os arquivos env

- Dentro de database.ts eu vou trocar o client por DATABASE_CLIENT, na parte de 
connection eu vou passar que se o DATABASE_CLIENT for igual ao sqlite vai ser 
passado um objeto com filename DATABASE_URL, se não , se for postgress vai ser
passado direto DATABASE_URL 

export const config: Knex.Config = {
    client: env.DATABASE_CLIENT,
    connection: 
        env.DATABASE_CLIENT == 'sqlite'
            ? {
                filename: env.DATABASE_URL,
               }
            : env.DATABASE_URL,
    useNullAsDefault: true,
    migrations: {
        extension: 'ts',
        directory: './db/migrations',
    }
}

PS- Por padrão o render utiliza a versão 14 do node porém essa versão é antiga pois 
no projeto utilizamos a versão 18 do node, por isso um padrão que existe na comunidade
é dentro de package.json passar "engines" e passando node informando qual versão 
do node quero utilizar, aqui informei maior ou igual a 18 >= 18 com isso ele vai usar 
todas as vesões que são iguais ou maiores a versão 18 do node.

 "engines": {
    "node": ">=18"
  },

- O ultimo detalhe na aplicação antes de ser enviada é na porta é que o render 
envia a port para rodar a aplicação como string e não como número, vai gerar um 
erro por que dentro de env estamos pedindo para que a porta seja um número, para
resolver esse problema utilizamos uma funcionalidade bem interessante do zod que é 
o coerce isso faz com que independente do tipo do valor que for recebido na porta 
ele vai ser transformado em um número, o coerce faz uma convenção para um número.

const envSchema = z.object({
    NODE_ENV: z.enum(['development', 'test', 'production']).default('production'),
    DATABASE_CLIENT: z.enum(['sqlite', 'pg']),
    DATABASE_URL: z.string(),
    PORT: z.coerce.number().default(3333),
})

