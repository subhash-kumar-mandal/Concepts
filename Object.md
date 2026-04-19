# Object

## what is Object?
- object is a standalone data structure that stores related data and functionality as a collection of properties (key-value pairs);


-      Properties : A Property is an association between a name (key) and value 
-      Methods    : When a property  value is a function ,it is called a method.
-      this       : Inside an object method ,this refers to the  "owner" of the method -- the object itself And This depends on how the function is called .



#

## Ways  to Create  Object

-     1. Object Literal (The most common way, using curly braces {})

```js
const car ={
    make :"Toyota",
    year :2024,
    start(){
        console.log("Start Toyota");
    }
}
```
#

-     2. Constructor Function (this → new object)


```js
function User(name,age){
    this.name = name;
    this.age  = age;
}

const u1 = new User("subhash",20) 

console.log(u1.name) // subhash ;
console.log(u1.age)  // 20
```
#

-     3. Object.create (Prototype (child → parent से inherit करता है) )


```js
const obj = {
    name :"Dog",
    start(){
        console.log(this.name)
    }
} 

const cat = Object.create(obj);
cat.name ="cat"

console.log(cat.name) // cat ;  (cat object own the name)
cat.start()  // cat    ( start method inherit kiya gya hai  obj (parent) se )
```
#

-     4. Class ( Modern syntax ) 
internally: constructor function ही है


```js
class User {
    constructor(name,age){
        this.name = name;
        this.age  = age;
    }
};

const user1 = new User("subhash",24);
  
```

#
-     5. Factory function (closure + object)


```js
const obj = {
    return {
    name :"Dog",
    start(){
        console.log(this.name)
    }
    };
} 

const cat = Object.create(obj);
cat.name ="cat"

console.log(cat.name) // cat ;
u1.start()  // cat
```




