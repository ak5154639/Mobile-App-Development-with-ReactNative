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
