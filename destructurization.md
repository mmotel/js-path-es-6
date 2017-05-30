# Destrukturyzacja

Składnia ES6 pozwala na przypisanie destrukturyzujące tablic oraz obiektów.

## Tablica

W ES5 aby przypisać do zmiennych elementy tablicy należało zrobić trzema osobnymi przypisaniami. 

##### Przykład 5.1
```js
let numbers = [1, 2, 3];
let first  = numbers[0];
let second = numbers[1];
let third  = numbers[2];
```

Dzięki nowej składni możemy dokonać tego prościej.

##### Przykład 5.2
```js
let [first, second, third] = [1, 2, 3];
console.log(first);  // -> 1
console.log(second); // -> 2
console.log(third);  // -> 3
```

Jeśli spróbujemy pobrać do zmiennej element tablicy, którego w niej nie ma zwrócona zostanie wartość `undefined`.

##### Przykład 5.3
```js
let [first, second, third] = [1, 2];
console.log(first);  // -> 1
console.log(second); // -> 2
console.log(third);  // -> undefined
```

Możemy również wykorzystać parametr resztowy aby pobrać do jednej zmiennej pozostałe elementy tablicy.

##### Przykład 5.4
```js
let [first, ...other] = [1, 2, 3];
console.log(first); // -> 1
console.log(other); // -> [2, 3]

## Obiekt

```js
let foo = { bar: 'bar' };

let { bar: fooBar } = foo;

console.log(fooBar); // -> 'bar' 
```

```js
let foo = { bar: 'bar' };

let { bar } = foo;

console.log(bar); // -> 'bar'
```

```js
let { foo = 'bar' } = {}

console.log(foo); // -> 'bar'
```

```js
function foo ({first, second, third}) {}

function bar ({first=1, second=2, third=3}) {}
```

---

###### Źródła

* http://shebang.pl/artykuly/destrukturyzacja/