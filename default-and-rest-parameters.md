# Parametry domyślne i resztowe

## Parametry domyślne

Zdarza się, że podawanie wszystkich parametrów funkcji nie jest konieczne. Wtedy musimy ustalić ich domyślną wartość.

Dotychczas musieliśmy radzić sobie z wartościami domyślnymi _ręcznie_ w ciele funkcji.

##### Przykład 4.1
```js
function square (a) {
    a = a !== undefined ? a : 0;

    return a * a;
}
```

ES6 pozwala na ustalenie wartości domyślnej parametru w momencie jego deklaracji.

```js
function square2 (a=0) {
    return a * a;
}
```

Ważną cechą parametrów domyślnych jest moment ich ewaluacji. W przeciwieństwie do języków takich ja `Pyhton`, ich wartość jest ustalana w momencie wykonywania funkcji, a nie w momencie jej definiowania.

##### Przykład 4.2
```js
class Foo {
    today (now=new Date()) {
        return 'Today is ' + now;
    }
}
```

## Parametry resztowe

JavaScript pozwala na pisanie funkcji przyjmujących dowolną ilość argumentów. 

Zdefiniujemy funkcję `concatAll`, która przyjmuje conajmniej dwie tablice i zwraca ich konkatenację. 

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

Aby uzyskać dostęp do wszystkich argumentów skorzystaliśmy z obiektu `arguments`, który przypomina tablicę. Aby pominąć pierwsze dwa arguemnty musieliśmy skorzystać z portotypu obiektu `Array`. 

Na pierwszy rzut oka trudno stwierdzić ile argumentów przyjmuje nasza funkcja. Dopiero jej analiza pozwala stwierdzić, że może być ich wiele. Jest to niezbyt eleganckie rozwiązanie.

Odpowiedzią na wszystkie te problemy jest parametr resztowy.

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

Specjalna składnia `...arrays` mówi nam, że funkcja przyjmuje dowolną ilość parametrów. Dodatkowo parametr `arrays` jest tablicą, która zamiera wszystkie parametry znajdujące się po `array2`. Jeśli ich nie ma `arrays` będzie pustą tablicą - nigdy nie będzie to `undefined`. 

_**UWAGA**_: Funkcja może zawierać tylko jeden parametr resztowy i musi on znajdować się na końcu listy parametrów.

---

##### Źródła

* [http://shebang.pl/artykuly/es6-bez-tajemnic-parametry-resztowe-domyslne/](http://shebang.pl/artykuly/es6-bez-tajemnic-parametry-resztowe-domyslne/)



