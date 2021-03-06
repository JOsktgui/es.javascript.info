# Tipos de datos

Una variable en JavaScript puede contener cualquier dato. Una variable puede ser una cadena en un momento dado y en otro, un número:

```js
// no hay error
let message = "hola";
message = 123456;
```

Los lenguajes de programación que permiten estas cosas se denominan "dinámicamente tipeados", lo que significa que hay tipos de datos, pero las variables no están vinculadas a ninguno de ellos.

Hay siete tipos de datos básicos en JavaScript. Aquí, los cubriremos en general y en los próximos capítulos hablaremos de cada uno de ellos detalladamente.

## Un número
```js
let n = 123;
n = 12.345;
```

El tipo *número* representa tanto números enteros como de punto flotante.

Hay muchas operaciones para números, por ejemplo, multiplicación `*`, división `/`, suma `+`, resta `-`, y demás.

Además de los números comunes, existen los llamados "valores numéricos especiales" que también pertenecen a este tipo de dato: `Infinity`, `-Infinity` and `NaN`.


- `Infinity` representa el [Infinito](https://es.wikipedia.org/wiki/Infinito) matemático ∞. Es un valor especial que es mayor que cualquier número.

    Podemos obtenerlo como resultado de la división por cero:

    ```js run
    alert( 1 / 0 ); // Infinito
    ```

    O simplemente hacer referencia a ello directamente:

    ```js run
    alert( Infinity ); // Infinito
    ```
- `NaN` representa un error de cálculo. Es el resultado de una operación matemática incorrecta o indefinida, por ejemplo:

    ```js run
    alert( "no es un número" / 2 ); // NaN, tal división es errónea
    ```

    `NaN` es pegajoso. Cualquier otra operación sobre `NaN` retorna `NaN`:

    ```js run
    alert( "no es un número" / 2 + 5); // NaN
    ```

    Por lo tanto, si hay un `NaN` en alguna parte de una expresión matemática, se propaga a todo el resultado.

```smart header="Las operaciones matemáticas son seguras"
Hacer matemáticas es "seguro" en JavaScript. Podemos hacer cualquier cosa: dividir por cero, tratar las cadenas no numéricas como números, etc.

El script nunca se detendrá con un error fatal ("morir"). En el peor de los casos, obtendremos `NaN` como resultado.
```

Los valores numéricos especiales pertenecen formalmente al tipo "número". Por supuesto que no son números en el sentido estricto de la palabra.

Veremos más sobre el trabajo con números en el capítulo <info:number>.

## Una cadena

Una cadena en JavaScript debe estar encerrada entre comillas.

```js
let str = "Hola";
let str2 = 'Las comillas simples también están bien';
let phrase = `puede incrustar ${str}`;
```

En JavaScript, hay 3 tipos de comillas.

1. Comillas dobles: `"Hola"`.
2. Comillas simples: `'Hola'`.
3. Backticks (acento grave): <code>&#96;Hola&#96;</code>.

Las comillas dobles y simples son comillas "simples". No hay diferencia entre ellas en JavaScript.

Los Backticks son comillas de "funcionalidad extendida". Nos permiten incrustar variables y expresiones en una cadena encerrándolas en `${...}`, por ejemplo:

```js run
let name = "Juan";

// incrustar una variable
alert( `Hola, *!*${name}*/!*!` ); // Hola, John!

// incrustar una expresión
alert( `el resultado es *!*${1 + 2}*/!*` ); //el resultado es 3
```

La expresión dentro de `${...}` se evalúa y el resultado pasa a formar parte de la cadena. Podemos poner cualquier cosa ahí dentro: una variable como `name`, una expresión aritmética como `1 + 2`, o algo más complejo.

Tenga en cuenta que esto sólo se puede hacer en los "backticks". Otras comillas no tienen esta capacidad de incrustación!
```js run
alert( "el resultado es ${1 + 2}" ); // el resultado es ${1 + 2} (las comillas dobles no hacen nada)
```

En el capítulo <info:string> trataremos más a fondo las cadenas.

```smart header="No existe el tipo *carácter*".
En algunos idiomas, hay un tipo especial "carácter" para un solo carácter. Por ejemplo, en el lenguaje C y en Java es `char`.

En JavaScript no existe tal tipo. Sólo hay un tipo: `string`(cadena). Una cadena puede estar formada por un solo carácter o por varios de ellos.
```

## Un booleano (tipo lógico)

El tipo booleano tiene sólo dos valores: `verdadero` y `falso`.

Este tipo se utiliza comúnmente para almacenar valores de sí/no: `verdadero` significa "sí, correcto", y `falso` significa "no, incorrecto".

Por ejemplo:

```js
let nameFieldChecked = true; // sí, el campo name está marcado
let ageFieldChecked = false; // no, el campo age no está marcado
```

Los valores booleanos también son el resultado de comparaciones:

```js run
let isGreater = 4 > 1;

alert( isGreater ); // verdadero (el resultado de la comparación es "sí")
```

En el capítulo <info:logical-operators> trataremos más a fondo el tema de los booleanos.

## El valor "null" (nulo)

El valor especial `null` no pertenece a ninguno de los tipos descritos anteriormente.

Forma un tipo propio separado que contiene sólo el valor `null`:

```js
let age = null;
```

En JavaScript, `null` no es una "referencia a un objeto inexistente" o un "puntero nulo" como en otros lenguajes.

Es sólo un valor especial que representa "nada", "vacío" o "valor desconocido".

El código anterior indica que la "edad" es desconocida o está vacía por alguna razón.

## El valor "undefined" (indefinido)

El valor especial `undefined` también se distingue. Hace un tipo propio, igual que `null`.

El significado de `undefined` es "valor no asignado".

Si una variable es declarada pero no asignada, entonces su valor es `undefined`:

```js run
let x;

alert(x); // muestra "undefined"
```

Técnicamente, es posible asignar `undefined` a cualquier variable:

```js run
let x = 123;

x = undefined;

alert(x); // "undefined"
```

...Pero no recomendamos hacer eso. Normalmente, usamos `null` para asignar un valor "vacío" o "desconocido" a una variable, y usamos `undefined` para chequeos como ver si una variable ha sido asignada.

## Objetos y símbolos

El tipo `object` (objeto) es especial.

Todos los demás tipos se llaman "primitivos" porque sus valores pueden contener una sola cosa (ya sea una cadena,  un número o lo que sea). Por el contrario, los objetos se utilizan para almacenar colecciones de datos y entidades más complejas. Nos ocuparemos de ellos más adelante en el capítulo <info:object> después de aprender más sobre los primitivos.

El tipo `symbol` (símbolo) se utiliza para crear identificadores únicos para los objetos. Tenemos que mencionarlo aquí para una mayor completitud, pero es mejor estudiar este tipo después de los objetos.

## El operador typeof [#type-typeof]

El operador `typeof` retorna el tipo del argumento. Es útil cuando queremos procesar valores de diferentes tipos de forma diferente o simplemente queremos hacer una comprobación rápida.

Soporta dos formas de sintaxis:

1. Como operador: `typeof x`.
2. Como una función: `typeof(x)`.

En otras palabras, funciona con paréntesis o sin ellos. El resultado es el mismo.

La llamada a `typeof x` devuelve una cadena con el nombre del tipo:

```js
typeof undefined // "undefined" (indefinido)

typeof 0 // "number" (número)

typeof true // "boolean" (booleano)

typeof "foo" // "string" (cadena)

typeof Symbol("id") // "symbol" (símbolo)

*!*
typeof Math // "object"  (1)
*/!*

*!*
typeof null // "object"  (2)
*/!*

*!*
typeof alert // "function"  (3)
*/!*
```

Las últimas tres líneas pueden necesitar una explicación adicional:

1. `Math` es un objeto incorporado (built-in) que proporciona operaciones matemáticas. Lo aprenderemos en el capítulo <info:number>. Aquí, sólo sirve como ejemplo de un objeto.
2. El resultado de `typeof null` es `"object"`. Esto es incorrecto, es un error oficialmente reconocido de `typeof` que se mantiene por cuestiones de compatibilidad. Por supuesto, `null` no es un objeto. Es un valor especial con un tipo propio separado. Así que, de nuevo, esto es un error en el lenguaje.
3. El resultado de `typeof alert` es `"function"`, porque `alert` es una función del lenguaje. Estudiaremos las funciones en los próximos capítulos donde veremos que no hay ningún tipo especial "function" en JavaScript. Las funciones pertenecen al tipo objeto. Pero `typeof` las trata de manera diferente. Formalmente, es incorrecto, pero muy conveniente en la práctica.


## Resumen

Hay 7 tipos básicos en JavaScript.

- `number` para números de cualquier tipo: enteros o en punto flotante.
- `string` para cadenas. Una cadena puede tener uno o más caracteres, no hay un tipo especial para un único carácter.
- `boolean` para `verdadero`/`falso`.
- `null` para valores desconocidos -- un tipo independiente que tiene un solo valor `nulo`.
- `undefined` para valores no asignados -- un tipo independiente que tiene un único valor `indefinido`.
- `object` para estructuras de datos más complejas.
- `symbol` para identificadores únicos.

El operador `typeof` nos permite ver qué tipo está almacenado en una variable.

- Dos formas: `typeof x` o `typeof(x)`.
- Retorna una cadena con el nombre del tipo, por ejemplo `"string"`.
- Para `null` retorna `"object"` -- esto es un error en el lenguaje, en realidad no es un objeto.

En los siguientes capítulos, nos concentraremos en los valores primitivos y una vez que nos familiaricemos con ellos, pasaremos a los objetos.
