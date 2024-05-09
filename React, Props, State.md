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

## Props
  - Passes as an object to a component and used to compute ther returned node
  - Changes in these props will cause a recomputation of the returned node ("render")
  - Unlike in HTML, these can be an JS value

## State
  - Adds internally-manages configuration for a component
  - `this.state` is a class property on the component instance
  - Can only be updated by invoking `this.setState()`
    - Implemented in React.Component
    - `setState()` calls are batched and run asynchronously
    - Pass an object to be merged, or a function of previos state
  - Changes in state also cause re-renders

> But why limit React to just web?

## React Native
  - A framework that relies on React core
  - Allows us build mobile apps usinf only JavaScript
    - "Learn once, write anywhere"
  - Supports iOS and Android
