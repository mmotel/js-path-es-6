# Interatory i pętla for...of

## Pętla `for-of`

### `for`

Iterowanie po tablicach klasycznym sposobem.

##### Przykład 8.1
```js
let myArray = ['Alfa','Bravo','Charlie','Delta'];

for (let i = 0; i < myArray.length; i++) {
    console.log(i);
    console.log(myArray[i]);
}
```

### `for-in`

Można także wykorzystać petlę `for-in` ale nie jest to zalecany sposób.

##### Przykład 8.2
```js
for (let i in myArray) {
    console.log(i);
    console.log(myArray[i]);
}
```

Index `i` będzie typu string.  Kolejność iteracji nie jest gwarantowana.  `for..in`  stworzono do iteracji po właściwościach obiektu.

### `forEach`

W ES5 możemy użyć metody  `Array.forEach()` do iterowania po tablicach.

##### Przykład 8.3
```js
myArray.forEach((element, index) => {
    console.log(index);
    console.log(element);
});
```

Pewnym problemem jest przerwanie takiej pętli. Nie ma zastosowania `break` . Ponadto:

> There is no way to stop or break a`forEach()`loop other than by throwing an exception. If you need such behavior, the `forEach()`method is the wrong tool. Use a plain loop instead. If you are testing the array elements for a predicate and need a Boolean return value, you can use[`every()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every) or [`some()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some) instead. If available, the new methods [`find()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find) or [`findIndex()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex) can be used for early termination upon true predicates as well.

### `for-of`

Pętla `for-of` została stworzona do rozwiązania problemów pętli przedstawionych powyżej. Pozwala iterować po wielu typach danych  (Array, String, TypedArray, Map, Set, DOMCollection, Iterators, Generators\), nie powielając problemów wyżej przedstawionych rozwiązań.

##### Przykład 8.4
```js
let myArray = ['Alfa', 'Bravo', 'Charlie', 'Delta'];

for (let i of myArray) {
    console.log(i);
}
```

* powyższe rozwiązanie stanowi najzwięźlejszą i najprostszą pętlę operującą na elementach tablic,
* pozbawiona jest pułapek związanych z pętlą  `for-in`,
* w przeciwieństwie do metody `forEach()`, dobrze współpracuje z instrukcjami `break`, `continue`, `return`.

## Iteratory

> Tak jak instrukcje `for` i `foreach` w tych innych językach, pętla `for–of` działa wyłącznie na zasadzie wywołania metody. Tym, co łączy obiekty `Array`, `Map`, `Set` i inne, o których zdążyliśmy nadmienić, to metoda iteracyjna.
>
> Metodę iteracyjną może ponadto mieć jeszcze jeden rodzaj obiektu: dowolnie wybrany obiekt.
>
> Podobnie jak dodanie `mójObiekt.toString()` do jakiegokolwiek obiektu sprawia, że JS od razu wie jak konwertować dany obiekt na łańcuch znaków, dodanie metody [`mójObiekt[Symbol.iterator]`](symbols.md) do **dowolnego obiektu** sprawi, że JS bez problemu wykona na nim pętlę.

Obiekty z metodą `[Symbol.iterator]()` nazywamy obiektami iterowalnymi.  Stwórzmy najprostszy możliwy iterator (obiekt, który zawiera jedynie metodę iteratora).

##### Przykład 8.5
```js
let timestampForeverIterator = {
    [Symbol.iterator]: () => ({
        next: () => ({
            done: false,
            value: Date.now()
        })
    })
}

for (let value of timestampForeverIterator) {
    console.log(value);
}
```

Funkcja iteratora musi zwracać obiekt zawierający metodę `next`. Metoda `next` zaś musi zwracać obiekt informujący czy iteracja dobiegła już końca (pole `done`) oraz, że kolejną wartością  `value` jest timestamp (`Date.now()`).

> Funkcjonowanie takiego iteratora, mającego własności `done` i `value`, różni się od iteratorów w innych językach. W Javie iteratory mają osobne metody `hasNext()` i `next()`. W Pythonie natomiast istnieje pojedyncza metoda `next()`, która zgłasza wyjątek `StopIteration` po wyczerpaniu się wszystkich wartości. We wszystkich trzech przypadkach zwracane są jednak właściwie te same informacje.

Obiekt iteratora może również implementować opcjonalne metody `return` i `throw(wyjątek)`. Pętla `for–of` wywoła metodę `return`, jeśli do zakończenia pętli doszło przedwcześnie w wyniku wyjątku lub instrukcji `break` bądź `return`. Iterator może implementować metodę `return`, jeśli potrzebne jest zwolnienie wykorzystywanych wcześniej zasobów.

### Potencjalne zastosowania iteratorów:

1. [genrowanie](/generators.md)(!) danych,
2. ukrywanie implementacji,
3. iterowanie po wybranych właściwościach obiektu.

```js
const randomRange = (items = 1, from = 0, to = 10) => ({
    [Symbol.iterator]: () => {
        let currentItemCounter = 0;
        return {
            next() {
                if (currentItemCounter === items) {
                    return {
                        done: true
                    }
                }
                ++currentItemCounter;
                return {
                    done: false,
                    value: from + Math.floor(Math.random() * to) + 1
                }
            }
        }
    }
});


for (let n of randomRange(10)) {
    console.log(n);
}
```

```js
class Words {
    constructor(str) {
        this._str = str;

        this[Symbol.iterator] = () => {
            const re = /\S+/g,
                str = this._str;

            return {
                next: () => {
                    const match = re.exec(str);
                    return match ? { value: match[0], done: false } : { value: undefined, done: true }
                }
            }
        }
    }
}


const lipsum = new Words("Kopczyński i podług biegu rzeczy niemożemy miary szczęśliwości lub czynnym, lecz i jako przyboczny wynik, gdy pierwej był w pojecie o tym świecie.");

for (let word of lipsum) {
    console.log(word);
}
```

### Ćwiczenie

(8.1) Zaimplementować klasę `OverNameIterate()`   w konstruktorze przyjmującą kolekcję  obiektów. Klasa musi implementować iterator, pozwalający na wypisywanie z kolejnych obiektów własności `name`.

```js
let sampleCollection = [
    {"name": "Calvin", "surname": "Castillo", "email": "nibh.vulputate@velnislQuisque.edu", "city": "Landeck"},
    {"name": "Oren", "surname": "Austin", "email": "semper@hendreritidante.co.uk", "city": "Morrovalle"},
    {"name": "Buckminster", "surname": "Johnston", "email": "sed.hendrerit.a@eudoloregestas.net", "city": "Olen"},
    {"name": "Byron", "surname": "Cooke", "email": "Ut@Integersemelit.co.uk", "city": "Habergy"},
    {"name": "Ciaran", "surname": "Alford", "email": "Vivamus.molestie@Nuncsollicitudincommodo.co.uk", "city": "Bussolengo"},
    {"name": "Cedric", "surname": "Battle", "email": "tincidunt@ligulatortor.edu", "city": "Kelkheim"},
    {"name": "Alec", "surname": "Rasmussen", "email": "taciti.sociosqu@utlacus.co.uk", "city": "Colleretto Castelnuovo"},
    {"name": "Fuller", "surname": "Hooper", "email": "Nam.porttitor@tempuseuligula.com", "city": "Izel"},
    {"name": "Brett", "surname": "Fox", "email": "venenatis@tempor.ca", "city": "Castello Tesino"},
    {"name": "Armand", "surname": "Nicholson", "email": "magna.Nam@blanditcongue.ca", "city": "Bournemouth"},
    {"name": "Kennan", "surname": "Blair", "email": "eleifend.vitae@sedduiFusce.net", "city": "Paranaguá"},
    {"name": "Jack", "surname": "Lowe", "email": "erat.vitae@Nunc.ca", "city": "Roveredo in Piano"}
];
```

---

**Źródła**

* [https://medium.com/ecmascript-2015/es6-iterators-4afec026f70a](https://medium.com/ecmascript-2015/es6-iterators-4afec026f70a)
* [http://shebang.pl/artykuly/es6-bez-tajemnic-iteratory-i-petla-for-of/](http://shebang.pl/artykuly/es6-bez-tajemnic-iteratory-i-petla-for-of/)
* [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration\_protocols](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols)



