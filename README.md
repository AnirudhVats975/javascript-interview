# javascript-interview

### 1.Is Javascript single-threaded?

Yes, JavaScript is a single-threaded language. This means that it has only one call stack and one memory heap. Only one set of instructions is executed at a time.

Also, Javascript is Synchronous and blocking in nature. meaning that code is executed line by line and one task must be completed before the next one begins

However, JavaScript also has asynchronous capabilities, which allow certain operations to be executed independently of the main execution thread. This is commonly achieved through mechanisms like callbacks, promises, async/await, and event listeners. These asynchronous features enable JavaScript to handle tasks such as fetching data, handling user input, and performing I/O operations without blocking the main thread, making it suitable for building responsive and interactive web applications.


### 2.What is Promise and Promise chaining?

Promise: A Promise is an object in JavaScript used for asynchronous computations. It represents the result of an asynchronous operation, the result may be resolved or rejected.

Promises have three states:

Pending: The initial state. This is the state in which the Promise’s eventual value is not yet available.
Fulfilled: The state in which the Promise has been resolved successfully, and the eventual value is now available.
Rejected: The state in which the Promise has encountered an error or has been rejected, and the eventual value cannot be provided.

Promise constructor has two parameters (resolve, reject) which are functions. If the async task has been completed without errors then call the resolve function with message or fetched data to resolve the promise.
If an error occurred then call the reject function and pass the error to it.
we can access the result of promise using .then() handler.
we can catch the error in the .catch() handler.
```
// Creating a Promise
const fetchData = new Promise((resolve, reject) => {
  // Simulate fetching data from a server
  setTimeout(() => {
    const data = 'Some data from the server';
    // Resolve the Promise with the retrieved data
    resolve(data);
    // Reject the Promise with an error
    // reject(new Error('Failed to fetch data'));
  }, 1000);
});

// Consuming the Promise
fetchData
  .then((data) => {
    console.log('Data fetched:', data);
  })
  .catch((error) => {
    console.error('Error fetching data:', error);
  });

```
Promise chaining: The process of executing a sequence of asynchronous tasks one after another using promises is known as Promise chaining.
It involves chaining multiple .then() methods to a Promise to perform a series of tasks in a specific order.

```
new Promise(function (resolve, reject) {
  setTimeout(() => resolve(1), 1000);
})
  .then(function (result) {
    console.log(result); // 1
    return result * 2;
  })
  .then(function (result) {
    console.log(result); // 2
    return result * 3;
  })
  .then(function (result) {
    console.log(result); // 6
    return result * 4;
  });
```
expample:-
```
const fetchData = new Promise((resolve, reject) => {
  fetch("https://jsonplaceholder.typicode.com/users")
    .then((response) => {
      if (!response.ok) {
        throw new Error("Cannot access this data");
      }
      return response.json();
    })
    .then((data) => {
      resolve(data);
    })
    .catch((error) => {
      reject(error);
    });
});

fetchData
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.error(error);
  });
```

### 3.What is async/await ?

Async/await is a modern approach to handling asynchronous code in JavaScript. It provides a more concise and readable way to work with Promises and async operations, effectively avoiding the “Callback Hell” and improving the overall structure of asynchronous code.
In JavaScript, the async keyword is used to define an asynchronous function, which returns a Promise.
Within an async function, the await keyword is used to pause the execution of the function until a Promise is resolved, effectively allowing for synchronous-looking code while working with asynchronous operations.

```
async function fetchData() {
  try {
    const data = await fetch('https://example.com/data');
    const jsonData = await data.json();
    return jsonData;
  } catch (error) {
    throw error;
  }
}

// Using the async function
fetchData()
  .then((jsonData) => {
    // Handle the retrieved data
  })
  .catch((error) => {
    // Handle errors
  });
```
In this example, the fetchData function is defined as an async function, and it uses the await keyword to pause the execution and wait for the fetch and json operations, effectively working with Promises in a way that resembles synchronous code.


### 4.Describe Arrow functions.

The ES6 Javascript version introduced Arrow functions. With the Arrow functions, we can declare functions using new and shorter syntax. These functions can only be used as function expressions. The declaration of these functions is done without using the function keyword. Moreover, if there is a single returning expression, then even the return keyword is not needed. Additionally, wherever the code occurs in a single line only, we can omit the curly {} braces. If there is only one argument in a function, then we can omit even the () parenthesis. ?

### 5.What are classes in Javascript?

Classes in Javascript are templates for building objects. Classes bind the data with code so that the data works as per the code. They were introduced in the ES6 version of Javascript and while they were created on prototypes, they also have syntax and semantics that are not common with ES5. Classes can be seen as special functions. There are two components of class syntax: class expressions and class declarations.

Class expressions are one of the ways to define classes. They may or may not have names. If a class expression has a name, it is held locally in the class body but can be accessed through the name property. Before using class expressions, one must declare them.

Another way to define classes is class declaration. For declaring a class, the class keyword must be followed by the class name.

One class may use the properties of methods of another class by using the extend keyword. Classes in Javascript must follow the strict mode. If the strict mode is not followed, errors will appear.

```
// Class Declaration
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
  }
}

// Creating an instance of the Person class
const person1 = new Person('Alice', 30);
person1.greet();
```

```

// Unnamed Class Expression
const Animal = class {
  constructor(type, sound) {
    this.type = type;
    this.sound = sound;
  }

  makeSound() {
    console.log(`${this.type} makes ${this.sound} sound.`);
  }
};

// Creating an instance of the Animal class
const animal1 = new Animal('Dog', 'Bark');
animal1.makeSound(); // Output: Dog makes Bark sound.

// Named Class Expression
const Car = class Car {
  constructor(model, year) {
    this.model = model;
    this.year = year;
  }

  displayInfo() {
    console.log(`This is a ${this.year} ${this.model}.`);
  }
};

// Creating an instance of the Car class
const car1 = new Car('Toyota Corolla', 2020);
car1.displayInfo();

```

### 6.Methods for Defining JavaScript Objects?
1.JavaScript Object Literal
```
 const person = {
  name : "anirudh",
  age  :25,
  geetingData : function() {
  console.log(`Hello, my name is ${this.name}`);
  }
 } 
 person.geetingData();
```


2.Using the new Object() syntax
```
 const person = new Object(); 
  person.name = "anirudh",
  person.age  =25,
  person.geetingData = function() {
  console.log(`Hello, my name is ${this.name}`);
  }
 
 
 person.geetingData();
```

3.Constructor Functions
```
function Person(name, age){
 this.name = name,
 this.age = age,
 this.geetingData = function() {
  console.log(`my name is ${this.name} and my age is ${this.age}`)
 }
}
 
const person1 = new Person("anriudh", 20);
person1.geetingData();
 
```
4.ES6 Classes
```
class Person{
   constructor(name, age){
    this.name = name,
    this.age = age
   }   
   getingData() {
    console.log(`my nmae is ${this.name} and my age ${this.age}`)
   }
}
 const person1 = new Person("anirudh", 25);
 person1.getingData();
```
5.Object.create() Method

```
 const person = {
  geeting : function(){
    console.log(`my name is ${this.name} and my age is ${this.age}`)
  }
 }
 
 const Person1 = Object.create(person);
  Person1.name = "anirudh";
  Person1.age = 25;
  
  Person1.geeting();

```

### 7.What's the difference between undefined and not defined in JavaScript?
JavaScript if you try to use a variable that doesn't exist and has not been declared, then JavaScript will throw an error var name is not defined and the script will stop executing thereafter. But If you use typeof undeclared_variable then it will return undefined.

```
console.log(myname); //not define

console.log(typeof(myname)); //undefine
```

### 8.JavaScript Patterns

### Design Patterns  :-
Design patterns are concepts to performantly solve commonly recurring problems in software architecture.
Over the years, the JavaScript ecosystem and language has changed rapidly, and design patterns that used to be valuable some years ago may not be as valuable as they used to be.

### 1.Module Pattern
Split up your code into smaller, reusable pieces

ES2015 introduced built-in JavaScript modules. A module is a file containing JavaScript code and makes it easy to expose and hide certain values.
The module pattern is a great way to split a larger file into multiple smaller, reusable pieces. It also promotes code encapsulation, since the values within modules are kept private inside the module by default, and cannot be modified. Only the values that are explicitly exported with the export keyword are accessible to other files.

Key Characteristics of the Module Pattern:-

Encapsulation: It encapsulates private variables and methods to prevent them from being accessed directly from the outside.
Public API: It exposes only certain methods and properties, creating a clear interface for interacting with the module.
Self-contained: Each module can be developed and tested independently.

Advantages of the Module Pattern :-

Code Organization: It helps in organizing code into manageable and self-contained units.
Encapsulation: It hides implementation details, exposing only the necessary parts.
Reusability: Modules can be easily reused across different parts of the application.
Maintainability: Encapsulated code is easier to maintain and test.


### 9.JavaScript deep copy and  shallow copy with example.

### Shallow Copy

Shallow copy method creates a copy where the source and the copied variable reference remain the same. This means that modifications made in one place would affect both places.

```
const first_person = {
name: "Jack",
age: 24,
}

const second_person = first_person;

second_person.age = 25;

console.log(first_person.age); // output: 25
console.log(second_person.age); // output: 25

```

### Deep Copy

Deep copy method creates a copy where the source and the copied variable reference are completely different. This means that modifications made in one place would only affect the variable where we are making a change.

1.Spread (...) operator

```
const first_person = {
name: "Jack",
age: 24,
}

const second_person = { ...first_person };

second_person.age = 25;

console.log(first_person.age); // output: 24
console.log(second_person.age); // output: 25

```

Note - In case of nesting, the spread operator creates a shallow copy.

```
const first_person = {
  name: "Jack",
  age: 24,
  address: {
    apartment: "A",
    city: "London"
  }
};

const second_person = { ...first_person };

second_person.age = 25;
second_person.address.apartment = "N";
console.log(first_person.address.apartment); // output: N
console.log(second_person.address.apartment); // output: N
```

2.JSON.parse() and JSON.stringify()

```
const first_person = {
  name: "Jack",
  age: 24,
  address: {
    apartment: "A",
    city: "London"
  }
};

const second_person = JSON.parse(JSON.stringify(first_person));

second_person.age = 25;
second_person.address.apartment = "N";
console.log(first_person);
console.log(second_person);

```

### 10. impliment the deep clone function?

```
function deepClone(obj) {
  // Check if the input is null or not an object
  if (obj === null || typeof obj !== 'object') {
    return obj;
  }

  // Handle Date objects
  if (obj instanceof Date) {
    return new Date(obj);
  }

  // Handle Array
  if (Array.isArray(obj)) {
    const copy = [];
    for (let i = 0; i < obj.length; i++) {
      copy[i] = deepClone(obj[i]);
    }
    return copy;
  }

  // Handle Object
  const copy = {};
  for (const key in obj) {
    if (obj.hasOwnProperty(key)) {
      copy[key] = deepClone(obj[key]);
    }
  }

  return copy;
}

// Example usage:
const original = {
  a: 1,
  b: {
    c: 2,
    d: [3, 4],
    e: new Date(),
  },
};

const deepCopy = deepClone(original);

console.log(deepCopy); // { a: 1, b: { c: 2, d: [3, 4], e: <Date> } }
console.log(deepCopy.b === original.b); // false (different objects)

```

### 11.What is a Polyfill?
A piece of code called polyfill is used to add support for more recent features in earlier browsers that don't already have native support for them.
For instance, let's pretend 💭 that as part of their language iteration, JavaScript releases a new function, let's say x. Now, this feature might not be supported by all older browsers. However, as developers, we would prefer that our apps function across all browsers. Using bespoke code, polyfills assist us in making this achievable.

### Polyfill for map()

```
Array.prototype.myMap =  function(callback){
   let temp = [];
   for(let i =0; i< this.length; i++){
     temp.push(callback(this[i],i,this));
   }
   
   return temp;
}

const nums=[1,2,3,4];
const multiply=nums.myMap((x)=>{
    return x*2;
})
console.log(multiply);
```

### Polyfill for filter()

```

Array.prototype.myFilter=function(callback){
    let temp=[];
    for(let i=0;i<this.length;i++)
    {
        if(callback(this[i],i,this))
            temp.push(this[i]);
    }
    return temp;
}
//Performing filter method through custom made filter called myFilter
const nums=[1,2,3,4];
const FilterOdd=nums.myFilter((x)=>{
   return x%2;
})
console.log(FilterOdd);

```

### Polyfill for reduce()

```
Array.prototype.myReduce=function(callback,initial_value){
    var acc=initial_value;
    for(let i=0;i<this.length;i++)
    {
        acc=acc?callback(acc,this[i],i,this):this[i];
    }
    return acc;

}
//Performing reduce method through custom made reduce called myReduce
const nums=[1,2,3,4];
const sum=nums.myReduce((acc,curr,i,nums)=>{
   return acc+curr;
},0);
console.log(sum)

```


### 12.f Web APIs provided by the browser?

### 1.Storage API
The Storage API in JavaScript provides mechanisms for storing data on the client side, allowing web applications to persist data even after the user navigates away from the page or closes the browser. The two primary components of the Storage API are LocalStorage and SessionStorage.

 ### 1 LocalStorage
Persistent Storage: Data stored in LocalStorage is persistent, meaning it remains available even after the browser is closed and reopened. The data is stored per domain, so it’s available across all pages of a web application on the same domain.
Capacity: Typically, LocalStorage can store around 5-10 MB of data, depending on the browser.
Synchronous API: All operations on LocalStorage are synchronous, meaning they block the main thread while reading or writing data.

```
localStorage.setItem('username', 'JohnDoe');

const username = localStorage.getItem('username');
console.log(username); // Outputs: JohnDoe

localStorage.removeItem('username');

localStorage.clear();

console.log(localStorage.length);
```


### 12.What is call method?
The call() method in JavaScript is used to invoke a function with a specified this value and optional arguments. It allows you to execute a function in a specific context, overriding the default value of this.


```
 const person1 = {
  name : "anirudh",
  work  : "front end developer"
 }
 
  const person2 = {
  name : "ashu",
  work  : "backend end developer"
 }
 
 function getInfo(city){
  console.log(this.name + " " + this.work + " " +  "work in" +  " " +  city);
 }
 
const result= getInfo.call(person1, "delhi");
```




















