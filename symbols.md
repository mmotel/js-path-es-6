# Symbole

Do momentu pojawienia się ES6 JavaScript posiadał sześć typów: `null`, `undefined`, `boolean`, `string`, `number` i `object`. Wraz z ES6 język zyskał nowy typ - `Symbol`.

 Symbol może być nazwą pola obiektu, nie można im również nadawać własności - cechy typu `string`. 
 
 ##### [Przykład 7.1](https://codepen.io/mmotel/pen/xrZNjj)
 ```js
 let name = Symbol('name');
 
 let obj = {};
 
 obj[name] = 10;
 
 console.log(obj[name]); // -> 10
 ```
 
Symbole nie są jednak zwykłymi napisami. Każdy utworzony symbol ma unikalną wartość a ich tworzenie nie sprawia żadnych problemów - cechy typu `object`. Po utworzeniu wartość sybmolu jest niemodyfikowalna. 

W odróżnieniu od pozostałych typów, wartości typu `Symbol` nie można automatycznie przekształcić na napis.

##### [Przykład 7.2](https://codepen.io/mmotel/pen/xrZNjj)
```js
let name = Symbol('name');

console.log('My name is ' + name); // -> typeError

console.log('My name is ' + name.toString()); 
```

## Do czego można wykorzystać symbole?

Załóżmy, że chcemy stworzyć funkcjonalność, która będzie zliczała wszystkie kliknięcia na stronie i zapisywała ich ilość w obiekcie `window` w polu `clicks`. Istnieje spora szansa, że kod z biblioteki czy też innego skryptu może również wykorzystywać to pole. Dodanie lub modyfikacja pola wykorzstywanego również przez inny kod może zakłócić lub nawet zepsuć jego działanie.

##### Przykład 7.3
```js
window.clicks = 0;

let clicks = Symbol('clicks');
window[clicks] = 0;
```

Dzięki unikalności symboli możemy dodawać pola do istniejących obieków, które nie należą do nas lub mogą być wykorzystywane przez inne skrypty czy biblioteki bez obaw o kolizje nazw. 

Dodatkowo pola z nazwami, które są symbolami są pomijane przez większość narzędzi do inspekcji obiektów takie jak pętla `for-in`, `Object.keys()` czy `Object.getOwnPropertyNames()`. Możemy zatem pokusić się o stworzenie prawie-prywatnych pól w klasach.

##### [Przykład 7.4](https://codepen.io/mmotel/pen/NgxVBx)
```js
let privateField = Symbol('private-field');

class Foo {
 constructor (value) {
  this[privateField] = value;
 }

 greet () {
  return 'This is my private value: ' + this[privateField];
 }
}

let foo = new Foo('bar');

console.log(foo.greet()); // -> 'bar'
```

Jednak pola z kluczami będącymi symbolami nie są pomijane przez wszystkie dostępne narzędzia do inspekcji obiektów. Nowe interfejsy API pozwala na ich pobranie - `Object.getOwnPropertySymbols()`,  `Reflect.ownKeys()`.

## Sposoby uzyskania symbolu

* metoda `Symbol()` - zwraca za każdym razem unikalny symbol,

* metoda `Symbol.for(string)` - zwraca symbol z tzw. _rejestru symboli_, każde wywołanie `Symbol.for('name')` zwróci dokładnie ten sam współdzielony symbol dla opisu `name`,

* symbole zdefiniowane w standardzie, np. `Symbol.iterator`.

---

###### Źródła

* http://shebang.pl/artykuly/es6-symbole/