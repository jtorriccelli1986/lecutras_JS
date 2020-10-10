# Funciones
Las funciones son fragmentos de codigo que vamos a poder usar las veces que necesitemos , las funciones se creean con la idea de factorizar codigo que vamos a reutilizar dentro de nuestro código.

## Tradicionales

Las funciones pueden ser de los siguientes tipos: 
con parametros, sin parametros, con retorno y sin retorno. Tener en cuenta que no debemos confundir la creación de la función con el uso de la función.

un ejemplo de como podemos definir una función es el siguiente:

`````````javascript
 //a continuación  se declara la función
function actualizacion(intento){
	intento++
}

 //en esta linea estamos usando/llamando a la función

actualizacion()
`````````

En Javascript, las funciones se pueden crear a través de una declaración de función, o una expresión de función.

Declarar una función es la forma más común de crear una función con nombre:

`````````javascript
// Declaración de una función con nombre
function myFunction() { /* código aquí */ }
`````````

Por otro lado, si estás asignando una función a una variable o a una propiedad, estás tratando con una expresión de función.

`````````javascript
// Asignar una expresión de función a una variable
var myFunction = function () { /* código aquí */ };

// Asignar una expresión de función a una propiedad
var myObj = {
    myFunction: function () { /* código aquí */ }
};
`````````



tener en cuenta que bajo lo indicado notemos como el trabajar con una declaración ó una expresión de función:


`````````javascript
// esto funciona 
console.log(suma(2,2));
function suma (a,b) {
return a+b;

}


//esto no funciona

console.log(suma(2,2));
var suma= function (a,b) {
    return a+b;

}
`````````

## Flecha

Declaraciones de tipo feclhas son una nueva manera de declarar las funciones la cual a su vez tiene diferentes formas de poder ser declaradas, dependiendo en la mayoria de casos de los que quieras realizar.

Todas las variaciones comienzan con los argumentos de la función, seguidos por la flecha, seguidos por el contenido de la función. Tanto los argumentos como el contenido pueden tener diferentes formas dependiendo de su uso.

Veamos algunos ejemplos que nos ayuden a entender como funciona:


`````javascript
(parametro)=>{
	console.log(paremtro)
}
`````

en el ejemplo siguiente podemos ver una función de tipo felcha que retorna su mismo valor  y su equivalente en JS

``````javascript
var data = value => value;

// Que sería lo mismo que hacer esto:
var data = function (value) {
  return value;
};

``````
Del ejemplo mostrado anteriormente definimos lo siguiente con respecto a la función de tipo flecha:

* cuando la función recibe un solo parametro no necesita parentisis
* en una sola linea no es necesario declarar el return ya que la función flecha retorarnara el primer argumento que encuentre.

Para el caso que la función reciba más de un argumento entonces si debemos hacer uso de los parentisis :

``````javascript
var sum = (n1, n2) => n1 + n2;

// Que sería lo mismo que hacer esto:
var sum = function (n1, n2) {
  return n1 + n2;
};
``````

En el caso que la función no reciba ningún parametro se usan los paréntisis solos

``````javascript
var getName = () => "Luis Miguel";

// Que sería lo mismo que hacer esto:
var getName = function () {
  return "Luis Miguel";
};
``````

Pero debemos tener en cuenta y muy claro que no es la unica forma que tenemos para declarar una función de tipo flecha y podemos decir que recurrimos de una otra manera a una sintaxis más tradicional.
Esto sucede para el caso que nuestra función realiza más tareas debemos encapsular nuestro contenido entre llaves y usar explicitamente el return en nuestra función
``````javascript
var sum = (n1, n2) => {
  return n1 + n2;
};

// Que sería lo mismo que hacer esto:
var sum = function (n1, n2) {
  return n1 + n2;
};
``````
 en este caso vemos claramente que trabajamos como si lo hicieramos de manera tradicional , pero lo que debemos de tener en cuenta es que el valor arguments no se encontara disponible.


 para el caso que queramos que nuestra función returno un objeto  y queramos trabajar en una sola linea debemos tener en cuenta que nuestra función de flecha quedaría de la siguiente manera.

``````javascript
var getTempItem = id => ({id: id, name: "Temp"});

// Que sería lo mismo que hacer esto:
var getTempItem = function (id) {
  return {
    id: id,
    name: "Temp"
  };
};
``````

Esto se hace por que al encapsular el objeto entre paréntesis declaramos que las llaves son el objeto y no que pertenecen al cuerpo de la función.




## IIEFs (Immediately-invoked function expressions)

``````javascript
(function () {
    // algún código aquí
})();
``````



## Palabra reserva This
 
La palabra clave this tiene en Javascript un comportamiento diferente al de otros lenguajes pero por lo general, su valor hace referencia al propietario de la función que la está invocando o en su defecto, al objeto donde dicha función es un método. pero debe estar referenciada a un objeto, en caso no tenga un objeto de referencai sera hara referencia al objeto window;


por ejemplo:
``````javascript
function llamado(){
	console.log(this.name)
}

var persona1={
	nombre="juan carlos",
	ver_nombre=llamado
}

var persona2={
	nombre="Diego",
	ver_nombre=llamado	
}


persona1.ver_nombre();
``````


Como vemos el valor de this cambia según sobre que objeto lo llamemos. Bien, Javascript sabe que valor tiene que poner a this antes de llamar a una función, pero nosotros necesitamos entenderlo para no encontrarnos con bugs imposibles de corregir. Para ésto hay una regla de oro: el objeto this pasado a una función es el objeto que está antes del punto que precede los paréntesis que invocan a la función. Es decir, la llamada objectA.myMethod() la podríamos dividir en cuatro partes:
* objectA: El objeto que contiene la función
* **. (punto)**: Separa el objeto de su propiedad (la función)
* myMethod: Nombre de la función
* () (paréntesis): Ejecutan la función En éste caso vemos que

antes del punto está objectA por lo que será objectA lo que se le pasará a la variable this del método myMethod.

Pero que pasa si no hay ningún punto? si la función no está en ningún objeto?

``````javascript
function testScope() {
  console.log(this);
}
testScope();
``````

Aquí podríamos pensar que this es null y tendría sentido pero no, Javascript define que una función invocada sin contexto, el contexto debe ser el Objeto Global, que en el caso de un navegador sería window. Por lo que en una función que no esté contenida en ningún objeto recibirá el objeto global como this.

Pero que pasa cuando hacemos el llamado a una función que no esta asociada a un objeto , veamos el siguiente escenario

``````javascript

var alice = {
  nombre: "Alice",
  cansarse: function() {
    console.log(this.nombre);
  }
};

var myFunction = alice.cansarse;

myFunction();


``````

Si llamamos a myFunction directamente lo estaríamos llamando sin contexto por lo el la variable this tendría el objeto global dentro de myFunction, como podemos hacer que ejecute myFunction pero pasándole alice como this? Para ésto tenemos las funciones .call() y .apply(), empecemos por la función .call().

### call
La función .call() recibe los mismos argumentos que la función mas uno, el valor que tendrá this que se pasa antes que los demás argumentos. Es decir, nuestra función myFunction no recibe ningún argumento así que si llamamos a su método .call() y le pasamos lo que queremos que sea this es decir, alice conseguiremos que el método funcione igual que si lo hubiésemos llamado con alice.cansarse


``````javascript
// como la función no recibe parametros solo se pasa el un parametro que en este caso sera el objeto que queremos que sea el contexto dentro de la función

myFunction.call(alice);

// en el caso que la función tenga parametros tendriamos lo siguiente

myFunction.call(alice,parametro1,parametro2);


``````


### apply

El método .apply() actúa de forma bastante similar a .call(), pero con una variación, solo recibe dos argumentos, el primero es el contexto de la función, el valor de this y el segundo será un array que contendrá los argumentos que se le pasarán a la función, veamos su uso en el ejemplo anterior:
``````javascript
myFunction.apply(alice, [ "Bob", "Rob" ]);


function callWithAlice() {
  alice.saludar.apply(alice, arguments);
}
callWithAlice("Rob", "Bob");

``````

Esto aunque en un principio parezca bastante inútil nos servirá cuando, queriendo o no cambiar el contexto de una función, querramos llamarla y no sepamos ni nos interese saber cuántos argumentos tiene, supongamos que tenemos la función callWithAlice() que llama a la función .saludar() de alice y le pasa todos los argumentos que recibe.

observación:Para ésto hace falta aclarar que el objeto arguments es una especie de array con los argumentos pasados a la función, más adelante profundizaremos en ello.


### bind

El método .bind() recibe un argumento, el contexto que se le podrá a la función sobre la que se aplica el .bind() y devolverá una función que cuando sea llamada ejecutará la función original con el contexto que se le pasó a .bind(). Lo veremos mejor con un ejemplo:

``````javascript
var alice = {
  nombre: "Alice",
  saludar: function() {
    console.log("Hola! Soy " + this.nombre);
  }
};

var myFunction = alice.saludar.bind(alice);
myFunction();

``````


## Argumentos


### Parametros Rest
El operador rest es una característica de JavaScript ES6 que nos permite evitar el trabajo repetitivo en las funciones con el tratamiento de parámetros. Gracias a ES6, podemos definir valores predeterminados a las funciones, aunque no solo se limita a esto, sino que el operador rest nos va a permitir obtener un número indefinido de parámetros de forma estructurada a través de un array de valores. En este artículo, explicamos cómo utilizarlo, ya que nos permite acortar y simplificar los códigos que se utilizaban antes para obtener cualquier número de argumentos en una función. (se utiliza en la declaración de una función)

`````javascript
// uso básico del operador Rest
function max(...numeros) {
   console.log(numeros);
 }

`````
En este ejemplo, lo que indicamos es que cualquier cantidad de parámetros que se envíen al invocar la función se estructurará como un array y dentro de la función se conocerá con el nombre de “numeros”. De este modo, podremos invocar a la función con el número de parámetros que queramos, teniendo siempre en el parámetro numero un array, con el número de casillas deseado.
Para comprobar esto, basta con invocar a la función anterior utilizando el juego de parámetros que deseemos:

`````javascript
 max("test", 4, true, 2000, "90");
 // en este caso el manejo de los parametros ingresados será en base a un arreglo 
 `````

Los parámetros a los que no hemos asignado un nombre son los que el operador rest nos va a ofrecer en el array. Por tal motivo, en una función podremos recibir un número de parámetros en variables normales, pero también recibir cualquier número de parámetros en un array gracias al operador rest.


`````javascript
function max(max = 0, ...numeros) {
  for(let i = 0; i < numeros.length; i++) { if(numeros[i] > max) {
      max = numeros[i];
    }
  }
  return max;
}
 `````

 En el siguiente ejemplo vamos a recibir cualquier número de parámetros y comprobaremos si el primero de los parámetros se repite en los parámetros que se indican posteriormente:

`````javascript
function enLista(buscar, ...nombres) {
  for(let i = 0; i < nombres.length; i++) {
    if(buscar === nombres[i]) {
      return true;
    }
  }
  return false;
}
console.log(enLista('José', 'Álvaro', 'María', ' José ')); // muestra true
console.log(enLista(' José ', ' Álvaro ', ' María ', 'Manolo')); // muestra false
 `````


### Parametros Spread

Spread, el nuevo operador de propagación que ofrece JavaScript ES6, nos resultará de ayuda para ahorrar líneas de código, ya que genera una lista de valores a partir de un array y es un excelente recurso para mejorar el código JavaScript

Al igual que el operador rest, del que hablamos hace poco en este artículo, utiliza la misma sintaxis de los tres puntos seguidos.

`````javascript
// pasamos los parametros 1 por 1
Math.min(3, 5, 7, 2, 9);


// usamos el operador spread

cons valores=[2,3,4,56,7]
Math.min(...valores);

// tener en cuenta que no es lo mismo usar el arreglo de manera directa en el metodo Min , esto generaría un error en la ejecución
cons valores=[2,3,4,56,7]
Math.min(valores);
`````

esto puede parecer confuso pero debemos de tener en cuenta que es como el conocido operador rest, pero lo invocamos en una función.


Vamos a ver como podemos combinar el uso de los operadores spred y rest

Vamos a poner como ejemplo una función que admite cualquier cantidad de cadenas por parámetro y devuelve un array con esas mismas cadenas, eliminando los espacios vacios de antes y después.

`````javascript
// declaramos la función usando el operador REST
function EliminarEspacios(...cadenas) {
   for (let i=0; i < cadenas.length; i++) {
     cadenas[i] = cadenas[i].trim();
   }
   return cadenas;
 }

 // ahora hacemos uso de la función

let limpiandoCadenas = EliminarEspacios('aquí ', ' lados ', ' espacio');
 console.log(limpiandoCadenas);


 // pero que pasa si en vez de una cadena queremos pasar un array 
 const cadenasOriginales = ['aquí ', ' lados ', ' espacio'];
 let limpiandoCadenas = EliminarEspacios(cadenasOriginales); // devuleve un error

// para poder solucionar este inconveniente podemos usar el operador spread

const cadenasOriginales = ['aquí ', ' lados ', ' espacio'];
 let limpiandoCadenas = EliminarEspacios(...cadenasOriginales); // el array se convertira en una lista de parametros que es lo que requiere la función.

`````

let limpiandoCadenas = EliminarEspacios('aquí ', ' lados ', ' espacio');
 console.log(limpiandoCadenas);


para entender los parametros 
Rest parameter funciona en la declaración de la funcion.
Spread operator funciona cuando se usa en la ejecución.