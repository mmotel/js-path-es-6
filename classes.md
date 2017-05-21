# Klasy

```js
class Foo {}

let bar = new Foo();
```

## Konstruktor

```js
class Foo {
    
    constructor (bar) {
        this.bar = bar;
    }

}
```

## Metody

```js
class Foo {
    
    constructor (bar) {
        this.bar = bar;
    }
    
    update (baz) {
        this.bar = baz;
    }

}
```

## Właściwości `set` i `get`

```js
class Foo {
    
    constructor (bar) {
        this._bar = bar;
    }
    
    get greetBar () {
        return 'Hello ' + this._bar;
    }
    
    set bar (value) {
        this._bar = value;
    }

}
```

## Dziedziczenie

```js
class Foo {
    
    constructor (bar) {
        this.bar = bar;
    }
    
    update (baz) {
        this.bar = baz;
    }

}

class Bar extends Foo {
    
    constructor (bar, baz) {
        super(bar);
        this.baz = baz;
    }
    
    update (bar, baz) {
        super.update(bar);
        this.baz = baz;
    }
}
```
---

###### Źródła
