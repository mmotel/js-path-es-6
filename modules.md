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

**Uwaga**: Słowo kluczowe `export` musi znajdować się na najwyższym poziomie kodu, nie może być zagnieżdżone w bloku lub funckji.

#### Korzystanie z modułów

Aby wykorzystać elementy modułu musimy je zaimportować.

```js
import { A, B, greet } from 'our-module.js';

greet('John Doe', A + B);
// -> 'Hello! My name is John Doe and I am 30 years old.'
```

**Uwaga**: Słowo kluczowe `import`, podobnie jak `export`, musi znajdować się na najwyższym poziomie kodu, nie może być zagnieżdżone w bloku lub funckji.

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

Importowanie wszystkich elementów modułu powoduje przypisanie jego całej przestrzeni nazw do obecnego zakresu. Może być to kłopotliwe, na przykład z powodu kolizji nazw. Możemy wykorzystać `as` aby zamknąć przestrzeń nazw modułu w obiekcie.

```js
import * as ourModule from 'our-module.js';

console.log(ourModule.B); // -> 10
```

#### Moduły agregujące

Często przydają się również moduły, których zadaniem jest ponowy eksport elementów wielu modułów.

```js
//our-module.js
export * from 'module-1.js';
export * from 'module-2.js';
```

#### [Przykład 11.1 z wykorzystaniem BabelJS](https://github.com/mmotel/es6-modules-demo) 


### Problemy z modułami

Obecnie moduły nie są jeszcze wspierane we wszystkich przeglądarkach. Nie jest to jednak największy problem korzystania z modułów. 

Każdy import powoduje wykonanie zapytania o plik zawierający moduł. Kiedy mamy wiele modułów, które mają wiele zależności ilość zapytań może radykalnie wydłużyć czas ładowania się aplikacji. 

Czy zatem powinniśmy dzielić nasze aplikacji na moduły? Jak najbardziej, dzięki wykorzystaniu narzędzi takich jak [`Webpack`](https://webpack.js.org) możemy spakować naszą podzieloną na moduły aplikację i załadować ją jednym zapytaniem. Jest to możliwe ponieważ system modułów ES6 jest statyczny - wymaga umieszczenia importów oraz eksoprtów na najwyższym poziomie kodu. Wszystkie zależności mogą zostać rozwiązane na etapie "kompilacji" i być spakowane do jednego pliku.

---

###### Źródła

* http://shebang.pl/artykuly/es6-bez-tajemnic-moduly/
* https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import
* [https://blog.revillweb.com/using-es2015-es6-modules-with-babel-6](https://blog.revillweb.com/using-es2015-es6-modules-with-babel-6-3ffc0870095b)