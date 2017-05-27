# Funkcje strzałkowe

Funkcja strzałkowa - _strzałka_ - jest nowym sposobem na definiowanie wyrażeń funkcyjnych.

```js
function square (a) {
  return a * a;
}

let square2 = a => a * a;
```

Nowa notacja pozwala na pominięcie słów kluczowych `function` i `return` oraz klamry. _Strzałki_ domyślnie zwracają to co znajduje się za `=>`.

### Parametry

Jeżeli chcemy aby nasza _strzałka_ miała więcej niż jeden lub zero parametrów musimy użyć nawiasów.

```js
() => 10

(a, b) => a * b
```

### Ciało funkcji

Jednak nie zawsze chcemy lub możemy wykonać wszystko w jednym wyrażeniu. Je

```js
(a) => {
  return a * a;
}
```

### `this`

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



