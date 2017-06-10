# Przyszłość - ES7, ES8, ...

Kolejne wersje standardu ECMAScript przyniosą sporo ciekawych funkcjonalności. Poniżej lista kilku najciekawszych z nich.

### `Array.prototype.includes()` `ES7`

Obecnie aby sprawdzić czy element znajduje się w tablicy trzeba skorzystać z metody `Array.indexOf()`.

```js
let numbers = [1, 2, 3];

let containsOne = numbers.indexOf(1) > -1;

console.log(containsOne); // -> true
```

Nowa metoda `Array.includes()` pozwoli na prostszy zapis.

```js
let numbers = [1, 2, 3];

let containsOne = numbers.includes(1);

console.log(containsOne); // -> true

```

### Operator potęgowania `ES7`

Obecnie aby podjeść `x` do potęgi `y` należy wykorzystać metodę `Math.pow()`.

```js
let x = 2;
let y = 3;
let result = Math.pow(x,y);

console.log(result); // -> 8
```

Będziemy mogli zapisać tę operację prościej wykorzystując operator `**`.

```js
let x = 2;
let y = 3;
let result = x ** y;

console.log(result); // -> 8
```

### Operator `spread`

Operator `spread` jest przeciwieństwem operatora resztowego.

```js
let [a, ...b] = [1, 2, 3];

console.log(a); // -> 1
console.log(b); // -> [2, 3]

let numbers = [a, ...b];

console.log(numbers) // -> [1, 2, 3];
```

Operator `...` pozwala podzielić tablicę na pojedyncze elementy.


### Dekoratory


### Funkcje `async/await`


### Opcjonalne anotacje typów

---

###### Źródła

* https://www.quora.com/What-features-will-be-in-ES7-and-ES8
* http://shebang.pl/artykuly/es6-bez-tajemnic-przyszlosc/