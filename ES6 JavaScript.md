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
