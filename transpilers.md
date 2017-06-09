# Transpilatory ES6

Aby pisać kod w ES6 bez obawy o wsparcie przegląd należy skorzystać z translipatora. Jest to narzędzie, które nasz kod napisany w ES6 zamienia na przyjazny, obsługiwany przez wszystkie przeglądarki kod ES5.

### `ES6` -> `transpilator` -> `ES5`

Mamy do wyboru kilka opcji:
* [BabelJS](https://babeljs.io),
* [Traceur.js](https://github.com/google/traceur-compiler),
* [~~TypeScript~~](http://www.typescriptlang.org).

#### Na czym polega transpilacja?

Piszemy kod wykorzystując składnię ES6.

```js
let name = 'John Doe';

function greet (name = 'Jane Doe') {
    return `My name is ${name}.`;
}

console.log(greet(name));
console.log(greet());
```

Transpilator tłumaczy nasz kod na ES5.

```js
var name = 'John Doe';

function greet (name) {
    if (name === undefined) { name = 'Jane Doe'; };
    return `My name is ' + name + '.';
}

console.log(greet(name));
console.log(greet());
```

#### Przykłady działania

* [let, parametry domyślne, łańcuchy szablonowe - BabelJS](http://bit.ly/2rJCPiu),

* [klasy, metody, właściwości - BabelJS](http://bit.ly/2rex9cL),

* [TypeScript](http://www.typescriptlang.org/play/).

---

###### Źródła

* http://shebang.pl/artykuly/es6-babel-broccoli/
