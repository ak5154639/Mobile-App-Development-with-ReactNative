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
