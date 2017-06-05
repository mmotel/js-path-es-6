# Destrukturyzacja

Składnia ES6 pozwala na przypisanie destrukturyzujące tablic oraz obiektów.

> Przypisanie destrukturyzujące umożliwia przypisanie własności tablicy lub obiektu do zmiennych z wykorzystaniem składni przypominającej składnię tablic czy literałów obiektowych. Może być ona niezwykle zwięzła, a jednocześnie znacznie czytelniejsza od tradycyjnego kodu służącego do uzyskania dostępu do własności.

## Tablica

W ES5 aby przypisać do zmiennych elementy tablicy należało zrobić trzema osobnymi przypisaniami. 

##### Przykład 5.1
```js
let numbers = [1, 2, 3];
let first  = numbers[0];
let second = numbers[1];
let third  = numbers[2];
```

Dzięki nowej składni możemy dokonać tego prościej.

##### Przykład 5.2
```js
let [first, second, third] = [1, 2, 3];
console.log(first);  // -> 1
console.log(second); // -> 2
console.log(third);  // -> 3
```

Jeśli spróbujemy pobrać do zmiennej element tablicy, którego w niej nie ma zwrócona zostanie wartość `undefined`.

##### Przykład 5.3
```js
let [first, second, third] = [1, 2];
console.log(first);  // -> 1
console.log(second); // -> 2
console.log(third);  // -> undefined
```

Możemy wykorzystać parametr resztowy aby pobrać do jednej zmiennej pozostałe elementy tablicy.

##### Przykład 5.4
```js
let [first, ...other] = [1, 2, 3];
console.log(first); // -> 1
console.log(other); // -> [2, 3]
```

Ponadto możemy skorzystać również z parametrów domyślych.

##### Przykład 5.5
```js
let [first=1, second=2, third=3] = [];
console.log(first);  // -> 1
console.log(second); // -> 2
console.log(third);  // -> 3
```

Możliwa jest również destrukturyzacja zagnieżdżonych tablic.

##### Przykład 5.6
```js
let [first, [second, third, [fourth]]] = [1, [2, 3, [4]]];
console.log(first);  // -> 1
console.log(second); // -> 2
console.log(third);  // -> 3
console.log(fourth); // -> 4
```

## Obiekt

Do czasu ES6 w przypadku obiektów również trzeba dokonać kilku przypisań aby wyciągnąć do zmiennych pola obkietu.

##### Przykład 5.7
```js
let foo = { 
    bar: 'bar',
    baz: 'baz'
};

let barFromFoo = foo.bar;
let bazFromFoo = foo.baz;

console.log(barFromFoo); // -> 'bar'
console.log(bazFromFoo); // -> 'baz'
```

Składnia ES6 ponownie ułatwia nam pracę.

##### Przykład 5.8
```js
let foo = { 
    bar: 'bar',
    baz: 'baz'
};

let { bar: barFromFoo, baz: bazFromFoo } = foo;

console.log(barFromFoo); // -> 'bar'
console.log(bazFromFoo); // -> 'baz'
```

Jeśli nazwa pola obiektu oraz zmiennej, do której chcemy przypisać jego wartość są takie same możemy użyć uproszczonej składni.

##### Przykład 5.9
```js
let foo = { 
    bar: 'bar',
    baz: 'baz' 
};

let { bar, baz } = foo;

console.log(bar); // -> 'bar'
console.log(baz); // -> 'baz'
```

Podobnie jak w przypadku tablic, również podczas destrukturyzacji obiektów, przyspianie do zmiennej pola, którego nie ma w obiekcie, spowoduje zwrócenie wartości `undefined`.

##### Przykład 5.10
```js
let { foo } = {}

console.log(foo); // -> undefined
```

Gdy destrukturyzujemy obiekt możemy wykorzystać parametry domyślne.

##### Przykład 5.11
```js
let { foo = 'bar' } = {}

console.log(foo); // -> 'bar'
```

Szczególnie przydatne jest to podczas pisania funkcji, które przyjmują jako parametr obiekt i nie wymagają podawania wszystkich jego własności.

##### Przykład 5.12
```js
function foo ({first, second, third}) {}

function bar ({first=1, second=2, third=3}) {}
```

Również w przypadku obiektów, możemy łączyć i zagnieżdżać wyrażenia destrukturyzujące.

##### [Przykład 5.13](https://codepen.io/mmotel/pen/oWKqPJ)
```js
var complicatedFoo = {
    bar: [
        { baz: 'baz' } 
    ]
};

let { bar: [ {baz: foo } ]} = complicatedFoo;
console.log(foo); // -> 'baz'
```

---

### Ćwiczenie

(5.1) Zaimplementuj metodę `greet`, która przyjmuje jako parametr dwuelementową tablicę obiektów zawierających pola `name` oraz `age` i zwraca komunikat: `First person is <name1> and <age1> years old. Second person is <name2> and <age2> years old.`

---

###### Źródła

* http://shebang.pl/artykuly/destrukturyzacja/