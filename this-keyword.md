# This Keyword 

## Rule 
this depends on the how the  function is is called.

# Cases 

## Global 
 this --> window 


 ```js
console.log(this) // window / undefined(strict mode);
 ```

## Regular Function  and Arrow function
this ---> window / undefined (strict) ;

```js
function Call(){
    console.log(this);
};

//  window / undefined (strick mode );


const Arrow = ()=>{
    console.log(this) // 
};
// window / undefined (not own this, inherit parent function) 
```

## Object Method 
This ---> object 

```js

const obj = {
    Age:20,
    Get(){
        console.log(this.Age);
    },
    Get2:()=>{
        console.log(this.Age);
    }
};


obj.Get() // 20;
obj.Get2() // undefined
  
```


## Evnt handler

```js 
Button.addEventListener("click",function()=>{
    console.log(this)  // button Element
})

Button.addEventListener("click",()=>{
    console.log(this)  // window object
})


```

## Constructor Function 

```js 
function User(name){
    this.name = name ;
}

const  u1 = new User("Aman");

console.log(u1.name) // Aman

// this ---> new object ko point karta hai 

```


## Explicit Binding

```js
const User = {
    name:"Aman",
    Age:26,
};

function Info(city,lastname){
        console.log(this.name,lastname,"Your age is ",this.Age,"from",city)
}


Info.call(User,"Delhi","Kumar")// call this ko bind karo User object ke sath or call karo 
//Output --->  Aman Kumar Your age is  26 from Delhi


Info.apply(User,['Delhi','kumar']) //  apply this ko bind karo User ke sath same hai call ki tara bass array mein aggrement jaate hai 
// output --->  Aman Kumar Your age is  26 from Delhi


const fn = Info.bind(User);
fn("Delhi",'kumar');
// bind this ko User ke sath bind karo or ek new function return karta hai 
// output ----> Aman Kumar Your age is  26 from Delhi


```


 # Question


```js 
const object ={
    name:"JS",
    say(){
        setTimeout(()=>{
            console.log(this.name)
        },0)
    }
}

 ```


 ```js

object.say(); // undefined 

// say function object ne call liya but phele sync code run hua or settimeout memory mein register ho gya sync code mein ke bad event loop ne esko callback queues se utha or call stack execute ke liye diya or es time standalone kyuki callbackmke sath koi bind nhi hai object kaa
 ```