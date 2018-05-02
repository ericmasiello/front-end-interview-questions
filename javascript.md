# JavaScript


### 1. How can you copy an array in JavaScript?

Answer: Firstly, they should not just do:

```js
var arr1 = [1, 2, 3];
var arr2 = arr1;
```
If they do that, ask them what the potential downsides are of doing this? (answer: this is a reference, not a copy)

Possible solutions:

```js
var arr1 = [1, 2, 3];
var arr2 = [...arr1];

var arr3 = arr1.slice();
```

### 2. Explain what a closure is in JavaScript. Provide an example.

Answer: A closure is a function defined inside another function (called parent function) and has access to the variable which is declared and defined in parent function scope.

### 3. How do you define a class or class-like construct in JavaScript? How would you add both static and instance methods to it?

Answer: two ways: ES6 style or old school style.

```js
class Thing {
	constructor() {
	}
	
	instanceMethod1() {}
	
	instanceMethod2() {}
	
	// one way to add static methods
	static staticMethod1() {}
}

// another way to add a static methods
Thing.staticMethod2 = function() {}
```

```js
function Thing() {
}

Thing.staticMethod = function() {}

// note: this should be `function` and not an arrow function
// otherwise `this` won't mean what you think it does
Thing.prototype.instanceMethod1 = function() {}
```

### 4. What is hoisting in JavaScript?

Answer: In JavaScript variable and functions are hoisted. Let's take function hoisting first. Basically, the JavaScript interpreter looks ahead to find all the variable declaration and hoists them to the top of the function where it's declared.

### 5. Name 2 (or more) different ways `this` is applied within a function

Answer: (note the names of these e.g. "the defualt binding rule" aren't actual technical names so don't expect the interviewee to refer to these rules by these names)

1: THE DEFAULT BINDING RULE (`this` === global object)

```js
function foo() {
  return this === window;
}
foo();

function bar() {
  'use strict'
  return this === undefined;
}
bar();
```

2: THE IMPLICIT BINDING RULE: The owning object at the call site becomes this 

```js
function foo() {  
  console.log(this.name);
}
const o1 = {
  name: 'First',
  foo: foo
};
foo(); // undefined
o1.foo(); // "First"
```

3: EXPLICIT BINDING (AT CALL SITE): Use `.call` or `.apply`

```js
var name = 'The Window'; // window.name === 'The Window'

function foo(a, b) {  
  console.log(this.name, a, b);
}

var obj = { name: 'The Object' };

foo('a', 'b'); // 'The Window', 'a', 'b'

foo.call(obj, 'c', 'd'); // 'The Object', 'c', 'd'
foo.apply(obj, ['e', 'f']); // 'The Object', 'e', 'f'
```

3.1: HARD BINDING: Makes this keyword bound to a specific context

```js
var name = 'The Window';

function foo() {  
  console.log(this.name);
}

var obj = { name: 'The Object' };

foo = foo.bind(obj); //hard binding

foo(); // 'The Object'
foo.call(obj); // 'The Object'
foo.apply(obj); // 'The Object'
```

4: USING NEW: new treats any function call as a constructor

```js
var globalBar = 'bar';

function Foo() {
  this.name = 'The foo';
  console.log(this.globalBar);
}

Foo(); // logs 'bar'
var foo1 = new Foo(); // logs undefined
console.log(foo1.name); // logs 'The foo'
```

5: ARROW FUNCTIONS: Always inherit the parent context's this value

```js
var name = 'The Window';
const foo = () => {
  console.log(this.name);
}
const o1 = { name: 'Object 1' };

foo(); // 'The Window';
foo.call(o1); // 'The Window';
foo.apply(o1); // 'The Window';
foo.bind(o1)(); // 'The Window';
```


### 6. What is the drawback of creating true private in JavaScript?

```js
var Employee = function (name, company, salary) {
  this.name = name || "";       //Public attribute default value is null
  this.company = company || ""; //Public attribute default value is null
  this.salary = salary || 5000; //Public attribute default value is null

  // Private method
  var increaseSalary = function () {
    this.salary = this.salary + 1000;
  };

  // Public method
  this.dispalyIncreasedSalary = function() {
    increaseSalary();
    console.log(this.salary);
  };
};

// Create Employee class object
var emp1 = new Employee("John","Pluto",3000);
// Create Employee class object
var emp2 = new Employee("Merry","Pluto",2000);
// Create Employee class object
var emp3 = new Employee("Ren","Pluto",2500);
```
Answer: One of the drawback of creating a true private method in JavaScript is that they are very memory inefficient because a new copy of the method would be created for each instance.

Here each instance variable emp1, emp2, emp3 has own copy of increaseSalary private method.


So as recommendation don't go for a private method unless it's necessary.
