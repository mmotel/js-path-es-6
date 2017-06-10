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

Jeżeli chcemy aby nasza _strzałka_ nie miała parametrów lub miała ich więcej niż jeden musimy użyć nawiasów.

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

##### [Przykład 4.4](https://codepen.io/mmotel/pen/mwVQmV)

```js
class Foo {
  constructor (data) {
    this.data = data;
  }

  update (data) {
    let self = this;
    setTimeout(function () { self.data = data; }, 50);
  }
}
```

W powyższym przykładzie wewnątrz `function` wartość `this` będzie równa `undefined` lub `window` przez co musieliśmy zasotoswać `self pattern` aby móc uzyskać dostęp do własciwego `this` - instancji klasy `Foo`.

Rozwiązaniem jest zasotoswanie funkcji strzałkowej.

##### [Przykład 4.5](https://codepen.io/mmotel/pen/zzrMzy)

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

Funkcja strzałkowa _dziedziczy_ `this` z zewnętrzego zakresu dzięki czemu mogliśmy bezpośrednio odwołać się do instancji klasy `Foo` przez `this`.

**_TIP_**:

> * Z funkcji _niestrzałkowych_ należy korzystać w przypadku metod wywoływanych poprzez składnię `obiekt.metoda()`. Funkcje te otrzymają sensowną wartość `this` od wywołującego je obiektu.
* Funkcji strzałkowych należy używać w pozostałych przypadkach.

---

### Ćwiczenie

(4.1) Uzupełnij implementację metody `even()`, tak aby zwracała ona tylko parzyste liczby z przekazanej tablicy liczb.

```js
class ArrayUtils {
  static even (numbers) {
    // return ... 
  }
}
```

---

###### Źródła

* [http://shebang.pl/artykuly/es6-funkcje-strzalkowe/](http://shebang.pl/artykuly/es6-funkcje-strzalkowe/)
