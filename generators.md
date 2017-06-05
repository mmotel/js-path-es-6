# Generatory

Generatory są [iteratorami](/iterators-and-for-of.md). Wszystkie generatory mają wbudowaną implementację metod `.next()` i `[Symbol.iterator]()`

## Przykładowy generator

```js
function* sampleGenerator() {
    yield 1;
    yield 2;
    yield 3;
}
```

### Specyficzne elementy składani

* **function\*** - specjalny rodzaj funkcji, która zwraca instancję generatora.
* **yield** - wewnątrz generatora yield jest słowem kluczowym o składni podobnej do instrukcji return. Różnica polega na tym, że instrukcja return może być użyta wewnątrz funkcji \(nawet generatora\) tylko raz. W przypadku instrukcji yield takich ograniczeń nie ma. Wyrażenie yield **powoduje wstrzymanie wykonywania generatora**, co umożliwia późniejsze wznowienie jego działania.

_**Kluczową różnicą pomiędzy zwykłymi funkcjami a generatorami jest to, że  wstrzymanie funkcji nie jest możliwe. Generatory natomiast wstrzymać można.**_

### Uruchamiamy generator

```js
let gen = sampleGenerator(); // [object Generator]
console.log(gen.next()); // Object {value: 1, done: false}
console.log(gen.next()); // Object {value: 2, done: false}
console.log(gen.next()); // Object {value: 3, done: false}
console.log(gen.next()); // Object {value: undefined, done: true}
console.log(gen.next()); // Object {value: undefined, done: true}

for (var val of sampleGenerator()) {    //Tak! var zamiast let
    console.log(val);
}

console.log(val);

//1
//2
//3
//3
```

### Co się wydarzyło?

Samo wywołanie generatora wygląda identycznie jak wywołanie funkcji : `sampleGenerator()`.  Generator nie rozpoczyna jednak działania od razu. Na początek zwracany jest wstrzymany obiekt generatora - gen – można go porównać do wstrzymanego wywołania funkcji. Do wstrzymania tego dochodzi zaraz na początku generatora, tuż przed wykonaniem pierwszej linijki kodu.

Po każdym wywołaniu metody obiektu generatora `.next()` funkcja zostaje wznowiona i jest wykonywana aż do kolejnej instrukcji yield.

Po ostatnim wywołaniu metody `gen.next()` generator dobiega końca, dlatego w polu .done zwracanego obiektu mamy wartość true. Zakończenie wywoływania funkcji oznacza praktycznie zwrócenie wartości undefined, stąd też wartość ta pojawia się w polu `value`.

### Istotne!

> Za każdym razem, gdy generator wykonuje instrukcję yield jego ramka stosu – zmienne lokalne, argumenty, wartości tymczasowe oraz informacja na temat aktualnego miejsca wykonania w kodzie generatora – zostaje usunięta ze stosu. Obiekt generatora przechowuje jednak odniesienie do ramki \(bądź jego kopię\), dzięki czemu kolejne wywołanie metody .next\(\) może ją reaktywować i kontynuować wykonywanie funkcji.

## Generatory są iteratorami

Powtórzmy jeszcze raz: Generatory są [iteratorami](/iterators-and-for-of.md). Wszystkie generatory mają wbudowaną implementację metod `.next()` i `[Symbol.iterator]()`.  Programista musi tylko napisać kod realizujący działanie pętli.  Zaimplementujmy zatem generator `randomRange()` zwracający losowe liczby z określonego zakresu \(analogicznie do [iteratora z poprzedniego rozdziału](/iterators-and-for-of.md)\)

```js
function* randomRange(items = 1, from = 0, to = 10) {
    for (let i = 0; i < items; i++) {
        yield from + Math.floor(Math.random() * to) + 1;
    }
}

for (let n of randomRange(10)) {
    console.log(n);
}
```

Jak widać implementacja krótsza i sprowadza się jedynie do określenia tego co ma być generowane. Nie trzeba implementować metod iteratora.

### Sterowanie generatorem

[**Generator.prototype.next\(\)**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Generator/next)

* podobnie jak iterator, zwraca obiekt z wartościami  `done`oraz `value`.  `next()` pozwala także na przekazanie wartości do generatora.

**Generator.prototype.return\(\)  ** - pozwala na zatrzymanie działania generatora, z opcjonalnie przekazaną wartością.

```js
function* sampleGenerator() {
    yield 1;
    yield 2;
    yield 3;
}

let gen = sampleGenerator(); // [object Generator]
console.log(gen.next()); // Object {value: 1, done: false}
console.log(gen.next()); // Object {value: 2, done: false}
console.log(gen.return('SolwIT')); // Object {value: 'SolwIT', done: true}
console.log(gen.next()); // Object {value: undefined, done: true}
console.log(gen.next()); // Object {value: undefined, done: true}
```

**Generator.prototype.throw\(\)** - pozwala na zatrzymanie działania generatora poprzez rzucenie wyjątku.

```js
function* sampleGenerator() {
    try {
        yield 1;
        yield 2;
        yield 3;
        yield 4;
    } catch (e) {
        console.log('Ooops! ', e.message);
    }
}

let gen = sampleGenerator(); // [object Generator]
console.log(gen.next()); // Object {value: 1, done: false}
console.log(gen.next()); // Object {value: 2, done: false}
console.log(gen.throw(new Error('SolwIT'))); // Ooops!  SolwIT, Object {value: undefined, done: true}
console.log(gen.next()); // Object {value: undefined, done: true}
```

### Potencjalne zastosowanie generatorów

* tworzenie kosztownych danych
* ukrywanie implementacji
* generowanie danych niestandardowych rozmiarów

### Ćwiczenie

(9.1) Przepisz klasę `Words` z poprzedniego rozdziału. Zamiast implementacji iteratora, użyj generatora.

---

**Źródła:**

* [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Generator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Generator)
* [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function\*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*)
* [https://davidwalsh.name/es6-generators](https://davidwalsh.name/es6-generators)
* [http://mrzepinski.pl/es6-generators.html](http://mrzepinski.pl/es6-generators.html)
* [http://shebang.pl/artykuly/es6-bez-tajemnic-generatory/](http://shebang.pl/artykuly/es6-bez-tajemnic-generatory/)



