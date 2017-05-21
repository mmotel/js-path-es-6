# Funkcje strzałkowe


```js
function square (a) {
  return a * a;
}

let square2 = (a) => a * a;
```


## Domyślnym return

```js
(a) => a * a
```

## Ciało funkcji

```js
(a) => {
  return a * a;
}
```

## `this`

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

* http://shebang.pl/artykuly/es6-funkcje-strzalkowe/

