# Classes 

Classes are a feature which basically replace constructor functions and prototypes. You can define blueprints for JavaScript objects with them.

```
class Person {
    constructor () {
        this.name = 'Ali';
    }
}

const person = new Person();
console.log(person.name);
```

In the above example, not only the class but also a property of that class (=> name ) is defined. They syntax you see there, is the "old" syntax for defining properties. In modern JavaScript projects (as the one used in this course), you can use the following, more convenient way of defining class properties:


```
class Person {
    name = 'Ali';
}
```
```
class Person {
    this.name = 'Ali';

    // Method
    printMyName() {
        console.log(this.name);
    }

    // Another way of method
    printName = () => {
        console.log(this.name);
    }
}

```
The second approach has the same advantage as all arrow functions have: The this keyword doesn't change its reference.

You can also use inheritance when using classes:


## Inheritence
```
class Human {
    constructor(age) {
        this.age = age
    }

    printAge = () => {
        console.log(this.age);
    }
}


class Person extends Human {
    constructor() {
        super();
    }

    this.name = 'Ali';

    // Method
    printMyName() {
        console.log(this.name);
    }

    // Another way of method
    printName = () => {
        console.log(this.name);
    }
}
```