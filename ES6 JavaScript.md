# ES6 JavaScript
## ES5, ES6, ES2016, ES2017, ES.Next
  - ECMAScript vs JavaScript
    ECMAScript is basically the spec for this language ECMAScript defines the syntax, semantics, and behavior of the JavaScript language. <br/>
    Javascript is just the implementation of the ECMAScript spec.
  - What do most environments support?
    Most evnironments support ES5
  - Transpilers (Babel, TypeScript, CoffeeScript, etc.)
    Transpilers are tools used in JavaScript development to convert code written with newer language features (such as ES6) into code that older browsers or environments can understand (like ES5). They enable developers to use modern language features while ensuring compatibility with older systems.
  - Which syntax should we use?
    Use syntax that meets your project's requirements and supports your target environments. Consider factors like compatibility, community adoption, project needs, and personal preference when choosing syntax features

## Closures
  - Functions that refer to variables declared by parent function still have access to those variables
  - Possible because of JavaScript's scoping
  - Some code snippets shoud be noted their outputs
    <a id="closureBug"></a>
    ```
    function makeArrayFunction() {
        const arr = []
        for(var i = 0; i<5;i++){
            arr.push(function () {console.log(i)})
        }
        console.log(i);
        return arr;
    }
    
    const functionArr = makeArrayFunction();
    functionArr[0]();
    functionArr[1]();
    ```
    ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/8e65954c-01d6-4e52-a1bb-c2f01b92e1c7) <br/>
    We can see `var i` have access to entire function `makeArrayFunction()` and during `functionArr[0]()` and `function[1]()` called bother have accessed the value after last execution of i.
    ```
    function makeArrayFunction() {
        const arr = []
        for(let i = 0; i<5;i++){
            arr.push(function () {console.log(i)})
        }
        // console.log(i);  //This will give Reference error as i is not defined in this scope
        return arr;
    }
    
    const functionArr = makeArrayFunction();
    functionArr[0]();
    functionArr[1]();
    ```
    ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/9bfb3a92-fcfd-4887-8a15-7c2a056fb055) <br/>
    In above example `console.log(i)` will raise Reference error as `i` is not defined in this scope and during `functionArr[0]()`,`functionArr[1]()` call it used the values of i during its scope inside `sayHello()`

    ```
    function makeHelloFunction() {
        const message = "Hello!";
        function sayHello() {
            console.log(message)
        }
        return sayHello
    }
    
    const sayHello = makeHelloFunction();
    console.log("type of message:", typeof message);
    console.log(sayHello.toString());
    sayHello()
    ```
    ##### Output
    ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/cf6a5d8d-9746-4d43-8f5f-e486251e39e7)

## Imediately Invoked Function Expression
  - A functions expression that gets invoked immediately
  - Creates closure
  - Doesn't add to or modify global object
    ```
    const sayHello = (function () {
        var message = "Hello!";
        function sayHello() {
            console.log(message)
        }
        return sayHello
    })();
    
    sayHello();
    ```

  - Solution to the Closure Bug of first example of above [closures](#closureBug) heading using IIFE
    ```
    function makeArrayFunction() {
        const arr = []
        for(var i = 0; i<5;i++){
            arr.push((function (x) {
                return function (){console.log(x)}
            })(i))
        }
        console.log(i);
        return arr;
    }
    
    const functionArr = makeArrayFunction();
    functionArr[0]();
    functionArr[1]();
    ```
    ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/720e524e-cd5c-4a33-94ad-2842d446fe1f)

    - Here `functionArray[0]()` and `function[1]()` both will give different outputs as that functions inside `makeArrayFunction()` was immediately invoked.
      <br /><br />
    - Another application of IIFE
      ```
      const counter = (function(){
          let count = 0;
      
          return {
              inc: function() {count = count + 1},
              get: function() {console.log(count)},
              dec: function() {count = count - 1}
          }
      })();
      
      counter.get();
      counter.inc();
      counter.inc();
      counter.get();
      counter.dec();
      counter.get();
      ```
      ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/b4aafd8f-c528-424b-82b6-785aef2c36d2)

## First-Class Functions
  - Functions are treated the same way as any other value
    - Can be assigned to variables, array values, object values
    - Can be passed as arguement to other functions
    - Can be returned from functions
  - Allows for the creation of higher-order functions
    - Either takes one or more functions as arguements or returns a function
    - map(), filter(), reduce()
      ```
      const x = [0,1,2,3];
      
      function addOne(number) {
          return number + 1;
      }
      function sum(x, y){
          return x+y;
      }
      function sumThree(x,y,z){
          return x+y+z;
      }
      console.log("X: ",x);
      console.log("x.map(addOne): ",x.map(addOne));
      console.log("filtering X where element>1: ",x.filter(num=>num>1))
      console.log("reducing x using sum method which takes two arguement and make it one: ",x.reduce(sum));
      ```
    - `map()` maps the function to every element of array
    - `filter()` filters the elements which holds true
    - `reduce()` reduces by taking two elements and making it one and iteration it till it becomes single
    - Arguements of `reduce()` are in the form `reduce(callbackfn: (previousValue: number, currentValue: number, currentIndex: number, array: number[]) => number)`
    - We can also define high order functions
      ```
      // HigheOrderFinctions
      function map(arr, fn){
          const newArr = []
          arr.forEach(element => {
              newArr.push(fn(element));
          });
          return newArr;
      }
      function addOne(number){
          return number + 1;
      }
      
      const x = [0,1,2,3];
      
      console.log(map(x, addOne));
      ```
      ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/1004a92e-3bcc-40bc-897c-a509689d640b)


## Synchromous? Async? Single-Threaded?
  - JavaScript is a single-threaded, synchronous language
  - A function that takes a long time to run will cause a page to become unresponsive
    ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/9c346d35-b5be-41a2-bbf2-0f4697e087ec)
    This will hang out webpage for 10 seconds, We can't do anything else on that webpage

  - JavaScript has functions that act asynchronously <a id="asyncExample"></a>
    ```
    function printOne(){
        console.log("one");
    }
    
    function printTwo(){
        console.log("two");
    }
    
    function printThree(){
        console.log("three");
    }
    
    
    setTimeout(printOne, 1000);
    setTimeout(printTwo, 0);
    printThree();
    ```
    ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/48a9c680-4bdc-461c-8a1a-c96c1267fa9b) <br />
    We can see that `printTree()` executed first even after `printTwo()` has timeout 0, bucause `setTimeout()` is asynchronous function and printTree is asynchronous functions and `printThree()` will get into the execution from stack later.

  - But how can it be both synchronous and asynchronous?

## Asynchronous JavaScript
  ### Execution stack
  - Functions invoked by other functions get added to the call stack
  - When functions complete, they are removed from the stack and the frame below continues executing
  - Browser APIs
  - Function queue
  - Event loop
    ```
    function addOne(number){
        throw new Error("Oh no here we got an error!")
    }
    
    function getNum() {
        return addOne(10);
    }
    
    function c(){
        console.log(getNum() + getNum());
    }
    
    c()
    ```
    ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/81dd22d7-f3d9-4859-8a89-974e6c3df163) <br />
    We can see error raised and how the functions were stacked
    
### How Asynchronous JavaScript works
  ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/49c47c9e-fcd4-426c-990b-0bc1f860f0f2)
  - Execution stack have current executing function [refer this examle](#asyncExample)
  - Browser API have APIs handled by browser any anync function is API sent to Browser API and Browser will send it back to function queue when ready
  - Function Queue is queue of ready functions to be excuted
    ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/11ea434f-c513-45cc-80e9-a9e073d9b664)
  - Firstly `setTimeout(printOne,1s)` and  `setTimeout(printTwo,0s)` will be sent to the Browser API and then `printThree()` will be executed, at the same time this browser API will send `printTwo()` function in the function queue as 0 seconds elapsed and to be excuted but it will wait for the already present function in execution stack `printThree()` executed successfully then it will go to execution stack.
  ### Aynchronous functions
  - setTimeout()
  - XMLHttpRequest(), jQuery.ajax(), fetch()
  - Database calls
## Callbacks
  - Control flow with asynchronous calls
  - Execute function once asynchronous call returns value
    - Program doesn't have to halt and wait for value
  1. Simple Callback Example:
     ```
      function greet(name, callback) {
          console.log("Hello, " + name + "!");
          callback(); // Call the callback function
      }
      
      function sayGoodbye() {
          console.log("Goodbye!");
      }
      
      greet("Aniket", sayGoodbye);
     ```
     ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/46151ecf-032b-4fcf-8b9d-3e995ebbaaaa)

  2. Asynchronous callback Example(setTimeout):
       ```
      console.log("Start");
      setTimeout(function() {
          console.log("Timeout done!");
      }, 2000); // Execute the callback after 2000 milliseconds (2 seconds)
      console.log("End");
       ```
     ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/8d85183a-e5b9-4ae4-a583-e8b6c76e8d8b)

  3. Callback with parameters:
       ```
      function add(a, b, callback) {
          let result = a + b;
          callback(result);
      }
      
      function displayResult(result) {
          console.log("The result is: " + result);
      }
      
      add(5, 3, displayResult);
       ```
     ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/9dac4a47-9eb4-4588-8873-43b2f67fa361)

## Promises
  - Alleviate "callback hell"
  - Allows you to write code that assumes a value is returned within a success function
  - Only needs a single error handler
  1. Basic Promise Example
     ```
      let myPromise = new Promise(function(resolve, reject) {
          // Asynchronous operation (e.g., fetching data from a server)
          setTimeout(function() {
              let data = "Hello, world!";
              resolve(data); // Resolve the promise with the data
          }, 2000);
      });
      
      myPromise.then(function(data) {
          console.log(data); // Output: Hello, world!
      }).catch(function(error) {
          console.error(error);
      });
     ```
  2. Chaining Promises
     ```
      function getData() {
          return new Promise(function(resolve, reject) {
              // Asynchronous operation
              setTimeout(function() {
                  let data = "Hello, world!";
                  resolve(data);
              }, 2000);
          });
      }
      
      getData().then(function(data) {
          console.log(data); // Output: Hello, world!
          return "Another Promise";
      }).then(function(data) {
          console.log(data); // Output: Another Promise
      }).catch(function(error) {
          console.error(error);
      });
     ```
  ### Callbacks vs Promises
  1. Readability
     ```
      // Callback Example
      function fetchData(callback) {
          setTimeout(function() {
              callback("Data received");
          }, 2000);
      }
      
      fetchData(function(data) {
          console.log(data); // Output: Data received
      });
     ```
     ```
      // Promise Example
      function fetchData() {
          return new Promise(function(resolve) {
              setTimeout(function() {
                  resolve("Data received");
              }, 2000);
          });
      }
      
      fetchData().then(function(data) {
          console.log(data); // Output: Data received
      });
     ```
     ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/2bc40e72-e7bb-495d-9b35-edf724338b9d) <br />
     Promises often result in cleaner and more readable code compared to nested callbacks, especially when dealing with multiple asynchronous operations or error handling.
     
  2. Error handling
     ```
      // Callback Example
      function fetchData(callback) {
          setTimeout(function() {
              if (Math.random() < 0.5) {
                  callback(null, "Data received");
              } else {
                  callback(new Error("Failed to fetch data"));
              }
          }, 2000);
      }
      
      fetchData(function(err, data) {
          if (err) {
              console.error(err);
          } else {
              console.log(data);
          }
      });
     ```
     ```
      // Promise Example
      function fetchData() {
          return new Promise(function(resolve, reject) {
              setTimeout(function() {
                  if (Math.random() < 0.5) {
                      resolve("Data received");
                  } else {
                      reject(new Error("Failed to fetch data"));
                  }
              }, 2000);
          });
      }
      
      fetchData().then(function(data) {
          console.log(data);
      }).catch(function(err) {
          console.error(err);
      });
     ```
     ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/478e4993-988d-4626-b70d-4bd4c84be870) <br />
     Promises provide a cleaner syntax for error handling using the catch() method, which can centralize error handling for multiple asynchronous operations.
     
  3. Ease of usage
     ```
      // Callback Example
      function fetchData(callback) {
          setTimeout(function() {
              callback("Data received");
          }, 2000);
      }
      
      fetchData(function(data) {
          processData(data, function(result) {
              displayResult(result, function() {
                  console.log("Result displayed");
              });
          });
      });
     ```
     ```
      // Promise Example
      function fetchData() {
          return new Promise(function(resolve) {
              setTimeout(function() {
                  resolve("Data received");
              }, 2000);
          });
      }
      
      fetchData().then(function(data) {
          return processData(data);
      }).then(function(result) {
          return displayResult(result);
      }).then(function() {
          console.log("Result displayed");
      });
     ```
     ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/318e3be1-1760-4a42-97de-6bfb7cc46558) <br />
     Promises simplify the chaining of asynchronous operations and eliminate the problem of "callback hell" (deeply nested callbacks), making the code easier to understand and maintain. <br />
     Callbacks are more straightforward and suitable for simple asynchronous tasks, Promises offer improved readability, error handling, and ease of use for more complex asynchronous workflows. However, it's important to note that with the introduction of async/await in modern JavaScript, Promises have become even more convenient and powerful for handling asynchronous code.

## Async Await
  - Introduced in ES2017
  - Allows people to write async code as if it were synchronous
