# Interatory i pętla for...of

## Pętla for...of

### for

Iterowanie po tablicach \(uda się po kolekcjach\)  klasycznym sposobem.

```js
var myArray = ['Alfa','Bravo','Charlie','Delta','Echo','Foxtrot','Golf']

for (var i = 0; i < myArray.length; i++) {
    console.log(i);
    console.log(myArray[i]);
}
```

### for ..in

Można także \(ale nie należy\)

```js
for (var i in myArray) {
    console.log(i);
    console.log(myArray[i]);
}
```

Index `i` będzie typu string.  Kolejność iteracji nie jest gwarantowana.  For..in  stworzono do iteracji po właściwościach obiektu.

### forEach

W ES5 możemy użyć  **metody**  `forEach()` do iterowania po tablicach i kolekcjach.

```js
myArray.forEach((element,index)=>{
    console.log(index);
    console.log(element);
});
```

Pewnym problemem jest przerwanie takiej pętli. Nie ma zastosowania `break` . Ponadto:

> There is no way to stop or break a`forEach()`loop other than by throwing an exception. If you need such behavior, the
>
> `forEach()`method is the wrong tool. Use a plain loop instead. If you are testing the array elements for a predicate and need a Boolean return value, you can use[`every()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every) or [`some()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some) instead. If available, the new methods [`find()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find) or [`findIndex()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex) can be used for early termination upon true predicates as well.

### for..of

Stworzona do rozwiązania problemów pętli przedstawionych powyżej. Pozwala iterować po wielu typach danych  \( Array, String, TypedArray, Map, Set, DOMCollection, Iterators, Generators\), nie powielając problemów wyżej przedstawionych rozwiązań.

* powyższe rozwiązanie stanowi najzwięźlejszą i najprostszą pętlę operującą na elementach tablic,
* pozbawiona jest pułapek związanych z pętlą  for...in,
* w przeciwieństwie do metody `forEach()`, dobrze współpracuje z instrukcjami `break`, `continue`, `return`.

```js
var myArray = ['Alfa', 'Bravo', 'Charlie', 'Delta', 'Echo', 'Foxtrot', 'Golf'];
var paragraphs = document.querySelectorAll('p');

for (var i of myArray) {
    console.log(i);
}
for (var i of paragraphs) {
    console.log(i);
}
```

## Iteratory

> Tak jak instrukcje for i foreach w tych innych językach, pętla for–of działa wyłącznie na zasadzie wywołania metody. Tym, co łączy obiekty Array, Map, Set i inne, o których zdążyliśmy nadmienić, to metoda iteracyjna.
>
> Metodę iteracyjną może ponadto mieć jeszcze jeden rodzaj obiektu: dowolnie wybrany obiekt.
>
> Podobnie jak dodanie mójObiekt.toString\(\) do jakiegokolwiek obiektu sprawia, że JS od razu wie jak konwertować dany obiekt na łańcuch znaków, dodanie metody [**mójObiekt\[Symbol.iterator\]\(**](/symbols.md)**\)** do **dowolnego obiektu** sprawi, że JS bez problemu wykona na nim pętlę.



Obiekty z metodą \[Symbol.iterator\]\(\) nazywamy obiektami iterowalnymi.  Stwórzmy najprostszy możliwy iterator \(obiekt, który zawiera jedynie metodę iteratora\).



```js
var timestampForeverIterator = {
    [Symbol.iterator]: () => ({
        next: () => ({
            done: false,
            value: Date.now()
        })
    })
}

for (value of timestampForeverIterator) {
    console.log(value);
}
```



Funkcja iteratora musi zwracać obiekt zawierający metodę  **next.** Metoda next zaś musi zwracać obiekt informujący czy iteracja dobiegła już końca `done` oraz, że kolejną wartością  `value`  jest timestamp \(Date.now\(\)\).



> Funkcjonowanie takiego iteratora, mającego własności .done i .value, różni się od iteratorów w innych językach. W Javie iteratory mają osobne metody `.hasNext()` i .`next()`. W Pythonie natomiast istnieje pojedyncza metoda `.next()`, która zgłasza wyjątek StopIteration po wyczerpaniu się wszystkich wartości. We wszystkich trzech przypadkach zwracane są jednak właściwie te same informacje.



Obiekt iteratora może również implementować opcjonalne metody .return\(\) i .throw\(wyjątek\) . Pętla for–of wywoła metodę .return\(\), jeśli do zakończenia pętli doszło przedwcześnie w wyniku wyjątku lub instrukcji break bądź return. Iterator może implementować metodę .return\(\), jeśli potrzebne jest zwolnienie wykorzystywanych wcześniej zasobów. 

### Potencjalne zastosowania iteratorów:

1. [genrowanie](/generators.md)\(!\) danych
2. ukrywanie implementacji
3. iterowanie po wybranych właściwościach obiektu



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



