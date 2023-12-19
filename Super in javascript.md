## What is super in javascript ?

A: The concept of `super keyword` comes with the idea of `inheritance` in JavaScript.It is mainly used when we want to access a variable, method, or constructor in the `base class(child class)` from the `derived class(parent class)`.

Syntax:

```
super(param);
```

Example:

```
class Rectangle {
  constructor(height, width) {
    this.name = 'Rectangle';
    this.height = height;
    this.width = width;
  }
  getName() {
    console.log('Hi, I am a ', this.name + '.');
  }
}

class Square extends Rectangle {
  constructor(length) {
    // Can't use this.height. It will throw a reference error

    // It calls the parent class's constructor
    super(length, length);

    // In derived classes, super() must be called before you
    // can use 'this'.
    this.name = 'Square';
  }
}
```

- `super` can also be used to call on `static methods` of the `parent class`:

```
class Rectangle {
    constructor() {}
    static getDescription() {
        return 'I have 4 sides';
    }
}
class Square extends Rectangle {
    constructor() {
        super()
    }
    static getDescription() {
        return super.getDescription() + ' which are all equal';
    }
}
console.log(Square.getDescription()) // I have 4 sides which are all equal
```
