# Moduły

Obecnie JavaScript to już nie tylko pojedyńcze skrypty. Dzisiaj tworzymy rozbudowane aplikacje, które siłą rzeczy dzielimy na moduły aby pogrupować nasz kod logicznie oraz funkcyjnie. 

Istnieje już kilka systemów modułów w JavaScript, np. `AMD`, `SystemJS` czy też `RequireJS`. Po co więc system modułów w ES6? Głównie po to aby ustandaryzować sposób definiowania  i wykorzystywania modułów oraz dadać kilka funkcjonalności znanych z innym języków. 

#### Definiowanie modułów

Moduł to po prostu plik `.js` eksportujący część swoich elementów - funkcji, zmiennych i stałych.


```js
//our-module.js
export const A = 10;

export let B = 20;

export function greet (name, age) {
    return `Hello! My name is ${name} and I am ${age} years old.`;
}
```

#### Korzystanie z modułów

Aby wykorzystać elementy modułu musimy je zaimportować.

```js
import { A, B, greet } from 'our-module.js';

greet('John Doe', A + B);
// -> 'Hello! My name is John Doe and I am 30 years old.'
```

Możemy także w łatwy sposób zaimportować wszystkie elementy modułu.

```js
import * from 'our-module.js';
``` 

#### Zmiana nazwy

Możemy też zmienić nazwę elementu podczas eksportu.

```js
//our-module.js
const A = 10;

export { A as B };
```

A także podczas importu.

```js
import { B as C } from 'our-module.js'; 
```

```js
import * as ourModule from 'our-module.js';
```

#### Moduły agregujące

Często przydają się również moduły, których zadaniem jest ponowy eksport elementów wielu modułów.

```js
//our-module.js
export * from 'module-1.js';
export * from 'module-2.js';
```

#### [Przykłady z wykorzystaniem BabelJS](link_do_repo_na_githubie) 

---

###### Źródła

* http://shebang.pl/artykuly/es6-bez-tajemnic-moduly/
* [https://blog.revillweb.com/using-es2015-es6-modules-with-babel-6](https://blog.revillweb.com/using-es2015-es6-modules-with-babel-6-3ffc0870095b)