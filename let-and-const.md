# Słowa kluczowe `let` i `const`

ES6 wprowadza dwa nowe słowa kluczowe `let` i `const`, które służą do deklarowania zmiennych oraz stałych.


## `let`

Słowo kluczowe `let` pozwala definiować zmienne podobnie jak `var`.

```js
  var a = 10;
  let b = 20;
```

W przeciwieństwie do `var`, zmienna zdefiniowana przy użyciu `let` ma zasięg blokowy a nie funkcyjny.

##### [Przykład 1.1](http://plnkr.co/edit/fkWrj6THZfqdhwgdazL8)
```js
{
  var a = 10;
}
{
  let b = 20;
}
console.log(a); // -> 10
console.log(b); // -> ReferenceError
```

Powyższy przykład pokazuje różnicę w działaniu `var` i `let`. Zmienne zadeklarowane przy użyciu `var` podlegają hoisting-owi i mają zasięg funkcyjny. Te zadeklarowane przez `let` mają zasięg blokowy a próba ich odczytania przed deklaracją powoduje błąd.

##### [Przykład 1.2](http://plnkr.co/edit/e7ro7q5JKs1K3EfgpdfJ)
```js
function foo () {
  console.log(a);   // -> undefined
  {
    var a = 10;
  }
  console.log(a);   // -> 10
}

function bar () {
  console.log(b);   // -> ReferenceError
  {
    console.log(b); // -> ReferenceError
    let b = 20;
    console.log(b); // -> 20
  }
  console.log(b);   // -> ReferenceError
}
```

Ważną róznicą pomiędzy `var` i `let` jest ich zachowanie gdy używamy ich w pętli `for`. 

##### [Przykład 1.3](http://plnkr.co/edit/qhvTBqPcI9Jph9cHnsGn)
```js
for (var i = 0; i < 3; i += 1) {
  setTimeout(function () {
    console.log(i);
  }, i * 5);
}
// -> 3 / 3 / 3

for (let i = 0; i < 3; i += 1) {
  setTimeout(function () {
    console.log(i);
  }, i * 5);
}

// -> 0 / 1 / 2
```

Dzięki zasięgowi blokowemu, w każdym obrocie pętli otrzymujemy nową kopię zmiennej zadeklarowanej przy użyciu `let`. 

_**TIP**_: Gdy używasz ES6 zapomnij o `var`, używaj tylko `let`, który działa intuicyjnie dzięki zakresowi blokowem.


## `const`

Słowo kluczowe `const` pozwala definiować stałe. Działa dokładnie tak jak `let` ale wartość stałej nie może zostać zmodyfikowana.

##### [Przykład 1.4](http://plnkr.co/edit/y2VpTazmZIvNH1T2Lb5P)
```js
const A = 'a';
A = 'b'; // -> TypeError
```

Jednak pilnowana jest jedynie referencja obiektu przypisanego do stałej. Sprawia to, że możliwe jest modyfikowanie wartości jego pól.

##### [Przykład 1.5](http://plnkr.co/edit/xA3JcHFoV5AON8dVe6cC)
```js
const A = {
  b: 10
};
console.log(A.b); // -> 10

A.b = 20;

console.log(A.b); // -> 20
```

---

###### Źródła

* http://shebang.pl/artykuly/es6-slowa-kluczowe-let-const/

