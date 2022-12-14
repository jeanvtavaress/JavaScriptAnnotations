
Anotações de estudo sobre JavaScript.
## <a name="inicio"></a> Início


# Tópicos
- [Destructuring](#Destructuring)
- [IF-ELSE, ELSE IF](#IF-ELSE)
- [Estrutura de repetição: WHILE, DO WHILE](#WHILE)
- [Estrutura de repetição FOR, FOR...IN, FOR...OF](#FOR)
- [setInterval e clearInterval, setTimeout e cleearTimeout](#setInterval)
- [This](#This)
- [Callback](#Callback)
- [Função Construtora](#FuncoesConstrutoras)
- [Class](#Class)
- [Object Methods](#Object)
- [Array](#Array)
- [Promise](#promise)
- [Async Await](#async)
- [Fetch](#fetch)
## <a name="Destructuring"></a> Destructuring
> É uma expressão que permite extrair dados de um array ou objeto de em variáveis distintas. 

**Exemplo 01:** Destruturação de elementos de um objeto.


```javascript
const pessoa = {
  name: "Gustavo",
  age: 21,
    links: {
      instagram: "https://www.instagram.com/",
      site: "https://www.google.com/"
    }
}

const {name, age} = pessoa;         // => Gustavo 21
const {instagram} = pessoa.links    // => https://www.instagram.com/
 ```
 
 **Exemplo 02:** Destruturação de elementos mais profundos de um objeto.

 
 ```javascript
  const veiculo = {
    marca: "Fiat",
    modelo: "Uno",
      registro: {
        cidade: "Manaus",
        estado: "Amazonas",
        país: "Brasil"
      }
  }
  
  const {modelo, registro:{estado}} = veículo 		// => Uno Amazoanas
 ```
 
 **Exemplo 03:** Pode-se atribuir novos valores a **variáveis**.
 ```javascript
  const person = {
    name: 'Gustavo',
    age: 21
  }
  const {name: 'nome', age: 'idade} = person   // => nome: 'Gustavo' idade: 21
 ```
 
 **Exemplo 04:** Destruturando um array, onde um elemento da matriz não seja pega, usa-se (,,).
 ```javascript
 const nome = ['Gustavo', 'Henrique', 'Souza']
 const [indice0,,indice2] = nome     // => Gustavo Souza
 ```
 
 **Exemplo 05:** Destruturação objetos interaveis, qualquer tipo de coisa que conseguimos fazer um laço sobre, exemplo: array, objeto etc.
 ```javascript
  const pessoas = [
    {
    nome: 'Gustavo',
      familia: {
        pai: 'Pedro',
        mae: 'Nilse'
      },
      idade: 21
    },
    {
    nome: 'Felipe',
      familia: {
        pai: 'Pedro',
        mae: 'Regina'
      },
      idade: 25
    }
  ]
  
  for(const {nome: n, familia:{pai: p}} of pessoas){
    console.log('Nome :' +n+ ', Pai: ' +p)               // => Nome: Gustavo, Pai: Pedro
  }                                                      // => Nome: Felipe, Pai: Pedro
 ```
 - [Início](#inicio)
 <hr>
 
 ## <a name="IF-ELSE"></a> IF, ELSE, ELSE IF
 > IF: Para especificar um bloco de código a ser executado se uma condição específica for verdadeira.
 ```javascript
 let idade = 18
    if(idade >= 18){
      return true            // => true
    }
 ```
 > ELSE: Bloco de código a ser executado, se a primeira for condição for falsa.
 ```javascript
 let idade = 17
    if(idade >= 18){
      return true            // => 
    } else {
      return false           // => false
    }
 ```
 > ELSE IF: Especifica uma nova condição a ser testada se a primeira confição for falsa.
 ```javascript
 let idade = 17
 let acompanhado = true
    if(idade >= 18){
      return true                                      // => 
    } else if(idade =< 18 && acompanhado == true){
      return true                                      // => true
    }
 ```
 - [Início](#inicio)
 <hr>
 
 ## <a name="WHILE"></a> Estrutura de repetição: WHILE, DO WHILE.
> WHILE: Pecorre um bloco de código enquanto uma condição específica for verdadeira. While primeiro verifica a condição, e depois executa o código.
```javascript
let contador = 0
  while(contador < 10){
    contador++                   // => 9
  }
```
> DO WHILE: Bloco de código é executado uma vez e repetido enquanto a condição for verdadeira.
```javascript
let i = 0
  do{
  console.log('Olá')
  i++
  } while(i < 10)
```
- [Início](#inicio)
<hr>

 ## <a name="FOR"></a> Estrutura de repetição: FOR, FOR...IN, FOR...OF.
 > FOR: Pecorre um bloco de código varias vezes.
 
 > Sintaxe: for(inicialização; condição; expressão final) - todas as três expressões na condição do loop são opcionais. No bloco de inicialização, não é necessário inicializar variável por exemplo.
 ```javascript
 let i = 0
  for(; i < 9; i++){
    console.log(i)               // => 0 1 2 3 4 5 6 7 8
  }
 ```
 > FOR...IN: Pecorre as propriedades de um objeto.
 
 > Sintaxe: for(key in object)
 ```javascript
 const monstros = {
  canada: 'sasquatch',
  nepal: 'yeti',
  scotland: 'loch ness monster'
 }
  for(let nomeMonstros in monstros){              // => sasquatch
    console.log(monstros[nomeMonstros])            // => yeti
  }                                                // => loch ness monster
 ```
 > FOR...OF: Permite fazer um loop sobre estruturas de dados interaveis como arrays, strings, maps, nodelist e etc.
 
 > Sintaxe: for(variavel of iteravel)
  ```javascript
//em Array
  const carros = ['bmw', 'volvo', 'mini']
    for(let nomeCarros of carros){                  // => bwm
      console.log(nomeCarros)                       // => volvo
    }                                               // => mini
// em String
  const stg = 'luana'
    for(letras of stg){
      console.log(letras)                          // => l u a n a 
    }
  }
```
- [Início](#inicio)
  <hr>
  
 ## <a name="setInterval"></a> setInterval( ) e clearInterval( ), setTimeout( ) e clearTimeout( ).
 
 
>**setInterval( ):** Método chama uma função em intervalos específicos em milissegundos. Função continua até clearInterval( ) ser chamado.
 ```javascript
 //suponha que há uma div criada no HTML com o ID: quadrado, medidas de 100px por 100px. E que tenha dois botões com IDs: btn1, btn2.
 
let temp
function mudarCor(){                                        // muda a cor do quadrado.
    const div = document.getElementById('quadrado')
    let r = Math.floor(Math.random() * 255)                   
    let g = Math.floor(Math.random() * 255)               // gerando cor aleatoria rgb. 
    let b = Math.floor(Math.random() * 255)                                         
    div.style.backgroundColor = "rgb("+r+","+g+","+b+")";
}

function iniciar(){
    temp = setInterval(mudarCor,2000)        // função iniciar vai chamar a função mudarCor a cada 2 segundos.
}

function parar(){
    clearInterval(temp)                     // para de chamar temp que está responsavel por iniciar a função mudarCor.
}

function addEventos(){                     // responsavel por adicionar evento aos botões.
    document.getElementById('btn1').addEventListener('click', iniciar)
    document.getElementById('btn2').addEventListener('click', parar)
}

window.addEventListener('load', addEventos)  // quando a página carregar a função de eventos já estará disponivel.
 ```
> **setTimeout( ):** Executa algo específico assim que o tempo que foi passado expirar.
```javascript
function saudar(){
    console.log('olá gustavo')      
}

const ativar = setTimeout(saudar, 3000)   // executa a função saudar em 3 segundos.

function parar(){
    clearTimeout(ativar)                 // para a constante ativar, que está responsavel por chamar a função saudar.
}

document.getElementById('btn').addEventListener('click', parar)
```
- [Início](#inicio)
<hr>

 ## <a name="This"></a> This
 > **This:** Em uma função padrão, **this** pode variar seu resultado.
 
 > Referência ao **this** sempre se refere a (e contém o valor de) um objeto.
 
 > Em um método de objeto, this refere-se ao objeto.
 
 > Em uma função, this refere-se ao objeto global.
 
 > Em uma função no strict mode, this é undefined.
 
 > Em um evento, this refere-se ao elemento que recebeu o evento.
 
 > As arrow functions não vinculam seus próprios this, em vez disso, eles herdam o escopo do pai, que é chamado de escopo léxico.
 ```javascript
 const diaAdia = {
  saudacao: 'Bom dia',
    falar(){
      console.log(this.saudacao)    // this está no contexto diaAdia
    }
 }
 ```
 > **This** funciona dentro de contexto. Para dar contexto ao **this**, usa-se .bind( )
 ```javascript
  const diaAdia = {
    saudacao: 'Bom Dia',
        falar(){
            console.log(this.saudacao)
        }
}

const falar = diaAdia.falar.bind(diaAdia)
falar();
 ```
 - [Início](#inicio)
 <hr>
 
 ## <a name="Callback"></a> Callback
 > O que caracteriza um uma callback, é passar uma função como argumento para outra função, e executa-la durante o código.
 ```javascript
 function saudacao(nome){
    console.log('Olá', nome);
}

function entradaDoUsuario(callback){
    let nome = prompt('Nome por favor')
    callback(nome)
}

entradaDoUsuario(saudacao)  
 ```
  ```javascript
function exibePrimeiraMensagem (mensagem, callback) {
	console.log(mensagem);
	callback();
}
function exibeSegundaMensagem(){
	console.log('Essa é a segunda mensagem do novo exemplo');
} 
exibePrimeiraMensagem ('Essa é a primeira mensagem do novo exemplo', exibeSegundaMensagem);  
 ```
 - [Início](#inicio)
 <hr>
 
 ## <a name="FuncoesConstrutoras"></a> Funções Construtoras
 > A função construtora serve de molde para criação de objetos.
 
 ```javascript
 function CadastroVeiculo(marca, modelo, ano){
	this.marca = marca
	this.modelo = modelo
	this.ano = ano
	this.statusCadastro = () => 'Ativo'
}

const palio = new CadastroVeiculo('Fiat', 'Palio', 2009)		
console.log(palio)

/*CadastroVeiculo {
  marca: 'Fiat',
  modelo: 'Palio',
  ano: 2009,
  statusCadastro: [Function (anonymous)]
}*/
 ```
 - [Início](#inicio)
 <hr>
 
 ## <a name="Class"></a> Class
 > Class são modelos para objetos JavaScript
 
 > Class não sofre hoisting.
 ```javascript
 class Livro {
	constructor(nome, editora, paginas){
		this.nome = nome
		this.editora = editora
		this.paginas = paginas
	}
	anunciarTitulo(){
		console.log(`Título: ${this.nome}`)
	}
	descreverTituilo(){
		console.log(`${this.nome} é um livro da editora ${this.editora}, e contém ${this.paginas} páginas`)
	}
}

const mindhunter = new Livro('MindHunter', 'Intrínseca', 374)
mindhunter.anunciarTitulo()					// => Título: MindHunter
mindhunter.descreverTituilo()					// => MindHunter é um livro da editora Intrínseca, e contém 374 páginas
 ```
 - [Início](#inicio)
 <hr>
 
 ## <a name="Object"></a> Object Methods
- [Object.assign()](#assign)
- [Object.create()](#create)
- [Object.entries()](#entries)
- [Object.freeze()](#freeze)
- [Object.keys()](#keys)
- [Object.values()](#values)
- [Object.seal()](#seal)
- [Object.hasOwn()](#wasOwn)
 
 
 ## <a name="assign"></a> Object.assign()
 > É usado para copiar valores de todas as propriedades próprias enumeráveis de um ou mais objetos de origem para um objeto destino.
 ```javascript
 const paleta01 = { corUM: 'Vermelho', corDois: 'Azul', corTres: 'Verde' }
 const paleta02 = { corQuatro: 'Amarelo', corCinco: 'Preto', corSeis: 'Marrom' }
 
 const totalCores = Object.assign(paleta01, paleta02)
 
 console.log(totalCores)
 
 /*
 {
corUm: 'Vermelho',
corDois: 'Azul',
corTres: 'Verde',
corQuatro: 'Amarelo',
corCinco: 'Preto',
corSeis: 'Marrom'
   } 
*/
 ```
 
## <a name="create"></a> Object.create()
 > Faz um objeto ser prototype de outro objeto
 ```javascript
 const pai = {pai: 'Gustavo'}
/* 
pai
{pai: 'Gustavo'}
*/

const filha = Object.create(pai)
/*
filha
{}
	[[Prototype]]: Object
	   pai: "Gustavo"
	   [[Prototype]]: Object
*/

 ```
 
## <a name="entries"></a> Object.entries()
> Retora uma matriz dos pares chaves e valores de um objeto.
```javascript
const coresTimes = {
	flamengo: 'Vermelho e Preto',
	palmeiras: 'Verde e Branco',
	vasco: 'Preto e Branco',
	gremio: 'Azul e Preto'
}

console.log(Object.entries(coresTimes))
/*
[
  [ 'flamengo', 'Vermelho e Preto' ],
  [ 'palmeiras', 'Verde e Branco' ],
  [ 'vasco', 'Preto e Branco' ],
  [ 'gremio', 'Azul e Preto' ]
]
*/
```

## <a name="freeze"></a> Object.freeze()
> Congela um objeto, não sendo possível mexer nele.
```javascript
const pessoa = {
	nome: 'Pedro',
	idade: 25,
	cidade: 'Santa Catarina',
	cep: '*********'
}
Object.freeze(pessoa)

pessoa.nome = 'Alberto'   // Nome continuará sendo Pedro, não se pode alterar nada no objeto depois que usar Object.freeze()
```

## <a name="keys"></a> Object.keys()
> Retorna todas as chaves de valores de um objeto, e em array ele retorna os indices dos elementos.
```javascript
const familia = {
	pai: 'Augusto',
	mae: 'Sandra',
	irmao: 'Ricardo',
	avó: 'Ana',
	avô: 'Inacio'
}

console.log(Object.keys(familia))
// [ 'pai', 'mae', 'irmao', 'avó', 'avô' ]


const ingredientes = ['Ovo', 'Trigo', 'Manteiga', 'Leite']
console.log(Object.keys(ingredientes))
// [ '0', '1', '2', '3' ]


```
## <a name="values"></a> Object.values()
> Retorna um array com os valores das propriedades de um objeto.
```javascript
const familia = {
	pai: 'Augusto',
	mae: 'Sandra',
	irmao: 'Ricardo',
	avó: 'Ana',
	avô: 'Inacio'
}

console.log(Object.values(familia))
// [ 'Augusto', 'Sandra', 'Ricardo', 'Ana', 'Inacio' ]
```


## <a name="seal"></a> Object.seal()
> Sela um objeto, evitando que novas propriedades sejam adicionadas a ele, valores das propriedades atuais ainda podem ser alterados desde que sejam writable.
```javascript
const familia = {
	pai: 'Augusto',
	mae: 'Sandra',
	irmao: 'Ricardo',
	avó: 'Ana',
	avô: 'Inacio'
}

Object.seal(familia)   // a partir de agora propriedades podem ser alteradas, mas não adicionadas ou excluidas.

familia.tio = 'Gerson'		// não adicionado.
familia.pai = 'Elias'		// propriedade alterada.

console.log(familia);

/*
{
  pai: 'Elias',
  mae: 'Sandra',
  irmao: 'Ricardo',
  'avó': 'Ana',
  'avô': 'Inacio'
}
*/
````

## <a name="wasOwn"></a> Object.hasOwn()
> Retorna um valor booleano, se o objeto especifico possui a propriedade indicada retorna true, se a propriedade for herdada ou não existir, retorna false.
```javascript 
const familia = {
	pai: 'pedro',
	mae: 'luana',
	avó: 'ana'
}

console.log(Object.hasOwn(familia, 'pai'))  //  true
console.log(Object.hasOwn(familia, 'avô'))  //  false
```
- [Início](#inicio)

<hr>

## <a name="Array"></a> Array
- [shitf()](#shift)
- [unshitf()](#unshift)
- [push()](#push)
- [pop()](#pop)
- [splice()](#splice)
- [slice()](#slice)
- [indexOf()](#indexof)
- [MAP()](#MAP)
- [REDUCE()](#REDUCE)
- [FILTER()](#FILTER)

## <a name="shift"></a> shift()
> Remove e retorna o primeiro elemento de um array.
```javascript
const frutas = ['uva', 'banana', 'maçã']

console.log(frutas.shift())  // [ 'banana', 'maçã' ]

// uva
```

## <a name="unshift"></a> unshift()
> Adiciona elemento no inicio de um array, e retorna o número de elementos
```javascript
const frutas = ['uva', 'banana', 'maçã']

console.log(frutas.unshift('pêra'))  // [ 'pêra', 'uva', 'banana', 'maçã' ]

// 4
```

## <a name="push"></a> push()
>  Adiciona elemento ao final do array e retorna o novo comprimento dele.
```javascript
const frutas = ['uva', 'banana', 'maçã']

console.log(frutas.push('pêra', 'damasco))  // [ 'uva', 'banana', 'maçã', 'pêra', 'damasco' ]

// 5
```

## <a name="pop"></a> pop()
> Remove e retorna o último elemento de um array.
```javascript
const frutas = ['uva', 'banana', 'maçã']

console.log(frutas.pop()) // [ 'uva', 'banana' ]

// maçã
````


## <a name="splice"></a> splice()
> Altera o conteúdo de uma lista, adicionando novos elementos enquanto remove os antigos.
```javascript
let animais = ['cachorro', 'gato', 'macaco', 'jacaré']

animais.splice(3, 1, 'vaca') 

console.log(animais)

// [ 'cachorro', 'gato', 'macaco', 'vaca' ]
````
## <a name="slice"></a> slice()
> Retorna um recorte do array a partir de índices.
```javascript
const frutas = ['banana', 'uva', 'laranja', 'morango']

const frutasDoces = frutas.slice(0, 2)

console.log(frutasDoces)

// [ 'banana', 'uva' ]
```

## <a name="slice"></a> slice()
> Retorna um recorte do array a partir de índices.
```javascript
const frutas = ['banana', 'uva', 'laranja', 'morango']

const frutasDoces = frutas.slice(0, 2)

console.log(frutasDoces)

// [ 'banana', 'uva' ]
```

## <a name="indexof"></a> indexOf()
> Retorna o primeiro indice que determinado elemento pode ser encontrado no array. E retorna -1 caso não esteja presente.
```javascript
var array = [2, 5, 9]
array.indexOf(2);     //  0
array.indexOf(7);     // -1
```

## <a name="MAP"></a> map()
> Cria uma nova matriz e chama uma função para cada elemento da matriz.
```javascript 
const users = [
	{id: 1, nome: 'victor', idade: 25},
	{id: 2, nome: 'claudio', idade: 23},
	{id: 3, nome: 'jesé', idade: 13},
	{id: 4, nome: 'paulo', idade: 48}
]

const nomes = users.map((nomes) => nomes.nome)
console.log(nomes)
// [ 'victor', 'claudio', 'jesé', 'paulo' ]

const idades = users.map((idades) => idades.idade)
console.log(idades)
// [ 25, 23, 13, 48 ]

```

## <a name="REDUCE"></a> reduce()
> O reduce busca reduzir um array. Ele iterará por cada elemento dessa lista com o objetivo de ao final gerar um único valor.
```javascript 
const rockets = [
	{país: 'russia', lançamentos: 32},
	{país: 'us', lançamentos: 23},
	{país: 'china', lançamentos: 16},
	{país: 'europa', lançamentos: 7},
	{país: 'india', lançamentos: 32},
	{país: 'japão', lançamentos: 2},
]

const totalLançamentos = rockets.reduce((anterior, atual) => anterior + atual.lançamentos, 0)

console.log(totalLançamentos)

// 112
```

## <a name="FILTER"></a> filter()
> Cria um novo array com todos os elementos que passaram no teste da função fornocida.
``` javascript
let produtos = [ 
	{nome: 'Coca Cola', preco: 5}, 
	{nome: 'Pizza', preco: 15}, 
	{nome: 'Kinder Ovo', preco: 99} 
  ];
  
  let produtosBaratos = produtos.filter(function(produto) {
	return produto.preco < 20;
  });
  
  console.log(produtosBaratos);
  
  // [ { nome: 'Coca Cola', preco: 5 }, { nome: 'Pizza', preco: 15 } ]
```
- [Início](#inicio)

<hr>

## <a name="promise"></a> Promise
> Promise representa um valor que pode ta disponivel agora, no futuro ou nunca.

> New Promise é uma função; Recebe função como parametro: "resolve" e "reject".

> Para acesssar o valor de "resolve" usa-se .then(); Para acessar o valor de "reject" usa-se .catch().
```javascript
const umaPromise = new Promise((resolve, reject) => {
    const umNumero = 89
    if(umNumero === 80){
        resolve('O número é igual a 80')
    } else {
        reject('O número não é 80')
    }
})

umaPromise
    .then(resolveValue => console.log(resolveValue))  // 
    .catch(rejectValue => console.log(rejectValue))   // O número não é 80
```
- [Início](#inicio)

<hr>

## <a name="async"></a> Async Await
> Async faz uma função retornar uma promessa

> Await faz uma função esperar por uma promessa.
```javascript
function esperarPor(tempo = 2000){
    return new Promise(function(resolve){
        setTimeout(() => resolve(), tempo)
    })
}

async function executar(){
    await esperarPor(5000)  // irá esperar 5 segundos para executar o console log 
    console.log('Await 1')

    await esperarPor(1500)  // irá esperar 1,5 segundos para executar o console log 
    console.log('Await 2')

    await esperarPor(3000)  // irá esperar 3 segundos para executar o console log 
    console.log('Await 3')
}

executar()
```
- [Início](#inicio)

<hr>

## <a name="fetch"></a> Fetch
> Fazendo requisão com fetch
```javascript
fetch(url)
    .then(resp => resp.jscon())
```


 

 
 
 
 


 
 
 
