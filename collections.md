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

Słownik podobnie jak obiekt pozwala przechowywać pary klucz-wartość. W odróżnieniu od obiektu, w przypadku słownika nie ma możliwość kolizji wartości z metodami. 

##### [Przykład 11.7](https://codepen.io/mmotel/pen/NgWVqg)
```js
class Student {
  constructor (firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
}

let students = new Map([
  ['John', new Student('John', 'Doe')],
  ['Jane', new Student('Jane', 'Doe')]
]);

console.log(students);
// => Map {
//      "John" => Student {firstName: "John", lastName: "Doe"}, 
//      "Jane" => Student {firstName: "Jane", lastName: "Doe"}
//    }
```

Słownik możemy utworzyć przekazując do jego konstruktora inny słownik, tablicę dwuelementowych tablic `[klucz, wartość]` oraz przy pomocy iteratora lub generatora zwracającego takie tablice.

Parę klucz-wartość dodajemy do słownika używając metodę `Map.set`. Dodanie do słownika wartości dla klucza, który już się w nim znajduje spowoduje nadpisanie starej wartości.

##### [Przykład 11.8](https://codepen.io/mmotel/pen/zzYQqe)
```js
class Student {
  constructor (firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
}

let students = new Map([
  ['John', new Student('John', 'Doe')],
  ['Jane', new Student('Jane', 'Doe')]
]);

students.set('John', new Student('John', 'Smith'));

console.log(students);
// => Map {
//      "John" => Student {firstName: "John", lastName: "Smith"}, 
//      "Jane" => Student {firstName: "Jane", lastName: "Doe"}
//    }

```

Podobnie jak zbiór, słownik również posiada metody `Map.has`, `Map.delete`, `Map.clear` oraz pole `Map.size`, które działają analogicznie jak w zbiorach.



## `WeakSet`

## `WeakMap`