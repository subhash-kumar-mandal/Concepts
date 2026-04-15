# Closure

## what is Closures?

A closures is a function that remembers  variable from its outer scope .
even after the outer function has finished  execution .


## Example
```js
 function outer(){
    let count =0;
    
    return function (){
        count++;
        console.log(count)
    }
 }
```

```js
const fn = outer();
fn() // 1
fn() // 2
```


## Key Points 

- Closure store reference , not copy 
- Used for data privacy 
- Used in memoization and React hooks

## Real Use Caces
