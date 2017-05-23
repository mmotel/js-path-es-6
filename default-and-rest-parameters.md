# Parametry domyślne i resztowe

## Parametry domyślne

##### Przykład 4.1
```js
function square (a) {
    a = a ? a : 0;

    return a * a;
}
```

```js
function square2 (a=0) {
    return a * a;
}
```

##### Przykład 4.2
```js
class Foo {
    greet (bar='bar') {
        return 'Hello ' + bar;
    }
}
```

## Parametry resztowe

##### [Przykład 4.3](http://plnkr.co/edit/JKMh4rFHwq8UYg0bCgDR)
```js
function concatAll (array1, array2) {
  let result = array1.concat(array2);
  let restArrays = Array.prototype.splice.call(arguments, 2);

  restArrays.forEach( (anotherArray) => {
    result = result.concat(anotherArray);
  });

  return result;
}

let allArrays = concatAll([1, 2], [3, 4], [5, 6], [7, 8]);
console.log(allArrays); // -> [1, 2, 3, 4, 5, 6, 7, 8]
```

##### [Przykład 4.4](http://plnkr.co/edit/6z4lqM4ekG4c4LXXrkdE)
```js
function concatAll2 (array1, array2, ...arrays) {
  let result = array1.concat(array2);

  arrays.forEach( (anotherArray) => { 
    result = result.concat(anotherArray); 
  });

  return result;
}

let allArrays2 = concatAll2([1, 2], [3, 4], [5, 6], [7, 8]);
console.log(allArrays2);// -> [1, 2, 3, 4, 5, 6, 7, 8]
```

---

##### Źródła

* [http://shebang.pl/artykuly/es6-bez-tajemnic-parametry-resztowe-domyslne/](http://shebang.pl/artykuly/es6-bez-tajemnic-parametry-resztowe-domyslne/)



