# Słowa kluczowe `let` i `const`

ES6 wprowadza dwa nowe słowa kluczowe `let` i `const`, które służą do deklarowania zmiennych oraz stałych.

## `let`

Słowo kluczowe `let` pozwala definiować zmienne podobnie jak `var`.

```js
  var a = 10;
  let b = 20;
```

W przeciwieństwie do `var`, zmienna zdefiniowana przy użyciu `let` ma zasięg blokowy a nie funkcyjny.

```js
function foo () {
  {
    var a = 10;
  }
  {
    let b = 20;
  }
  console.log(a); // -> 10
  console.log(b); // -> error
}
```

Powyższy przykład pokazuje różnicę w działaniu `var` i `let`. Zmienne zadeklarowane przy użyciu `var` podlegają hoisting-owi i mają zasięg funkcyjny. Te zadeklarowane przez `let` mają zasięg blokowy i są deklarowane dokładnie w miejscu ich wystąpienia.

```js
function foo () {
  console.log(a); // -> undefined
  {
    var a = 10;
  }
  console.log(a); // -> 10
}

function var () {
  console.log(b); // -> error
  {
    console.log(b); // -> error
    let b = 20;
    console.log(b); // -> 20
  }
  console.log(b); // -> error
}
```

_**TIP**: Gdy używasz ES6 zapomnij o `var`, używaj tylko `let`, który działa intuicyjnie._

## `const`

Słowo kluczowe `const` pozwala definiować stałe.

```js
const FOO = 'foo';
FOO = 'bar'; // -> error
```

Wartość stałej nie może zostać zmodyfikowana.

```js
const A = {
  b: 10
};
console.log(A.b); // -> 10

A.b = 20;

console.log(A.b); // -> 20
```

Jednak pilnowana jest jedynie referencja obiektu przypisanego do stałej. Sprawia to, że możliwe jest modyfikowanie wartość pól obiektu przypisanego do stałej.

