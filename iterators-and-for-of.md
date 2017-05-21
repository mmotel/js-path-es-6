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

> There is no way to stop or break a`forEach() `loop other than by throwing an exception. If you need such behavior, the
>
> `forEach() `method is the wrong tool. Use a plain loop instead. If you are testing the array elements for a predicate and need a Boolean return value, you can use[`every()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every) or [`some()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some) instead. If available, the new methods [`find()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find) or [`findIndex()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex) can be used for early termination upon true predicates as well.

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



