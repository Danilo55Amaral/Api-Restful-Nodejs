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














