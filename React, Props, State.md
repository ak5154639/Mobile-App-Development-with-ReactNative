# React, Props, State
## Classes
  - Syntax introduced in ES6
  - Simplifies the defining of complex objects with their own prototypes
  - Classes vs instances
    ```
    const d = new Date()
    console.log(d.toString());
    ```
    Here `Date` is a class and `d` is an instance of the class `Date`
  - Methods vs static methods vs properties
  - new, constructor, extends, super
    ```
    class Set {
        constructor(arr){
            this.arr = arr;
        }
        add(val){
            if(!this.has(val)){this.arr.push(val)}
        }
        delete(val){
            this.arr = this.arr.filter(x => x !== val);
        }
        has(val){
            return this.arr.includes(val);
        }
        get size(){
            return this.arr.length;
        }
    }
    
    const s = new Set([1,2,3,4,5])
    console.log(s)
    // trying to add the same value should'nt work
    s.add(1);
    console.log(s)
    // trying to ass different value and should work
    s.add(6);
    console.log(s)
    s.delete(6);
    console.log(s)
    console.log(s.size);
    ```
    ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/63cc168c-c14e-465e-9f4e-759c94292862) <br />
    Here we have defined `constructor` for the class `Set` along with four more functions `add`, `delete`, `has`, `size`, <br />
    Function `size` is defined with `get` keyword this will automatically invoked when member of object is accessed as we have used `s.size` instead of `s.size()`.
    <br/>
    JavaScript has already Set class above was just for the demonstration we will be using predefined Set class to extend and demonstrate `extends` keyword
    ```
      class MySet extends Set {
          constructor(arr){
              super(arr);
              this.originalArray = arr;
          }
      
          add(val){
              super.add(val);
              console.log(`added ${val} to the set!`);
          }
          toArray() {
              return Array.from(this);
          }
          reset(){
              return new MySet(this.originalArray)
          }
      }
      
      const s = new MySet([1,2,3,4,5]);
      console.log(s.toArray());
      s.add(6);
      console.log(s.toArray());
      s.add(7);
      console.log(s.toArray());
      console.log(s.reset().toArray());
    ```
    ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/5edd0b8d-81ba-402b-800f-747c43fb2c01) <br />
    In above example predefined class `Set` is Extended to MySet and `super()` are used to invoke methods of parent class.

## React
  - Allows us to write declarative views that "react" to changes in data
  - Allows us to abstract complex problems into smaller components
  - Allows us to write simple code that is still performant

## Imperative vs Declarative
  - How vs What
  - Imperative programming outlines a series of steps to get to what we want
  - Declarative programming just declares what we want
    Let's try to understand Imperative and Declarative usign Example of Guitar<br />
    ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/48c41902-6246-4986-8cbe-42da6bea3cfd) <br />
    ##### Pseudocode for Imperative Programming for the given example Guitar
    ```
      // Pseudocode
      const strings = ['E', 'A', 'D', 'G', 'B', 'E']
      
      function Guitar() {
          // create head and add pegs
          const head = createElement('head')
          for(let i =0; i<6; i++){
              const peg = createElement('peg')
              head.append(peg)
          }
      
      
          // create neck and add frets
          const neck = createElement('neck')
          for (let i = 0; i<19; i++){
              const fret = createElement('fret')
              neck.append(fret)
          }
      
          // create body and strings
          const body = createElement('body')
          strings.forEach(tone=>{
              const string = createElement('string')
              string.tune(tone)
              body.append(string)
          })
      
          return body
      }
    ```
    ##### Psudocode for declarative Programming for the same fiven example of Guitar
    ```
      const strings = ['E', 'A', 'D', 'G', 'B', 'E']
      
      function Guitar(){
          return (
              <Guitar>
                  {strings.map(note=><String note={note}></String>)}
              </Guitar>
          )
      }
    ```

## React is Declarative
  - Imperative vs Declarative
  - The browser APIs aren't fun to work with
  - React allows us to write what we want, and the library will take care of the DOM manipulation
    Below is imperating Programming of creating Slide using JavaScript
    ```
      const SLIDE = {
          title: 'React is Declarative',
          bullets: [
              'Imperative vs Declarative',
              'The browser APIs aren\'t fun to work with',
              'React allows us to write what we want, and the library will take care of the DOM manipulation', 
          ],
      }
      
      function createSlide(slide){
          const slideElement = document.createElement('div');
      
          // TODO: add to slide
          const title = document.createElement('h1');
          title.innerHTML = SLIDE.title;
          slideElement.appendChild(title);
      
          const list = createElement('ul');
          slide.bullets.map(bullet=>{
              const item = createElement('li');
              item.innerHTML = bullet;
              list.appendChild(item);
          })
          slideElement.appendChild(list);
      
      
          return slideElement
      }
    ```
    Below is Declarative Programming of creating Slide using React
    ```
      const SLIDE = {
          title: 'React is Declarative',
          bullets: [
              'Imperative vs Declarative',
              'The browser APIs aren\'t fun to work with',
              'React allows us to write what we want, and the library will take care of the DOM manipulation', 
          ],
      }
      
      function createSlide(slide){
          return (
              <div>
                  <h1>{slide.title}</h1>
                  <ul>
                      {slide.bullets.map(bullet=><li>{bullet}</li>)}
                  </ul>
              </div>
          )
      }
    ```

## React is Easily Componentized
  - Breaking acomplex problem into discreate components
  - Can reuse these components
    - Consistency
    - Iteration speed
  - React's declarative nature makes it easy to customize components
    ```
      <div>
          <div>
              <h1>React</h1>
              <ul>
                  <li>
                      Allows us to write declarative views that “react” to changes in data
                  </li>
                  <li>
                      Allows us to abstract complex problems into smaller components
                  </li>
                  <li>
                      Allows us to write simple code that is still performant
                  </li>
              </ul>
          </div>
          <div>
              <h1>React is Declarative</h1>
              <ul>
                  <li>
                      Imperative vs Declarative
                  </li>
                  <li>
                      The browser APIs aren’t fun to work with
                  </li>
                  <li>
                      React allows us to write what we want, and the library will take care of the DOM manipulation
                  </li>
              </ul>
          </div>
      </div>
    ```
    In above HTML code we can see code is repeated and if we want to change the style of list items or structure in some other way then we have to change at every place
    This can be eased with componetizing
    ```
      const slides = [
          {
              title: "React",
              bullets: [
                  "Allows us to write declarative views that “react” to changes in data",
                  "Allows us to abstract complex problems into smaller components",
                  "Allows us to write simple code that is still performant"
              ]
          },
          {
              title: "React is Declarative",
              bullets: [
                  "Imperative vs Declarative",
                  "The browser APIs aren’t fun to work with",
                  "React allows us to write what we want, and the library will take care of the DOM manipulation"
              ]
          }
      ]
      
      const slideShow = (
          <div>
              {slides.map(slide=><Slide slide={slide}/>)}
          </div>
      )
      
      const Slide = slide => (
          <div>
              <h1>{slide.title}</h1>
              <ul>
                  {slide.bullets.map(bullet=><li>{bullet}</li>)}
              </ul>
          </div>
      )
      
    ```
    In above code we have components Slide which will be iterated 2 time as slide have two slides but if there is more slid then we'll just add slide title and bullets to the array of slide and nothing else while in HTML we will have to write another div and all the stuffs.

## React is Performant
  - We write what we want and React will do the hard work
  - Reconciliation - the process by which React syncs changes in app state to the DOM
    - Reconstructs the virtual DOM
    - Diffs the virtual DOM against the DOM
    - Only makes the changes needed

## Writin React
  - JSX
    - XML-like syntax extension of JavaScript
    - Transpiles to JavaScript
    - Lowercase tags are treated as HTML/SVG tags, uppercase are treated as custom components
  - Components are just functions
    - Returns a node(something React can render, e.g. a <div />)
    - Receives an object of the properties that are passes to the element
      ```
        const Slide = slide => (
            <div>
                <h1>{slide.title}</h1>
                <ul>
                    {slide.bullets.map(bullet=><li>{bullet}</li>)}
                </ul>
            </div>
        )
      ```
      `Slide` is a component i.e. function that returns a node `<div>` and receives an object `slide`.

## Props
  - Passes as an object to a component and used to compute ther returned node
  - Changes in these props will cause a recomputation of the returned node ("render")
  - Unlike in HTML, these can be an JS value
    ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/4b31db42-952e-4b67-b1aa-ac1252427eac) <br/>
    In above exapmle we can see `count` is passed to component as props


## State
  - Adds internally-manages configuration for a component
  - `this.state` is a class property on the component instance
  - Can only be updated by invoking `this.setState()`
    - Implemented in React.Component
    - `setState()` calls are batched and run asynchronously
    - Pass an object to be merged, or a function of previos state
  - Changes in state also cause re-renders
    ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/de0f04c4-593d-43bb-b6d7-0c1070e463f0) <br/>
    ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/bd1631fb-f3d9-4eab-ada9-6ada7e9a439e) <br/>
    In above two screenshots we can see there is bug at `this.setState({count: this.state.count + 1});` as `this` is not bounded so it is undefined at the time of execution. <br/>
    We can remove this bug by two methods
    1. Using `bind()` method:
       ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/f35d58cc-c0cb-4dc8-a380-f5f41aec4f8e)
    2. Using Arrow notation:
       ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/e1e5bfe3-1463-43aa-9f9d-2d0a9d43b541) <br/>
       In above Example `this` will bind to the class where `render` method is.
    3. We can define it in constructor too
  - What if we want to increase two at a time? We will try to modifying `increaseCount` function to setState twice
    ```
      increaseCount() {
          this.setState({ count: this.state.count + 1 });
          this.setState({ count: this.state.count + 1 });
        }
    ```
    We will see it is resulting the count to increase one at a time not two<br/>
    This is because `setState` calls are batched and run asynchronously.
    Let's see consoling the value What we get
    ```
      increaseCount() {
          this.setState({ count: this.state.count + 1 });
          this.setState({ count: this.state.count + 1 });
          console.log(this.state.count);
        }
    ```
    ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative-Notes/assets/60311459/ab48d821-da09-4e21-9cf5-23a4f63b23c3) <br/>
    On clicking once `console.log()` returned 0 i.e. previous value as `setState()` was batched. and bothe `setState()` added value to 0.
    > What if we want to make it 2 not 1 in first click so we can use arrow notation to make this change happen using previuos state and it will return the an object.
    ```
      increaseCount() {
          this.setState((prevState) => ({ count: prevState.count + 1 }));
          this.setState((prevState) => ({ count: prevState.count + 1 }));
          console.log(this.state.count);
        }
    ```
    Above code will result the count to be 2 after clicking.


  #### React Todo App which will shown todos with check and uncheck and delete function at top it will show count no of todos and unchecked todos:
  Here we have used props, states, Components(function and class) etc.
  ```
    import "./styles.css";
    import React from "react";
    
    let id = 0;
    
    const Todo = (props) => (
      <li>
        <input
          type="checkbox"
          checked={props.todo.checked}
          onChange={props.onToggle}
        />
        <button onClick={props.onDelete}>Delete</button>
        <span>{props.todo.text}</span>
      </li>
    );
    
    export default class App extends React.Component {
      constructor() {
        super();
        this.state = {
          todos: [],
        };
      }
      addTodo() {
        const text = prompt("Add Todo text");
        this.setState({
          todos: [...this.state.todos, { id: id++, text: text, checked: false }],
        });
      }
    
      toggleTodo(id) {
        this.setState({
          todos: this.state.todos.map((todo) => {
            if (todo.id === id) {
              return { id: todo.id, text: todo.text, checked: !todo.checked };
            }
            return todo;
          }),
        });
      }
    
      removeTodo(id) {
        this.setState({
          todos: this.state.todos.filter((todo) => todo.id != id),
        });
      }
      render() {
        return (
          <div className="App">
            <div>Todos Count: {this.state.todos.length}</div>
            <div>
              Unchecked Todos Count:{" "}
              {this.state.todos.filter((todo) => !todo.checked).length}
            </div>
            <button onClick={() => this.addTodo()}>Add Todo</button>
            <ul>
              {this.state.todos.map((todo) => (
                <Todo
                  onToggle={() => this.toggleTodo(todo.id)}
                  onDelete={() => this.removeTodo(todo.id)}
                  todo={todo}
                />
              ))}
            </ul>
          </div>
        );
      }
    }

  ```
  - `<Todo/>` component will return list item with checkbox, button and todo text having props object with functions and data
  - Class `App` has functions `addTodo()`, `removeTodo()` and `toggleTofo()` and renderd `div` containing two other `divs` showing todo counts, button to add new todo whick will call `addTodo()` on click and unordered list having Todos mapped and each todo is passed as props to `<Todo/>` and functions to toggle and delete too.


> But why limit React to just web?

## React Native
  - A framework that relies on React core
  - Allows us build mobile apps usinf only JavaScript
    - "Learn once, write anywhere"
  - Supports iOS and Android
