# Destrukturyzacja

## Tablica

```js
let [first, second, third] = [1, 2, 3];
console.log(first);  // -> 1
console.log(second); // -> 2
console.log(third);  // -> 3
```

```js
let [head, ...tail] = [1, 2, 3];
console.log(head); // -> 1
console.log(tail); // -> [2, 3]
```

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
