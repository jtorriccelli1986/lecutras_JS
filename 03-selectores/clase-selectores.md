# Selectores

El uso de “selectores” en JavaScript permite encontrar y seleccionar elementos del DOM bien sea para extraer información de cada nodo o para manipularlos de ser necesario.

para poder realizar ese tipo de tarea tenemos un conjunto de posiblidad y debemos entender cada una de ellas para poder saber como actuar en cada situación

los selectores que tenemos disponbiles son los siguientes:
* Etiqueta o Tag 
* Clase
* ID
* QuerySelector
* QuerySelectorAll


### Selector de tipo etiqueta
Este selector nos devuelve un arreglo de elementos compuestos por todos los elementos que cumplan la condición

``````javascript
// esto devolvera a los elementos dentro del DOM de etiqueta "p" (array de elementos)
document.getElementBytag("p")

``````


### Selector de tipo clase
Este selector nos devuelve un arreglo de elementos compuestos por todos los elementos que cumplan la condición

``````javascript
// esto devolvera a los elementos dentro del DOM que contentan la clase "contendio" (array de elementos)
document.getElementsByClassName("contenido")

``````


### Selector de tipo id
Este selector nos devuelve un único elemento que cumplan la condición (en el caso que existan varios elementos , el selector devolvera el 1er elemento que encuentre)

``````javascript
// esto devolvera al elemento dentro del DOM que contenta el Id title
document.getElementById("title")

``````

### Selector de querySelector
Este selector nos devuelve el primer elemento que encuentre , se puede decir que es muy parecido al getElementById sin embargfo la caracteristica de este tipo de selector es que nos permite acceder a los elementos mediante selectores css .


``````javascript
// esto devolvera al elemento dentro del DOM que contenta el selector css #prueba .clase (elemento con la clase item dentro del elemento con el id prueba)
document.querySelector('#prueba .item')
``````


### Selector de querySelectorAll
El query querySelectorAll funciona igual que querySelector con la diferencia que nos devuelve todos los elementos que se cumplan con la condición:


``````javascript
// esto devolvera a todos los elementos dentro del DOM que contenta la clase item y se encuentren dentro de elemento que tenga id prueba
document.querySelectorAll('#prueba .item')

``````


con respecto a los selectores tenemos un pequeño detalle sobre como podemos usarlos a nuestro favor para acceder a elementos

* E#myid  un elemento E con ID igual a myid.
* E[foo]  un elemento E con un atributo foo
* E[foo="bar"]  un elemento E cuyo valor de atributo foo es exactamente igual a bar
* E[foo="bar" i] un elemento E cuyo valor de atributo foo es exactamente igual a cualquier permutación de caso (rango ASCII) de bar
* E[foo~="bar"] un elemento E cuyo valor de atributo foo es una lista de valores separados por espacios en blanco, uno de los cuales es exactamente igual a bar
* E[foo^="bar"] un elemento E cuyo valor de atributo foo comienza exactamente con el string bar
* E[foo$="bar"] un elemento E cuyo valor de atributo foo finaliza exactamente el string bar
* E[foo*="bar"] un elemento E cuyo valor de atributo foo contiene el substring bar

