
# Technical Writing Assignment

For guidance on setting up and submitting this assignment, refer to the Marcy lab School Docs How-To guide for [Working with Short Response and Coding Assignments](https://marcylabschool.gitbook.io/marcy-lab-school-docs/fullstack-curriculum/how-tos/working-with-assignments#how-to-work-on-assignments).

## Prompt 1 | Ibrahim

Imagine you are teaching a friend about OOP. They mainly want to understand what is Encapsulation. Write a brief lesson on Encapsulation that includes the following:

- What is encapsulation?
- What major goal does this help to achieve in software engineering?
- Give an example (in code) of encapsulation.
- An explanation of how the code example demonstrates encapsulation

### Response 1

Encapsulation is a fundamental concept in object-oriented programming (OOP) that involves bundling data (attributes) and methods (functions) that operate on the data into a single unit, typically a class. It also restricts direct access to some of an object's components.

In software engineering this allows developers to create reusable code with its own scope. Allowing for a brand new expansion on skills vital to developing large applications.

Heres an example of a person class:

```js
class Person {
  // Private fields (using #)
  #name;
  #age;

  constructor(name, age) {
    this.#name = name;
    this.#age = age;
  }

  // Public methods to access private fields
  getName() {
    return this.#name;
  }

  setName(newName) {
    this.#name = newName;
  }

  getAge() {
    return this.#age;
  }

  setAge(newAge) {
    if (newAge > 0) {
      // Validation
      this.#age = newAge;
    }
  }
}

const person = new Person("Bob", 30);
console.log(person.getName()); // Output: Bob
person.setAge(35);
console.log(person.getAge()); // Output: 35

// Direct access to private fields is not allowed
console.log(person.#name); // SyntaxError: Private field '#name' must be declared in an enclosing class
console.log(person.#age); // SyntaxError: Private field '#age' must be declared in an enclosing class
```

As you can see all of the code above is Encapsulated inside og the person class. Using a technique called closures.

## Prompt 2 | Autumn

The following `friendsManager` object is an example of an interface that is **NOT** consistent and predictable:

```js
const friendsManager = {
  friends: [],
  addFriend(newFriend) {
    if (typeof newFriend !== "string") return;
    this.friends.push(newFriend);
  },
};

friendsManager.addFriend("daniel");
friendsManager.addFriend(true);
friendsManager.friends.push("emmanuel");
friendsManager.friends.push(42);
```

Explain how the code is not consistent or predictable, then provide an example in code that uses closure to make it more consistent and predictable.

### Response 2

In the code snippet above, the `friendsManager` object has a `friends` property, initialized as an empty array. The `addFriend` method is created to act as a layer of protection to prevent the friends array from being **accessed and mutated** outside of the object. However, while this is the **implied** intent of this method, the array is **currently** able to be accessed and mutated outside of the object. This creates unpredictability in the `friends` array because a programmer expects it to only be accessed through the object's methods, and might mutate the array _unintentionally_. With no safety checks in place, it soon will become easy to lose track of how friends are added to this array.

In order to **fix** this, we must declare the `friends` array as a **private** property. This will prevent the _property/array_ from being accessed outside of the object's own **methods**. To declare a property **private**, you place a `#` in front of the property name, in this case, changing `friends` to `#friends`. Now when you try to access/mutate this array outside of the object's `addFriends()` method, you will receive an error. Now, the `#friends` array cannot be mutated at all, unless we use `addFriends()` or add other methods to the object such as `deleteFriend()` or `getFriends()`.

```js
const friendsManager = {
  #friends: [],
  addFriend(newFriend) {
    if (typeof newFriend !== "string") return;
    this.#friends.push(newFriend);
  },
};

friendsManager.addFriend("daniel"); // this works, "daniel" will be added to #friends array
friendsManager.addFriend(true); // will not push "true" to the array because it is not a string
friendsManager.friends.push("emmanuel"); // will not push "emmanuel" to the array
friendsManager.friends.push(42); // will not push "42" to the array because it is not a string
```

## Prompt 3

With OOP in JavaScript, it's possible to use factory functions to achieve encapsulation and re-use them to make objects that look alike. However, factory functions have drawbacks and we often use classes instead.

How would you explain to a budding developer what the drawbacks of using factory functions are and why it is better to use classes instead?

### Response 3

## Prompt 4 | Autumn

Do some research on the history of when / how classes were introduced into JavaScript and share your findings. Your response should include:

- What version of JavaScript were classes introduced in and when did it come out?
- Why were classes introduced into JavaScript?

### Response 4

Classes were introduced into **JavaScript** in 2015, with the version release of **ES6** (EcmaScript 6). JavaScript has always followed the _Object Oriented Programming_ style, but prior to this version release, it was tedious for developers to program using this style. Classes were introduced as essentially **syntactic sugar** to make it easier for developers to write and read the objects that they have created. Prior to this version, developers had to use **constructor functions** to create an object type, and then _manually add methods_ to that object later on in your code. There was no concise way to create an object with its attached **properties and methods** all at once. With classes, the code is much better organized because all of these are defined at **initialization**.

## Prompt 5 | Ibrahim

OOP can still be achieved in JavaScript without using the `class` keyword and instead using the "Constructor Functions" and the "Prototype Chain" (look them up!)

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.greet = function () {
  return `Hi, I'm ${this.name}, and I'm ${this.age} years old.`;
};

const alice = new Person("Alice", 30);
console.log(alice.greet());
```

Provide one point that advocates for the use of this syntax and then provide a counter-argument for the use of classes instead.

### Response 5

One of the most prominent benefits of achieving OOP this way is Backward Compatibility and Flexibility: Constructor functions and the prototype chain have been the traditional way to implement OOP in JavaScript since its inception. They are supported in all JavaScript environments, including older browsers, making them a reliable choice for projects that require broad compatibility. Additionally, they provide more flexibility in terms of dynamic behavior, as you can modify the prototype chain at runtime.

Though the new method is better, it has increased readability and maintainability. The class syntax introduced in ES6 is more intuitive and easier to read, especially for developers coming from other object-oriented languages like Java or C++. It provides a cleaner and more structured way to define classes, inheritance, and encapsulation.

Adding syntax like "#" as a new way to declare private values, the "extends" keyword which allows one to extend upon classes with sub classes.

This syntax is more concise and aligns with modern programming practices, making it easier to maintain and understand, especially in larger codebases.
