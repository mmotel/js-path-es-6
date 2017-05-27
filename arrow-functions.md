# Funkcje strzałkowe

Funkcja strzałkowa - _strzałka_ - jest nowym sposobem na definiowanie wyrażeń funkcyjnych.

##### Przykład 4.1
```js
function square (a) {
  return a * a;
}

let square2 = a => a * a;
```

Nowa notacja pozwala na pominięcie słów kluczowych `function` i `return` oraz klamry. _Strzałki_ domyślnie zwracają to co znajduje się za `=>`.

### Parametry

Jeżeli chcemy aby nasza _strzałka_ miała więcej niż jeden lub zero parametrów musimy użyć nawiasów.

##### Przykład 4.2
```js
() => 10

(a, b) => a * b
```

W przypadku funkcji strzałkowych nie możemy skorzystać z `arguments` ale w ES6 możemy skorzystać z parametrów resztowych.

### Ciało funkcji

Jednak nie zawsze chcemy lub możemy wykonać wszystko w jednym wyrażeniu. Aby zdefiniować ciało _strzałki_ używamy nawiasy klamrowe.

##### Przykład 4.3
```js
(a) => {
  return a * a;
}
```

Jeśli zdefiniujemy ciało _strzałki_ nie zwraca już ona domyślnie swojej wartości - musimy użyć jawnie słowa kluczowego `return`.

### `this`

Subtelną ale bardzo ważną rożnicą pomiędzy zwykłą funkcją a _strzałką_ jest wiązanie wartości `this`.

##### Przykład 4.4
```js
class Foo {
  constructor (data) {
    this.data = data;
  }

  update (data) {
    setTimeout(() => { this.data = data; }, 50);
  }
}
```

---

###### Źródła

* [http://shebang.pl/artykuly/es6-funkcje-strzalkowe/](http://shebang.pl/artykuly/es6-funkcje-strzalkowe/)



