# Kolekcje

W ES5 mamy do dyspozycji jedną klasę reprezentującą kolekcje - jest to tablica (`Array`). Możemy również wykorzystać obiekt jako tablicę asocjacyjną (słownik) klucz-wartość. Oba te rozwiązania mają swoje ograniczenia i problemy. Jednym z nich jest możliwość zinterpretowania metody obiektu jako danych. 

Aby rozwiązać dotychczasowe problemy twórcy standardu ES6 wprowadzili do niego nowe typy kolekcji: zbiór (`Set`) oraz słownik (`Map`).


## Zbiór - `Set`

Zbiór podobnie jak tablica jest modyfikowalną kolekcją. Zasadniczą różnicą pomiędzy nimi jest to, że zbiór nie może zawierać dwóch takich samych elementów. Próba dodania do zbioru elementu, który już się w nim znajduje nie powoduje żadnych zmian zbioru.

##### [Przykład 11.1](https://codepen.io/mmotel/pen/BZabqE)
```js
let students = new Set(['John', 'Jane']);

console.log(students);     // -> Set {"John", "Jane"}
console.log(students.size) // -> 2

students.add('John');

console.log(students);     // -> Set {"John", "Jane"}
console.log(students.size) // -> 2
```

Metoda `Set.add` pozwala na dodawanie do zbioru nowych elementów. Pole `Set.size` przechowuje rozmiar zbioru. Do usuwania elementów ze zbioru służy metoda `Set.delete`.

##### [Przykład 11.2](https://codepen.io/mmotel/pen/ZyEZYL)
```js
let students = new Set(['John', 'Jane']);

students.delete('John');

console.log(students);
console.log(students.size);
```

Aby sprawdzić czy zbiór zawiera jakiś element korzystamy z metody `Set.has`.

##### [Przykład 11.3](https://codepen.io/mmotel/pen/GERLKe)
```js
let students = new Set(['John', 'Jane']);

console.log(students.has('John')); // -> true
console.log(students.has('Joe'));  // -> false 
```



## Słownik - `Map`

## `WeakSet`

## `WeakMap`