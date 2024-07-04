# javascript-interview

### 1.Is Javascript single-threaded?

Yes, JavaScript is a single-threaded language. This means that it has only one call stack and one memory heap. Only one set of instructions is executed at a time.

Also, Javascript is Synchronous and blocking in nature. meaning that code is executed line by line and one task must be completed before the next one begins

However, JavaScript also has asynchronous capabilities, which allow certain operations to be executed independently of the main execution thread. This is commonly achieved through mechanisms like callbacks, promises, async/await, and event listeners. These asynchronous features enable JavaScript to handle tasks such as fetching data, handling user input, and performing I/O operations without blocking the main thread, making it suitable for building responsive and interactive web applications.


### 1.What is Promise and Promise chaining?

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





