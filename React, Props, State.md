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
