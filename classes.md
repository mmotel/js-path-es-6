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

console.log(ourCar.drive(120)); 
// -> 'Car with V8 engine drives at 120 km/h.'
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
console.log(ourCar.drive(120)); 
// -> 'Car with V8 engine drives at 120 km/h.'
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
console.log(ourCar.drive(120)); 
// -> 'Car with V8 engine drives at 120 km/h.'
console.log(ourCar.lastSpeed);  // -> 120
```

### Statyczne metody i własności

Do definiowania statycznych elementów klasy w ES5 należy przypisać je wprost do obiektu klasy. 

Załóżmy, że chcemy policzyć ilość stworzonych instancji klasy `Car`.

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

Jak każdy język obiektowy, JavaScript pozwala na dziedziczenie klas. W ES5 nie jest to jednak łatwe zadanie.

##### [Przykład 2.8](https://codepen.io/mmotel/pen/MoWQGx)
```js
Car = (function () {
  function Car (engine) {
    this.engine = engine;
  }
  
  Car.prototype.drive = function (speed) {
    return 'Car with ' + this.engine + ' engine ' + 
        'drives at ' + speed + ' km/h.';
  }
  
  return Car;
})();

Truck = (function () {
  function Truck (engine, capacity) {
    Car.call(this, engine);
    this.capacity = capacity;
  } 
  
  Truck.prototype = Object.create(Car.prototype);
  Truck.prototype.constructor = Truck;
  
  Truck.prototype.drive = function (speed) {
    return Car.prototype.drive.call(this, speed) + 
      ' It is a truck and has ' + 
          (this.capacity / 1000) + ' tons capacity.';
  }
  
  return Truck;
})();

let ourTruck = new Truck('V12', 12000);

console.log(ourTruck.engine, ourTruck.capacity); 
// -> 'V12' - 12000
console.log(ourTruck.drive(90)); 
// -> 'Car with V12 engine drives at 90 km/h. 
//     It is a truck and has 12 tons capacity.'
```

Składnia ES6 pozwala nam zapisać powyższe dziedziczenie znacznie prościej. Wykorzystamy słowa kluczowe `extends` oraz `super`.

##### [Przykład 2.9](https://codepen.io/mmotel/pen/owNqgZ)
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

class Truck extends Car {
  constructor (engine, capacity) {
    super(engine);
    this.capacity = capacity;
  }
  
  drive (speed) {
    return super.drive(speed) + 
      ' It is a truck and has ' + 
        (this.capacity / 1000) + ' tons capacity.';
  }
}

let ourTruck = new Truck('V12', 12000);

console.log(ourTruck.engine, ourTruck.capacity); 
// -> 'V12' - 12000
console.log(ourTruck.drive(90)); 
// -> 'Car with V12 engine drives at 90 km/h. 
//     It is a truck and has 12 tons capacity.'
```
---

### Ćwiczenia

(2.1) Zaimplementuj klasę `Person`, posiadającą pola `firstName`, `lastName` oraz `height` (w centymetrach). Konstruktor powinien przyjmować wartości `firstName` i `lastName`. Dodatkowo klasa powinna posiadać metodę `Person.getName`, która zwraca imię i nazwisko oraz parę własności pozwalającą pobrać i ustawić wzrost w metach.

(2.2) Zaimplementuj klasę `Student` dziedziczącą po klasie `Person` (z ćwiczenia 1.), która dodatkowo posiada pole `school` przechowujące nazwę szkoły. Klasa `Student` powinna posiadać metodę `Person.greet`, która zwraca komunikat `My name is <name> and I am going to <school>`.

(2.3) Dodaj do klasy `Student` (z ćwiczenia 2.) statyczne własności oraz metodę pozwalające obliczyć średni wzrost utworzonych studentów. 

---

###### Źródła

* http://shebang.pl/artykuly/es6-bez-tajemnic-klasy/
* http://shebang.pl/artykuly/es6-bez-tajemnic-podklasy/
* https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Inheritance