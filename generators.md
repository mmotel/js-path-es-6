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



Inne przykłady

//TODO range, randomRange  z iteratorów

//TODO  ćwiczenie - przepisać Words na generator

//TODO  .throw\(\) i .return\(\)  ,generatory zwracajace generatory

TODO Zastosowanie





**Źródła:**

* [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Generator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Generator)
* [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function\*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*)
* [https://davidwalsh.name/es6-generators](https://davidwalsh.name/es6-generators)
* [http://mrzepinski.pl/es6-generators.html](http://mrzepinski.pl/es6-generators.html)
* [http://shebang.pl/artykuly/es6-bez-tajemnic-generatory/](http://shebang.pl/artykuly/es6-bez-tajemnic-generatory/)



