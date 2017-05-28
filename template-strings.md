# Łańcuchy szablonowe

ES6 pozwana na definiowanie łańcuchów w nowy sposób - przy użyciu odwróconego apostrofu ``` ` ```. W przeciwieństwie do łańcuchów defniniowanych przy użyciu apostrofów `'` oraz cudzysłowów `"` te zdefiniowane przez odwrócone apostrofy ``` ` ``` mogą mieć wiele linii. Ponadto wszystkie białe znaki oraz nowe linie są odwzorowywane jeden do jeden.

##### Przykład 6.1
```js
let template1 = `<p>Hello World!</p>`;

let tempalte2 = `
    <p>
        Hello World!
    </p>
`;
```

##### Przykład 6.2
```js
function greet (name, city, age) {
    return `Hello, I am ${name} from ${city} and ${age} year old.`;
}
```

---

###### Źródła

* http://shebang.pl/artykuly/es6-bez-tajemnic-lancuchy-szablonowe/



