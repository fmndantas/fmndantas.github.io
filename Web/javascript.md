[TOC]

# javascript cheatsheet

 - [documentação](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference)

## variáveis
### declaração

```javascript
// usar let quando a variável for criada sem valor ou quando trocará de valor ao longo da execução
let a;
a = 10;

// usar const quando quando a variável terá valor constante e sabe-se seu valor no momento da declaração, pois o assignment é obrigatório
const a = 20;

// var tem escopo global, o que não é muito desejável. é melhor usar let e const
var a = 30;
```

### interpolação de strings

```javascript
const name = 'fernando';
console.log(`name = ${name}`) // "name = fernando"
```

### checar tipo da variável

```javascript
const numero = 10;
const string = "string";
console.log(typeof numero); // number
console.log(typeof string); // string
```

## controles de fluxo

### operador identidade
```javascript
1 == true // true (true eh representado como 1, mas os tipos são diferentes)
1 === true // false (operador identidade. checa igualdade de valor e de tipos)
```

### shorthand pra assign de string
```javascript
let name;
let defaultName = name || "stranger"; // stranger
name = "fernando";
defaultName = name || "stranger"; // fernando
```

### if-else

```javascript
if (condition) {
	// true
} else {
	// false
}

condition ? /* true */ : /* false */; // operador ternário
```

### switch
```javascript
let condition = "case1";
switch (condition) {
	case "case1":
		break;
	default: 
		break;
}
```

## funções

### declaração

```javascript
// forma padrão
function foo(parameter1, ..., parameterN) {
    // body
    return result;
}

// function expression: função não tem nome e é armazenada numa variável
const foo = function(parameter1, ..., parameterN) {
    // body
    return result;
}
```

### arrow function

```javascript
const foo = (parameter1, ... parameterN) => {
    // body
    return result;
}

// somente um parâmetro dispensa ()
const foo = singleParameters => {
    // body
    return result;
}

// se o body não contém {}, o que a única linha que compõe a função avaliar será retornado automaticamente (retorno implícito)
const foo = (parameter1, ..., parameterN) => parameter1 + ... + parameterN;
```

## escopo

```javascript
/* evitar muitas variaveis globais porque pode haver conflito entre escopo global e local */
const globalScope = "variavel acessivel de qualquer lugar"
function foo() {
    let blockScope = "variavel acessivel somente dentre de foo"
}
console.log(blockScope) // reference error
```

## arrays

```javascript
const a = ["item"]         // permite atualizacao do elemento, mas impede reassign de a
let a = ["item1", 10, -2]; // declaracao literal
a[0];                      // acessa o primeiro elemento
a[0] = 12;                 // atualiza elemento
a.length                   // tamanho de a. nesse caso, 3
a.push(1, 2, 3)            // adiciona os elementos passados como parametros ao array
const b = a.pop()          // remove o ultimo elemento de a armazena em b
a.shift()                  // remove o primeiro elemento do array
a.unshift("ola")           // adiciona ola como primeiro elemento do array
a.slice(0, 4)              // retorna o array entre [0, 4[ (ultimo elemento nao incluído)
a.indexOf(item)            // retorna o indice do elemento ou -1 se nao tiver presente
```

## loops

```javascript
for (let i = 0; i < 10; ++i) { /* ... */}
while (condition) { /* ... */ }           // roda enquanto condition == true 
do { /* ... */ } while (condition)        // roda no mínimo uma vez
```

## funções de ordem superior

- aceitam funcoes como argumentos ou retornam funcoes
- funcoes em js se comportam como qualquer outro objeto

```javascript
/* tratamento de funcao como objeto */
function foo() { }
let atalho = foo;
atalho()                 // igual a foo()
console.log(atalho.name) // foo


/* funcoes de ordem superior: recebem e/ou retornar funcoes como argumentos */
const foo = funcao => {
    console.log("chamando funcao passada como parametro");
    console.log(funcao());
}
foo(() => "valor qualquer"); // foo executa a funcao anonima passada e imprime o valor
```

## iteradores

- mesma idéia dos iteradores do `Python3`

```javascript
const array = [/* ... */];
array.forEach(element => console.log(element));       // itera sobre os elementos
array.map(element => 2 * element);                    // transforma os elementos por 2
array.filter(element => typeof element === "number"); // mantém só elementos que dão true
array.findIndex(element => element === 1);            // retorna o primeiro elemento = 1
array.reduce((accumulator, element) => accumulator + element, initialValue) /* soma os elementos de um array, mantendo um acumulador. initialValue é um valor inicial a partir do qual o acúmulo é realizado */
```

## objetos

- coleção de pares *key-value*
- um objeto é uma coleção de pares rodeados de chaves ( `{}` )

```javascript
let emptyObject = {};           // declara um objeto vazio

let primitiveObject = {
    key1: value1,               // chave não tem nenhum caractere especial => sem aspas!
    "this is key2": value2
}

primitiveObject.key1;           // retorna value1
primitiveObject[key1]           // também retorna value1

primitiveObject.key1 = value2;  // atualiza valor de key1
primitiveObject[key1] = value2; // atualiza valor de key2

primitiveObject.newPrp = value; // cria nova propriedade chamada newPrp on-the-fly 
delete primitiveObject.newPrp;  // remove propriedade key1

primitiveObject = {
    print: (msg) => {           // cria método no objeto
        console.log(msg);
    }
}
```

- objetos são passados por referência (endereço de memória) às funções

```javascript
const foo = (obj) {
obj.color = 'yellow';
}

let obj = { color: 'blue' };
console.log(obj); // imprime 'blue'
foo(obj);
console.log(obj); // imprime 'yellow'
```

- iterar sobre objetos

```javascript
let eu = {
    nome: "fernando",
    idade: 21,
};

for (let it in eu) {
    console.log(`${it}: ${eu[it]}`);
}

/*
	"nome: fernando"
	"idade: 21"
*/
```

## fetch API

## web

### adicionar callback para uma tag html

```javascript
const callback = () => { }
let tag = document.getElementById("tagId");
tag.addEventListener("eventName", callback);
```

###  verificar se houve algum input em um input de texto

```javascript
inputText.addEventListener('input', callback)
```

### impedir que enter dê submit no form em um text input

```javascript
inputText.addEventListener('keypress', e => {
    if (e !== null && e.keyCode === 13) {
        e.preventDefault(); // não acontece nada quando enter é apertado
    }
})
```

### desativar botão pelo javascript

```javascript
button.disabled = true
```