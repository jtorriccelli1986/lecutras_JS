Declaración de variables


# Variables
La variables en Js son contenedores para almacenar información que vamos a utilizar posteriormente.

JavaScript es un lenguaje de programación con el ámbito global como ámbito, visibilidad o scope predeterminado,Esto significa que una variable declarada fuera de una función es una variable global, por ejemplo:


`````````javascript
var texto = "global";

function actualizar() {
    texto = "local";
    console.log(texto); // local
}

actualizar();

console.log(texto); // local


`````````

En código anterior , podemos apreciar como la variable texto es una variable de ámbito global definida inicialmente fuera de la función es modificada dentro de la función;

Sin Embargo si declaramos la variable Texto con var tanto al inicio como dentro de la función , se va a generar una variable local cuyo ambito se reduce a la propia función donde ha sido declarada;


`````````javascript
var texto = "global";

function actualizar() {
    var texto = "local";
    console.log(texto); // local
}

actualizar();

console.log(texto); // global

`````````



# Declaraciones con let y const

## Let
El uso de let al momento de declarar una variable nos permite poder tener un mejor control sobre la declaración de la misma a medida que desarrollamos nuestra aplicación , esto debido a que el uso de let nos va a generar un error si queremos volver a declarar una variable con el mismo nombre, por ejemplo:

`````````javascript
let nombres="Juan carlos";
let nombres="Diego"
`````````

Si ejecutamos el codigo estos nos va a generar un error indicando lo siguiente Uncaught SyntaxError: Identifier 'nombre' has already been declared , esto debido a que el uso de let no permite que la variable pueda ser declara nuevamente.


Un bloque en JavaScript se puede entender como “lo que queda entre dos corchetes”, ya sean definiciones de funciones o bloques if, while, for y loops similares. Si una variable es declarada con let en el ámbito global o en el de una función, la variable pertenecerá al ámbito global o al ámbito de la función respectivamente, de forma similar a como ocurría con var.

`````````javascript

let i = 0;
function recorrer() {
    i = 1;
    let j = 2;
    if(true) {
        console.log(i); // 1
        console.log(j); // 2
    }
}
recorrer();
`````````

Por ejemplo, en el código de ejemplo la variable i es una variable global y la variable j es una variable local.

Sim embargo si declaramos una variable con let dentro un bloque que a su vez está dentro de una función, la variable pertenece solo a ese bloque:

`````````javascript
function foo() {
    let i = 0;
    if(true) {
        let i = 1; // Sería otra variable i solo para el bloque if
        console.log(i); // 1
    }
    console.log(i); // 0
}
foo();

`````````

Por otro lado fuera del bloque donde se declara con let la variable no esta definida
`````````javascript

function foo() {
    if(true) {
        let i = 1;
    }
    console.log(i); // ReferenceError: i is not defined
}
foo();
`````````

### recordar
* no permite redaclarar variables
* posee un scope (no puedo acceder a una variable declarada dentro de una función desde fuera de la función)
* el scope es de tipo bloque (todo lo que este dentro de llaves)


## Const
con respecto a la declaración de variables usando const se comporta de manera muy parecida a let.
El ámbito o scope para una variable declarada con const es al igual que con let también evita la redeclaración de variables por otro lado la declaración de variables con sont directamente prohíbe la reasignación de valores.


con un let la variable puede ser reasignada, ejemplo:

`````````javascript
function foo() {
    let i = 0;
    if(true) {
        i = 1;
     }
     console.log(i); // 1
}
foo();
`````````

sim embargo si usamos la declaración con const no es posible; si se intenta reasignar una variable constante se obtendrá un error tipo TypeError:

`````````javascript
const i = 0;
i = 1; // TypeError: Assignment to constant variable
`````````

### recordar
* no permite redaclarar variables
* posee un scope (no puedo acceder a una variable declarada dentro de una función desde fuera de la función)
* el scope es de tipo bloque (todo lo que este dentro de llaves)
* las constanste tienen un valor constante que nunca va a cambiar , esto lo podemos usar para variables que sabemos que en el transcurso de mi aplicación no va a cambiar (esto no aplica para los arreglos);




### Hoisting
El concepto de Hoisting fue pensado como una manera general de referirse a cómo funcionan los contextos de ejecución en JavaScript (específicamente las fases de creación y ejecución). En otras palarbas el Hositing hace que todas las declaracion de variables pase por un "levantamiento" hasta el inicio del ambito de aplicación , pero la asignación de valor permanece en el sitio donde se realice. 

Por ejemplo:

`````````javascript
console.log(dato)  // devuelve como valor undefined
var dato="hola"

`````````
El resultado del código anterior nos permite enender que la variable daos ha sido declarada pero al momento de acceder a ella no tenia ningún valor.

Teniendo en cuenta el concepto de Hositing lo que estaría sucediendo es lo siguiente:

`````````javascript
var dato  // Hoisting en acción
console.log(dato)  // devuelve como valor undefined
var dato="hola"

`````````

Tener encuenta que la caracteristica del hositing es solo aplicable para las declaracio de variables con var

Esto también sucede con las funciones por ejemplo:


`````````javascript
nombreDelGato("Dumas");

function nombreDelGato(nombre) { 
  console.log("El nombre de mi gato es " + nombre);
}

`````````

Como se puede observar, aunque primero llamamos a la función en el código, antes de que sea escrita, el código aún funciona. Esto sucede por la manera en la que el contexto de ejecución trabaja en JavaScript. 


Por último un ejemplo de como el hoisting afecta solo la declaración de la variables más no la inicialización. el valor será asginado cuando la setencia sea aclanzada.


`````````javascript
var x = 1; // Inicializa x
console.log(x + " " + y); // '1 undefined'
var y = 2; Inicializa y

`````````


## Resumen 
* var declara una variable de scope global o local para la función sin importar el ámbito de bloque. Permite hoisting.
* let declara una variable de scope global, local para la función o de bloque. Es reasignable y no permite hoisting.
* const declara una variable de scope global, local para la función o de bloque. No es reasignable, pero es mutable. No permite hoisting.
* puedes usar var, let o const para programar , pero actualmente ya no debemos usar var ya que esto nos puede llevar a cometer errores ante la posiblidad de poder redeclarar las variables.