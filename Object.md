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
internally: constructor function 


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

#

# Deep  understanding

```js

// ----> Prototype concept
   
  ## Object.create prototype se karo pass kiye huye object se 
    (prototype chaining)

   const parent ={
     Class:'8th',
     Section:"A"
   };

   const student_A = Object.create(parent);
   student_A.name ="Aman kumar";

   console.log(student_A.name)  //  "Aman"
   console.log(student_A.Class) //  "8th"
   console.log(student_A.Section) // "A"



//  Factory function and Constructor  one problem every new create  object not sharing method. every create object un-neccessry memory space fill



 function  Car(name,modal){
    return {
        name,
        modal,
        Get(){
            console.log(this.name)    // create every time new object 
        }
    }
 };


 const car1 = Car('Toyota',"S1"); // { name: 'toyota', modal: 'S1', Get: [Function: Get] }

 const car2 = Car("toyota","S2") // { name: 'toyota', modal: 'S2', Get: [Function: Get] }




 function Vehicle(name,type)
{
    this.name = name;
    this.type = type;
    this.state = function(){
        console.log(this.name) // Cretae Every time;   
    }

};

const vehicle_1 = new Vehicle('Bike',"Two wheeler");
//     Vehical {
//          name: 'Bike',
//          type: 'Two wheeler',
//          state: [Function (anonymous)] ----> Create here function
//              }



const vehicle_2 = new Vehicle("Car","four wheeler ")
//     Vehical {
//          name: 'Car',
//          type: 'four wheeler',
//          state: [Function (anonymous)] ----> Create here function
//              }



//  Solution



 function Vehicle(name,type)
{
    this.name = name;
    this.type = type;
 
};

Vehicle.prototype.vehicleType = function(){ // -------> ab ye function prototype mein ab ye haar bar new create nhi hoga  memory share hoga (store in prototype)
    console.log(this.type)
};  




const vehicle_1 = new Vehicle('Bike',"Two wheeler");
//     Vehical {
//          name: 'Bike',
//          type: 'Two wheeler'
//              }



const vehicle_2 = new Vehicle("Car","four wheeler ")
//     Vehical {
//          name: 'Car',
//          type: 'four wheeler'
//              }
 




 // factory dunction  
//  1. memory duplication 
//  2. prototype not use 
//  3. Factory function can use this but usually aviods it . It returns object  directly ,so "this " confusion nhi hota 


//  constructor function  
// 1. Methods can be shared via prototype 
// 2. memory efficient 
// 3. supports inhertance 

```



# Destructuring 

```js
const user ={
    name:"aman",
    active:false,
    age:20,
    city:'delhi'
} ;


const {name,age} = user
// output  aman 20 
```


# 

# Rest Operator (collect)
-      When used in a function's parameter list, it catches any extra arguments passed to the function and packs them neatly into an array
```js

function abc(a,...b){
    return b;
};

console.log(abc(1,2,3,4,5,5))// [1,2,3,4,5,5];




syntax Error 

function  Wrong1(...one,...wrong){}  ❌
function  Wrong2(...one,a,b){}   ❌
function Wrong3(...restParams,){} ❌
function Wrong4(...rest=10){}    ❌


// 1. Rest parameter must be last formal parameter
// 2. Rest parameter may not have a default initializer


```
#

# Spread Operator (Expand)
-      The spread (...) syntax allows an iterable, such as an array or string, to be expanded in places where zero or more arguments (for function calls) or elements (for array literals) are expected
```js
 const array = [1,2,3,4,5];

 const copy_array = [...array] // [1,2,3,4,5]



 const object ={
    name:"aman",
    class:"8th"
 };

 const copy_student = {...object};
 //{
 //   name:"aman",
 //   class:"8th"
 // }



 const a ={x:10};
 const b= {y:12};

 const Copy = {...a,...b};
 // { a:10,b:12}

```

# Tricky Part

```js
// Destructuring Deflault value;
// only undefined par run
const {x=10} = {};



// Rename 

const {a:value} = {a:5};
console.log(a)// undefined;
console.log(value) // 5



// Nested Destructuring 
const {a:{b}} = {a:{b:10}};
console.log(b) // 10


//  Lost this context

let object = {
    name:"js",
    say(){
        console.log(this.name);
    }
};


const {say} = object;
say()// undefined






//  Spread Big trap shallow copy

const obj1=  {
    a:10,
    b:{c:100}
};

const obj2 = {...obj2};
obj2.b.c =500;

console.log(obj1.b.c)// 500
```



#
# Object Propety Internals 

-      Every Property have four hidden info
    
      1. value --> The actual data stored in the property.
      2. writable -->  If true, the property's value can be changed; if false, it is read-only
      3. enumerable    -> If true, the property appears during loops  and in Object.keys() else not appears.
      4. configurable  ->  If true the property can be delete and  else false can be  not delete .


```js
const Car ={
    name:"toyota",
    modal:"S1",
    
};


console.log(Object.getOwnPropertyDescriptors(Car))
// see the hidden Info any keys

// {
//   name: {
//  value: 'toyota',
//  writable: true,
//  enumerable: true,
//  configurable: true 
// },

//   modal: {
//  value: 'S1',
//  writable: true,
//  enumerable: true,
//  configurable: true }
// }


// Custom property set 

Object.defineProperty(Car,'name',{
    value:"toyota 2.0", // set the value new 
    writable:false  // not change the value kabi bad mein
});


Car.name = 'hello' // ❌ yaha ab ye kaam nhi karega  kyuki writable :false hai
console.log(Car.name) // toyota 2.0


// hide any loop and console.log();

Object.defineProperty(Car,'modal',{
    enumerable:false  // false value hide the any loop and console
});



console.log(Car) // {name:"toyota 2.0"}


Object.defineProperty(Car,"secret",{
    value:"hidden",
    enumerable:false;
})






for(let key in Car){
    console.log(key)
}

// loop only print name

console.log(Object.keys(Car)) // ["name"]
console.log(Car.secret) // hidden




//  Use Case:
 1. Hidden Proertys (Security/ clean data)
 2. read only config
 3. library / Framework
 4. Controlled APIs
 5. Performance + clean loops

```
# 
# Shallow , Deep , Structured Clone

-     Shallow Copy
      1. Independent copy the top level (like nested Object or array pass the reference)
      2. Circuler Refs  N/A
      3. map/set/Dates --> Shared reference




-     Deep Copy
      1. Copy the deep copy (safe Nested object and array)
      2. Loss the propertys function , undefined , data---> String  
      3. Circuler flow throw error
      4. map/set/Dates --> converts to string / empty   


-     Structured Clone
      1. Fully Indepenedent
      2. Nested fully clone
      3. Ciruler flow  ---> Handled Corrently
      4. function --- > throw error      


```js

// Shallow copy trap

const obj = {
    a:1,
    b:{c:2}
};

const obj2 = {...obj}
obj2.b.c = 100;
console.log(obj.b.c) // 100

// b --> reference copy hua
// nested object share


//  Deep clone

const obj = {
    a:undefined,
    fn:()=>{},
    data:new Date()
};

console.log(JSON.stringify(obj)) // {"data":"2026-04-23T08:10:28.055Z"}



// StructuredClone
const obj = {
    fn:()=>{}
};


console.log(structuredClone(obj))
// DOMException [DataCloneError]: ()=>{} could not be cloned.

```