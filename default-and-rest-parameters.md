# Parametry domyślne i resztowe

## Parametry domyślne

```js
function square (a=0) {
    return a * a;
}
```


```js
class Foo {
    greet (bar='bar') {
        return 'Hello ' + bar;
    }
}
```

## Parametry resztowe

```js
function concatAll (array1, array2, ...arrays) {
    let result = array1.concat(array2);
    arrays.forEach( (a) => { result.concat(a) });
    return result;
}
```

---

##### Źródła

* http://shebang.pl/artykuly/es6-bez-tajemnic-parametry-resztowe-domyslne/