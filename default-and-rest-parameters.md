# Parametry domyślne i resztowe

## Parametry domyślne

Zdarza się, że podawanie wszystkich parametrów funkcji nie jest konieczne lub wymagane. Wtedy musimy ustalić ich domyślną wartość.

Dotychczas musieliśmy radzić sobie z wartościami domyślnymi _ręcznie_ w ciele funkcji.

##### [Przykład 4.1](https://codepen.io/mmotel/pen/LLGXNo)
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

##### [Przykład 4.2](https://codepen.io/mmotel/pen/MoKzeV)
```js
class CoolDate {
    today (now=new Date()) {
        return 'Today is ' + now;
    }
}
```

**_UWAGA_**: Po parametrze posiadającym wartość domyślną nie powinny występować parametry bez niej.

## Parametry resztowe

JavaScript pozwala na pisanie funkcji przyjmujących dowolną ilość argumentów. 

Zdefiniujemy funkcję `concatAll()`, która przyjmuje conajmniej dwie tablice i zwraca ich konkatenację. 

##### [Przykład 4.3](https://codepen.io/mmotel/pen/OgMaWb)
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

##### [Przykład 4.4](https://codepen.io/mmotel/pen/dRGQvb)
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

Specjalna składnia `...arrays` mówi nam, że funkcja przyjmuje dowolną ilość parametrów. Dodatkowo parametr `arrays` jest tablicą, która zawiera wszystkie parametry znajdujące się po `array2`. Jeśli ich nie ma `arrays` będzie pustą tablicą - nigdy nie będzie to `undefined`. 

_**UWAGA**_: Funkcja może zawierać tylko jeden parametr resztowy i musi on znajdować się na końcu listy parametrów.

---

### Ćwiczenia

(3.1) Zaimplementuj funkcję `greet`, która przyjmuje parametr `name` i zwraca komunikat `Hello World! I am <name>.`. Jeśli parametr nie zostanie podany funkcja powinna zwrócić komunikat `Hello World! I am John Doe.`.

(3.2) Zaimplementuj funkcję `addAll`, która przyjmuje dowolną ilość liczb i zwraca ich sumę.

---

##### Źródła

* [http://shebang.pl/artykuly/es6-bez-tajemnic-parametry-resztowe-domyslne/](http://shebang.pl/artykuly/es6-bez-tajemnic-parametry-resztowe-domyslne/)



