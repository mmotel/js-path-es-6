# Moduły

Obecnie kod pisany w JavaScript nie jest już pojedynczymi skryptami. Dzisiaj tworzymy rozbudowane aplikacje, które siłą rzeczy dzielimy moduły aby pogrupować nasz kod logicznie oraz funkcyjnie. 

Istnieje już kilka systemów modułów w JavaScript, np. `AMD`, `SystemJS` czy też `RequireJS`. Po co więc system modułów w ES6? Głównie po to aby ustandaryzować sposób definiowania  i wykorzystywania modułów oraz dodaniu kilku funkcjonalności znanych z innym języków. 

### Definiowanie modułów

Moduł to po prostu plik `.js` eksportujący część swoich funkcji, zmiennych i stałych.


```js
export const A = 10;

export let B = 20;

export function greet (name) {
    return `Hello! My name is ${name}.`;
}
```

Możemy też zmienić nazwę elementu podczas eksportu.

```js
const A = 10;

export { A as B };
```

export default

export barrels

### Korzystanie z modułów

import 

import as

import *

import default

### Przykład z wykorzystaniem BabelJS

---

###### Źródła

* http://shebang.pl/artykuly/es6-bez-tajemnic-moduly/
