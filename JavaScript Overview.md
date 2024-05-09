# Javascript Overview
## Javascript is Interpreted
  - Each browser has its own JavaScript engine, which either interprets, or uses lazy compilation
  - Some interpreters with browsers are:
    - V8: Chrome and Node.js
    - SpiderMonkey: Firefox
    - JavaScriptCore: Safari
    - Chakra: Microsoft Edge/IE
  - They each implement the ECMAScript standard, but may differ for anything not defined by the standard

## Syntax
  ```
  const firstName = "Aniket"    //semicolons can be omiited
  const lastName = "Sharma";
  const arr = ["student", 24, true, function(){
  console.log('hi')}
  ];
  
  // Comment
  for (let i = 0; i<arr.length; i++){
    console.log(arr[i]);
  }
  ```
  ### Output:
  ![image](https://github.com/ak5154639/ReactNative-Notes/assets/60311459/e457d187-c101-44d4-b306-956cdb5ca70a)


## Types
  - Dynamic typing
  - Primitive types (no methods, immutable)
      - undefined(absence of value) - on declaring any variable, JS automatically assigns is undefined
      - null(absence of value) - when we explicitly assign value
      - boolean
      - number
      - string
      - (symbol)
  - Objects

<details>
  <summary><strong>Bug</strong> On consoling <code>typeof(null)</code> we will get <code>Object</code> as ouput</summary>

  The reason why `typeof null` returns `"object"` in JavaScript is considered a historical quirk and is often considered a mistake or an oversight in the language's design.

When JavaScript was created, its initial implementation had a tagging system for its values. Each value in JavaScript had a tag that indicated its type. The tag for objects was `0x1`, and `null` was represented by the value `0x1` with the least significant bit set to 0, which effectively means it was a special kind of object. However, this doesn't mean that `null` is actually an object; it's a primitive value with its own unique characteristics.

Due to this historical reason, when you use `typeof null`, JavaScript returns `"object"`. This behavior persists for compatibility reasons, as changing it could potentially break existing code that relies on this behavior.

So, while `null` is not an object in the usual sense (it's a primitive value representing the absence of any object value), the `typeof` operator returning `"object"` for `null` is a result of JavaScript's historical design choices.
</details>

## Typecasting
  - Explicit vs Implicit coercion
      ```
      const x = 42;
      const explicit = String(x);      // explicit === "42"
      const implicit = x + "";          // implicit === "42"
      ```
  - == vs ===
      - == coerces the types
      - === requires equivalent types
  ### Examples
  ```
    console.log(typeof(string));
    console.log("42" === 42);
    console.log(42 === 42);
  ```
  #### Output
  ![image](https://github.com/ak5154639/ReactNative-Notes/assets/60311459/c72610c3-a4bf-49d0-943b-6b2b4e91dfb3)

  - Falsy values
      - undefined
      - null
      - false
      - +0, -0, NaN
      - ""
  - Truthy values
      - {}
      - []
      - everythning else
  > In Javascript arrays, functions and objects all are objects.

## Primitives vs Objects
  - Primitives are immutable
  - Objects are mutable and stored by reference
    #### Three methods to create objects:
    ```
    // METHOD 1
    const  o = new Object()
    o.firstName = "Aniket"
    o.lastName = 'Sharma'
    o.isStudent = true
    o.greet = function() {
        console.log("hi")
    }

    // METHOD 2
    const o2 = {}
    o2.firstName = "Aditya"
    o2['lastName'] = "Sharma"
    const key = "isStudent"
    o2[key] = true
    o2['greet'] = function() {
        console.log("hello")
    }

    // METHOD 3
    const o3 = {
        1 : "test"    //keys can be numbers and implicitly casted to string as "1"
        firstName : "Samar",
        lastName : "Bisht",
        isStudent : true,
        greet : function() {
            console.log("HI")
        },
        address : {     //objects can be nested
            houseNumber: 2123,
            street: 72,
            area: "NIT Faridabad"
        }
    }
    ```
    | On Consoling | Output | Remarks |
    |--------------|--------|---------|
    | `o3.address` | ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/2c794a67-2a1d-4b00-ace1-0fc4c0709917) | accesing values using keys of an object using dot notation |
    | `o3.address.houseNumber` | ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/ffabca49-086c-4074-8c3a-6f84e5a2c3fc) | accesing values using keys of nested object using dot notation |
    | `o3.address['houseNumber']` | ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/ffabca49-086c-4074-8c3a-6f84e5a2c3fc) | accesing value of key as string inside square braces |
    | `o3['1']` | ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/3a2d6e79-e94b-47eb-bfe6-da4834d69eb7) | accesing value of key as string inside square braces as it expects string |
    | `o3[1]` | ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/d7c9b255-c275-4413-a81d-ed7a41df2150) | 1 will be coerced to string as square braces expects string |
    
## Object Mutation
  - Objects are mutable and stored by reference
    ```
    const obj = {
        a: 'a',
        b:'b'
    }
    const o2 = obj;
    o2.a = "new";
    console.log(obj.a);
    ```
    above code will have output `new` as `obj.a` and `o2.a` both referencing to same object.

  ### How can we make this two different objects
  1. Manually create other duplicte object instead of assigning by object name this could be weird solution.
  2. Using `Object.assign()` method.
  ```
  const obj = {
      a: 'a',
      b:'b'
  }
  const o2 = Object.assign({}, obj);
  o2.a = "new";
  console.log(obj.a);
  ```
  > There is even a problem with this, can you tink about the output of code snippet below
  ```
  const obj = {
      a: 'a',
      b:'b',
      nest: {
          key: "this is key"
      }
  }
  const o2 = Object.assign({}, obj);
  o2.nest.key = "new";
  console.log(obj.nest.key);
  ```
  output of above code snippet will be `new` as nested object `nest` will be refering to same object in both `obj` as well as `o2`.
  ### Thw How can we do so **DEEPCOPY**
  ```
  const obj = {
      a: 'a',
      b:'b',
      nest: {
          key: "this is key"
      }
  }
  
  // deepcopy
  function deepCopy(obj) {
      // check if vals are object then deepcopy that
      // else return the value
      const keys = Object.keys(obj);
  
      const newObj = {}
  
      for (let i = 0; i < keys.length; i++){
          const key = keys[i];
          if (typeof(obj[key]) === 'object'){
              newObj[key] = deepCopy(obj[key])
          } else {
              newObj[key] = obj[key]
          }
      }
      return newObj
  }
  
  const o2 = deepCopy(obj);
  
  o2.nest.key = "changed"
  
  console.log(obj.nest.key)
  console.log(o2.nest.key)
  ```
  #### **Output**
   ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/81c2e39d-99f1-4bc8-8919-44ed6a7f862f)

## Prototype Inheritance
  - Non-primitive types have a few properties/methods associated with them
      - Arrays.prototype.push() - can be used as `arr.push(elem)`
      - String.prototype.toUpperCase() - can be used as `firstName.toUperCase()`
  - Each object stores a reference to its prototype
  - Properties/methods defined most tightly to the instance have priority
  - Using `arr.__proto__` we can check all prperties and methods associated with object.

## Prototypal Inheritance
  - Most primitive types have object wrappers
    - String()
    - Number()
    - Boolean()
    - Object()
    - (Symbol())
  - JS will automatically "box" (wrap) primitive values so you have access to methods
    ```
    42.toString()    //Errors
    const x = 42;
    x.toString()    // "42"
    x.__proto_      // [Number: 0]
    42.__proto__    //Error
    x instanceof Number  //false
    ```

    ### Why we use reference to ptototype?
      Referencing the prototype is important for creating efficient and organized code. It allows objects to inherit properties and methods from their prototype, reducing memory usage by sharing common functionality among multiple instances. This inheritance mechanism enables dynamic updates to shared behavior at runtime, optimizing performance and improving code organization for easier maintenance and scalability.
    ```
    function Person(name) {
        this.name = name;
    }
    
    // Adding a method to the prototype
    Person.prototype.greet = function() {
        console.log("Hello, my name is " + this.name);
    };
    
    // Creating instances of Person
    let person1 = new Person("Alice");
    let person2 = new Person("Bob");
    
    // Using the method from the prototype
    person1.greet(); // Output: "Hello, my name is Alice"
    person2.greet(); // Output: "Hello, my name is Bob"

    ```
    By referencing methods like `greet` through the prototype, we ensure that every instance of `Person` shares the same method. This saves memory as each instance doesn't need its own copy of the method.
    ## What's the alternative?
    ```
    // Using Object Composition
    function createPerson(name) {
        return {
            name: name,
            greet: function() {
                console.log("Hello, my name is " + this.name);
            }
        };
    }
    
    let person1 = createPerson("Alice");
    let person2 = createPerson("Bob");
    
    person1.greet(); // Output: "Hello, my name is Alice"
    person2.greet(); // Output: "Hello, my name is Bob"

    ```
     Instead of relying on prototypes for sharing behavior, we can use object composition to create objects with shared functionality. Each object has its own copy of the method, but the memory usage might be higher compared to prototypes.
    
    ### What's the danger?
    ```
    // Using prototype for inheritance
    function Animal(name) {
        this.name = name;
    }
    
    Animal.prototype.makeSound = function() {
        console.log("Animal sound");
    };
    
    function Dog(name, breed) {
        this.name = name;
        this.breed = breed;
    }
    
    // Inheriting from Animal
    Dog.prototype = Object.create(Animal.prototype);
    Dog.prototype.constructor = Dog;
    
    Dog.prototype.makeSound = function() {
        console.log("Bark");
    };
    
    let dog = new Dog("Buddy", "Labrador");
    dog.makeSound(); // Output: "Bark"
    ```
    One danger is unintentional overwriting of shared behavior. Here, we unintentionally overwrite the `makeSound` method of `Animal` in the `Dog` prototype. This can lead to unexpected behavior and bugs if not carefully managed.

## Scope
  - Variable lifetime
    - Lexical Scoping (`var`): from when they're declared until when their function ends
    - Block Scoping (`const`, `let`): until the next `}` is reached
      <table>
        <thead>
          <tr>
          <td>Code</td>
          <td>Output</td>
          <td>Explaination</td>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>
              <pre>
const thisIsConst = 50;
thisIsConst++   //Error
              </pre>
            </td>
            <td>![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/75f20c85-b603-40e6-ac12-5a72f38031a3)</td>
            <td>Values of const varibles can't be changes</td>
          </tr>
          <tr>
            <td>
              <pre>
let thisIsLet = 50;
thisIsLet = 51;
let thisIsLet = 10;              
              </pre>
            </td>
            <td>![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/65235565-0421-4fac-a0b9-70a28d42bf89)</td>
            <td>We can not redeclare the same variable in same scope</td>
          </tr>
          <tr>
            <td>
              <pre>
const obj = {};
obj.a = 51;
console.log(obj);
obj = {};
              </pre>
            </td>
            <td>![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/7352f5f6-5f2c-4e53-a73d-317d332dec95)</td>
            <td>property or attribute of const object can be modified but entire object can't be modified, const object means that can point to the same object and particular object attributes can be modified and You can notice that we didn't get output for `console.log(obj)` because of javascript's asynchronoius behavior</td>
          </tr>
          <tr>
            <td>
              <pre>
console.log(thisIsConst);
const thisIsConst = 50;
              </pre>
            </td>
            <td>![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/0a19ea6e-3934-4459-acbf-2929dc93f09e)</td>
            <td>As `const` is block scope and can not be accessed before defining</td>
          </tr>
          <tr>
            <td>
              <pre>
console.log(thisIsLet);
let thisIsLet = 50;
              </pre>
            </td>
            <td>![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/3059dc02-79c3-4c74-b59a-810ad5afa11a)</td>
            <td>For the same reason as `const` as bothe `let` and `const` are block scoped</td>
          </tr>
          <tr>
            <td>
              <pre>
var thisIsVar = 50;
thisIsVar++;
var thisIsVar = "shadowed value";
console.log(thisIsVar);
              </pre>
            </td>
            <td>![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/b564f512-588f-4753-b0a3-d3e9abdbc8d3)</td>
            <td>`var` can be overshadowed and redclared with same name</td>
          </tr>
          <tr>
            <td>
              <pre>
console.log(thisIsVar);
var thisIsVar = 50;
              </pre>
            </td>
            <td>`undefined`</td>
            <td>vars are hoisted to the top of file</td>
          </tr>
          <tr>
            <td>
              <pre>
thisIsAlsoAVBriable;
              </pre>
            </td>
            <td></td>
            <td>variables without `var`, `let`, `const` can also be declared in JS as **global** variables</td>
          </tr>
        </tbody>
      </table>
      

  #### Hoisting
  The behavior whereby a function definition declared at any point/line of file available to use at the top of a file too.
  - Function definitions are hoisted, nut not lexically-scoped initializations
      ```
      thisIsHoisted();
      
      function thisIsHoisted() {
          console.log("this is a function declared at the bottom of a file");
      }
      ```
      ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/64859621-b154-40ce-94c2-16aaa26900c0)
      <br/>Here `thisIsHoisted()` function is hoisted to the top of file and available to use anywhere in file
      ```
      thisIsNotHoisted()
      const thisIsNotHoisted = function () {
          console.log("This should not be hoisted");
      }
      ```
      ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/70b38cbf-f404-435e-9863-863e4ed474f7)
      ```
      thisIsNotHoisted()
      let thisIsNotHoisted = function () {
          console.log("This should not be hoisted");
      }
      ```
      ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/70b38cbf-f404-435e-9863-863e4ed474f7)
      ```
      thisIsNotHoisted()
      var thisIsNotHoisted = function () {
          console.log("This should not be hoisted");
      }
      ```
      ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/cd9c4821-a3d4-4a2d-8d8a-ca33d68db142)
      <br/>In above three snippets and their corresponding output we can see last one has `TypeError` not `ReferenceError` because varible containing function having declared with var is availabe to entire file but not got assigned the values i.e. anonymous function. 


## The JavaScript Engine
  - Before executing the code, the engine reads the entire file and will throw a syntax error if one is found
    + Any function definition will be saved in memory
    + Variables initializations will not be run, but lexically-scoped variable names will be declared
   
## The Global Object
  - All variables and functions are actually parameters and methods on the global object
    + Browser global object is the `window` object <br/>
      ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/73280f11-84de-4108-b148-45f0a3ae08fe)
      <br/>After executing these lines<br/>
      ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/bad678b5-0e29-4f9b-aa7d-80723afd1777)
      <br/> after scrolling down we can see</br>
      ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/e5a3ecba-bd61-4fc5-aa37-41519b89730a)
      
    + Node.js Global object is the `global` object <br/>
      ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/c5f85573-aab0-4454-82dd-ec6911f5e47b) <br/>
      ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/3022b479-1c7d-4c40-8459-427e55a2f34a)


