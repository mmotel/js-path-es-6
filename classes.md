# Klasy

Aby stworzyć klasę w ES5 należało stworzyć funkcję pełniącą rolę konstruktora a następnie posługując się jej prototypem dodawać nowe metody i własności. Aby cały kod klasy był łatwy do zidentyfikowania, dobrze jest ubrać go w IIFE (_Immediately Invoked Function Expression_).


##### [Przykład 2.1](ps://codepen.io/mmotel/pen/EXYGqJ)
```js
Car = (function () {
  function Car (engine) {
    this.engine = engine;
  }

  Car.prototype.drive = function (speed) {
    this._lastSpeed = speed;
    return 'Car with ' + this.engine + ' engine ' + 
      'drives at ' + speed + ' km/h.';
  }

  Object.defineProperty(Car.prototype, 'lastSpeed', {
    get: function () { 
      return this._lastSpeed ? this._lastSpeed : 0; 
    },
    enumerable: false,
    configurable: true
  });
  
  return Car;
})();

let ourCar = new Car('V8');

console.log(ourCar.drive(120)); // -> 'Car with V8 engine drives at 120 km/h.'
console.log(ourCar.lastSpeed);  // -> 120
```

Powyższy kod spełnia swoje zadanie. Definiuje klasę, jej  metody, pola oraz właściwości. Jest jednak dość skomplikowany i mało elegancki.

Nowa składnia klas wprowadzona w ES6 pozwala nam zdefiniować tą samą klasę w sposób znany z innych języków obiektowych taki jak `Java` korzystając ze słowa kluczowego `class`.

##### Przykład 2.2
```js
class Car {}

let ourCar = new Car();
```

### Konstruktor

Nasza klasa potrzebuje konstruktora. Definiujemy go używając słowa kluczowego `constructor`.

##### Przykład 2.3
```js
class Car {
    
    constructor (engine) {
        this.engine = engine;
    }

}

let ourCar = new Car('V8');
```

### Metody

Metody definiujemy podobnie jak konstruktor.

##### Przykład 2.4
```js
class Car {
    
    constructor (engine) {
        this.engine = engine;
    }
    
    drive (speed) {
        return 'Car with ' + this.engine + ' engine ' +
            'drives at ' + speed + ' km/h.';
    }

}

let ourCar = new Car('V8');
console.log(ourCar.drive(120)); // -> 'Car with V8 engine drives at 120 km/h.'
```

### Właściwości 

Definiowanie własności obiektu jest równie proste jak w przypadku metod. Wykorzystujemy do tego słowa kluczowe `set` i `get`.

##### Przykład 2.5
```js
class Car {
    
    constructor (engine) {
        this.engine = engine;
    }
    
    drive (speed) {
        this._lastSpeed = speed;
        return 'Car with ' + this.engine + ' engine ' +
            'drives at ' + speed + ' km/h.';
    }
    
    get lastSpeed () {
        return this._lastSpeed ? this._lastSpeed : 0;
    }

}

let ourCar = new Car('V8');
console.log(ourCar.drive(120)); // -> 'Car with V8 engine drives at 120 km/h.'
console.log(ourCar.lastSpeed);  // -> 120
```

### Statyczne metody i własności

Do definiowania statycznych elementów klasy w ES5 należy przypisać je wprost do obiektu klasy.

##### [Przykład 2.6](https://codepen.io/mmotel/pen/VWwQLL)
```js
Car = (function () {
    function Car (engine) {
        this.engine = engine;
        Car.carsMade += 1;
    }
    
    Object.defineProperty(Car, 'carsMade', {
        get: function () {
            return this._count ? this._count : 0;
        },
        set: function (value) {
            this._count = value;
        },
        enumerable: false,
        configurable: true 
    });
    
    Car.buildDefault = function () {
        return new Car('V8');
    };
    
    return Car;
})();

let ourCar = new Car('V16');
let anotherCar = Car.buildDefault();
console.log(Car.carsMade); // -> 2
```

Składnia klas z ES6 ponownie pozwala na uproszczenie zapisu dzięki wykorzystaniu słowa kluczowego `static`.

##### [Przykład 2.7](https://codepen.io/mmotel/pen/XgWZXO)
```js
class Car {
    constructor (engine) {
        this.engine = engine;
        Car.carsMade += 1;
    }
    
    static get carsMade () {
        return this._count ? this._count : 0;   
    }
    
    static set carsMade (value) {
        this._count = value;
    }
    
    static buildDefault () {
        return new Car('V8');
    }
}

let ourCar = new Car('V16');
let anotherCar = Car.buildDefault();
console.log(Car.carsMade); // -> 2
```

### Dziedziczenie

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

* http://shebang.pl/artykuly/es6-bez-tajemnic-klasy/
* http://shebang.pl/artykuly/es6-bez-tajemnic-podklasy/