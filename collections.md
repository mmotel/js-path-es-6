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

console.log(students);      // -> Set { "Jane" }
console.log(students.size); // -> 1
```

Metoda `Set.clear` pozwala usunąć ze zbioru wszystkie jego elementy.

##### [Przykład 11.3](https://codepen.io/mmotel/pen/yXLrVg)
```js
let students = new Set(['John', 'Jane']);

students.clear();

console.log(students);      // -> Set {}
console.log(students.size); // -> 0
```

Aby sprawdzić czy zbiór zawiera jakiś element korzystamy z metody `Set.has`.

##### [Przykład 11.4](https://codepen.io/mmotel/pen/GERLKe)
```js
let students = new Set(['John', 'Jane']);

console.log(students.has('John')); // -> true
console.log(students.has('Joe'));  // -> false 
```

Obiekt `Set` posiada metodę `Set[Symbol.iterator]`. Możemy po nim iterować na dwa sposoby. Pierwszym z nich jest pęta `for`.

##### [Przykład 11.5](https://codepen.io/mmotel/pen/QgWPjy)
```js
let students = new Set(['John', 'Jane']);

for (let student of students) {
  console.log(student);
}
// -> 'John'
// -> 'Jane'
```

Możemy również skorzystać z metody `Set.forEach`.

##### [Przykład 11.6](https://codepen.io/mmotel/pen/PjogZr)
```js
let students = new Set(['John', 'Jane']);

students.forEach( (student) => {
  console.log(student);
});
// -> 'John'
// -> 'Jane'
```

Jest kilka metod, których brakuje w obiekcie `Set`. Są to m.in. metody, które znamy z tablic - `map`, `filter`, czy też te pozwalające na grupowe operacje - `addAll`, `deleteAll`.

## Słownik - `Map`

## `WeakSet`

## `WeakMap`