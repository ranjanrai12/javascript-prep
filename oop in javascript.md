# Javascript OOP concept

## Q: Is javaScript is object-oriented language ?

A: JavaScript is not an `object-oriented` language. Neither is it completely a `functional` language. JavaScript is a prototype-based procedural language. It supports both `functional` and `object-oriented` patterns of programming.

- `Object-Oriented Programming (OOP)`: The object-oriented paradigm keeps data and actions grouped together inside classes. In OOP, we create classes and then create their instances called objects.
- `Prototype-based Programming`: In Prototype-based programming, we derive objects from other already existing objects.

`Note`: JavaScript is not a `OOP` language but it has support for it. It has the `class` keyword, which is just a `syntactic sugar` over `prototypes`. We actually create `prototypes` in javascript, and not classes. The `class` keyword is there to make javascript look like an `OOP` language.

## Q: Create object using `Class`.

A: Look at ES6 the way of defining the classes with `class` keyword.Define `constructor function` and all the other `data functions` inside the class declaration function. Then we create `instances` for this class using the `new` keyword.

```
class Student{
    constructor(first_name, last_name){
        this.first_name = first_name,
        this.last_name = last_name
    }
    display_full_name = function(){
        return`${first_name} ${last_name}`
    }
}

```

## Q: What is OOP concept and explain the four pillars of it ?

A: OOP is a programming `paradigm` that believes in grouping data (`properties`) and methods (`actions`) together inside a box. It demonstrates the pattern of `real-world` objects.

### `Encapsulation`:

`Encapsulation` can be defined as “the packing of data and functions into one component”. `Packing`, which is also known as bundling, grouping and binding, simply means to bring together data and the methods which operate on data. The component can be a function, a class or an object.

```
Ways to Achieve Encapsulation in Javascript
```

- Achieving Encapsulation Using the `Functional Scope`: Since a variable inside a `functional scope` can not be accessed from outside, we can restrict the direct access to data using the functional scope.

```
function Person(name) {
  // Private variables
  var name = name;

  // Public methods (privileged methods)
  function getName() {
    return name;
  };
}
```

- Achieving Encapsulation Using `Closures`:
  We can create a function inside a function, and the inner function will be able to access the local variable defined inside the outer function. This is called `closure`.
  Ex:
  ```
  function messageFunc() {
    const message = "Hey there!"
    const displayMessage = function() {
        console.log(message);
    }
    displayMessage();
  }
  // Calling the function which internally defines the message
    messageFunc();
  // Trying to access message from outside the function which defines it
  console.log("Message from outside: ",message);
  ```
  `another example` to access in case want to access inside data from outside.
  ```
  let student = function(){
    var id= 12;
    var name= "Isaac";
    var marks= 81;
    var obj = {
        setMarks: function(newMarks){
            if(isNaN(newMarks)){
                throw new Error(`${newMarks} is not a number`)
            }
            marks = newMarks
        },
        getMarks: function(){return marks},
        getName: function(){return name},
        getId: function(){return id}
    }
    return obj;
  }()
  console.log(student.getMarks()) //81
  student.setMarks(98)
  console.log(student.getMarks()) //98
  student.setMarks("Ninty")
  ```
- Encapsulation Using `Private Variables` using class.

```
class Student {
    constructor(id, name, marks){
        let _id = id;
        let _name = name;
        let _marks = marks
        this.getId = () => _id;
        this.getName = () => _name;
        this.getMarks = ()=> _marks;
        this.setMarks = (marks)=>{
            _marks = marks
        }
    }
}
let s = new Student(1,"harsh", 85)
s.getId() //1
s.getName() //harsh
s.setMarks(90)
s.getMarks() //90

```

### `Inheritance`:

Accessing the properties and method of one class to another with it's exising functionality that is known as `Inheritance`.
Syntax:
The `extends` keyword is used for developing the `inheritance` between two `child classe` and `parent class`.

```
childClassName extends parentClassName{
    //child class definition
}
```

- `Inheritance Example with no child class constructor`:

```
  //parent class
  class Animals {
      constructor(name) {
          this.name = name;
      }
      animalName() {
          console.log('Animal name is ' + this.name);
      }
  }

  //Pets(child class) extending the parent class
  class Pets extends Animals {

  }
  const p1 = new Pets('Dog');
  p1.animalName() // Animal name is Dog
```

`Note`: In above example as we can see that `instance` is created from `child class` and had access the method from `parent class`, Here one thing need to note that in child class `constructor` is not present in that case by default empty constructor is created by javascript (just to check print console.log(p1) and check inside the `prototype`), and also this is inheritance with no child class constructor then by default `super() keyword` is being used inside the `constructor` of child class.

- `Inheritance Example with child class constructor`:

  ```
  //parent class
  class Animals {
    constructor(name) {
        this.name = name;
    }
    animalName() {
        console.log('Animal name is ' + this.name);
    }
  }

  //Pets(child class) extending the parent class
  class Pets extends Animals {
    constructor(name) {
        super(name)
    }
  }
  const p1 = new Pets('Dog');
  p1.animalName() // Animal name is Dog
  ```

`Note`: if constructor is defined inside the child class which is known as `overriding constructor` then it's mandatory to keep `super` keyword inside the `constructor` at the `top level always`

- `Inheritance with overriding properties and method of parent class`:

```
    class Animals {
        constructor(name) {
            this.name = name;

        }
        animalDetails() {
            console.log('Animal name is ' + this.name);
        }
    }

    //Pets(child class) extending the parent class
    class Pets extends Animals {
        constructor(name, age) {
          super(name)
          this.age = age
          //overriding properties
          this.name = 'Cat'
        }
        // Overriding method
        animalDetails() {
            console.log('Animal name is ' + this.name + ' and age is '+ this.age);
        }
    }
    var p1 = new Pets('Dog', 2)
    console.log(p1.animalDetails())
```

- `Inheriting static members`: The static attributes and methods of the parent class are also inherited during inheritance in `javascript`. The inheriting static members in javascript belong to the class and are not part of the instantiated object.

```
class car {
    constructor(color) {
        this.color = color;
    }

    display() {
        console.log(`This car is ${this.color} in color`);
    }

    static greet() {
        console.log('Welcome!');
    }
}

class Skoda extends Car {
    modelName(){
        console.log(`This is a Skoda`);
    }
}

Skoda.greet(); // Welcome!

```

```
    To know more about static just read the static Method documentation.
```

- `Inheriting from built-in types`: Inheritance in javascript allows us to inherit non-primitive built-in types in javascript such as array, set, map etc.

```
class Queue extends Array {
    add(e) {
        super.push(e)
    }
}
let a1 = new Queue()
a1.add('Hery')
console.log(a1) // ['Hery']
```

### `Polymorphism`:

`Polymorphism` means the same function with different signatures is called many times.
This word has taken from `poly` means `many` and `morphism` means transforming one form into another.

In real life, for example, a boy at the same time may be a student, a class monitor, etc. So a boy can perform different operations at the same time. This is called polymorphism.

```
class Calculation {
    constructor(a, b) {
        this.a = a;
        this.b = b;
    }
    add() {
        console.log(this.a + this.b);
    }
}
class addition extends Calculation {
    constructor(a,b,c) {
        super(a,b);
        this.c = c;
    }
    add() {
        console.log(this.a + this.b + this.c);
    }
}
var add = new addition(1,2,3)
console.log(add)
```

In the above example we create different classes with the same method name and different definitions of methods and this behaviour is known as `polymorphism`

### `Abstraction`:

Abstract classes can be defined as classes that cannot be instantiated, i.e., whose object reference cannot be created and contains one or more abstract methods within it.

`Example: How to implement Abstraction in JavaScript`
By utilizing the `class` keyword, we will now define `Person` as an `Abstract class`, having a `constructor()`, and an `info()` Abstract method:

```
class Person {
  constructor() {
    if (this.constructor == Person) {
      throw new Error("Your Error Message...");
        }
    }
    info() {
        throw new Error(" Added abstract Method has no implementation");
    }
}
```

Next, we will create a subclass `Teacher`, which inherits the properties and method of the `Person` class using `Inheritance`

```
class Teacher extends Person {
    info() {
        //super.display(); // Invoking method of parent class
        console.log("I am a Teacher");
    }
}
var teacher1 = new Teacher();
teacher1.info();
```

In the above example If the Parent class abstract `info()` method is invoked in the `Teacher` class, it will throw an error.
