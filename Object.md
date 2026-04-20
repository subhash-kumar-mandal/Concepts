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




