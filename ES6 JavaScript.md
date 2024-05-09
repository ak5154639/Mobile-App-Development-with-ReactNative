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
    ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/8e65954c-01d6-4e52-a1bb-c2f01b92e1c7)
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
    ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/9bfb3a92-fcfd-4887-8a15-7c2a056fb055)
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
    
