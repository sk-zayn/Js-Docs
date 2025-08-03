# JavaScript: Sync, Async, Event Loop & Promises

JavaScript is **synchronous** in nature and **single-threaded**, but only for native code (things that are present in **ECMAScript docs**).

---

## CallStack
- A mechanism that keeps track of functions in the call stack.
- Works on **LIFO (Last In First Out)**.

---

## Event Queue / Callback Queue
- Keeps the functions that are completed by the runtime.

---

## Event Loop
- Continuously checks whether the **CallStack** is empty and whether the global code is finished.
- If empty, then only the functions inside the **EventQueue** will be executed.

---

### Example 1
```jsx
console.log("Hello World");
setTimeout(function exec(){
    console.log("Timer Done");
}, 0);
console.log("Bye");
```
output will be:

    Hello World  — it will print normal 
    Bye — It will print before timer done




Timer Done — as setTimeout is not Ecmascript function it will be sent to Runtime to process. it will process for how much time it has been given and then store the function in EventQueue. When all the CallStacks and global code is done then only the EventQueue functions will get printed.[ Thats why even tho it is before Bye in coding it will print after Bye as console.log is global code ]

```js
console.log("Hello World");
setTimeout(function exec(){
    console.log("Timer Done");
},0);
for(i=0; i <1000000000; i++){
    
}
console.log("Bye");
```
```jsx
console.log("Hello World");
for(let i= 0; i < 3; i++){
    setTimeout(function exec(){
    console.log("Timer Done");
},0);
}
for(i=0; i <1000000000; i++){  
}
console.log("Bye");
```

Set Interval — It will execute the code again and again with given interval unless we stop it.

```jsx
setInterval(function setIntervalDemo(){
    console.log("hi");
}, 1000);
```
It will print “hi” again and again with the interval of 1sec until we stop it.

Inversion Of Control — Here function fun is HOF. 

fn is a call back function.

fn is totally depended on fun.

we don’t know in function fun, fn is getting called or not or how many times it is getting called.

```js
function fun(x, fn){
    for(let i = 0; i < x ; i++){
        console.log(i);
        // return i;
    }
    fn();
}
fun(10, function ecept(){
    console.log("i am executed here");
})
```
Promises — Code readability enhancer, its a special type of object that gets returns immediately when we call it.
    
Its works as a placeholder for the data which we will use in future.
    
There are Three State in Promise:
1. Pending :-Its a default state. When we create a new promise object it is in default state.
2. Fulfilled :- if operation is successful it will go in a fulfilled state.
3. Rejected :- if operation failed it will go in a rejected state.

To create a Promise Object :

new Promise( function ( resolve, reject ){………. } );

- `new` is a **keyword** used to create a new **Promise object**.
- The function you pass inside `new Promise(...)` is called the **executor function**.
    
    👉 It runs **immediately** and **synchronously** when the promise is created.
    
- Inside that function, JavaScript gives you two functions:
    - `resolve()` → to mark the promise as **successful** (fulfilled).
    - `reject()` → to mark the promise as **failed** (rejected).
- You can pass values to `resolve()` or `reject()`:
    - These values are received later in `.then()` or `.catch()`.
- If you **don’t call** `resolve()` or `reject()`, the promise stays in the **pending state forever**.

---

### **Extra Point (Very Important):**

- When you use `.then()` or `.catch()` on a promise, those callbacks go into the **microtask queue**.
- Microtasks are run **after the current code (call stack)** finishes, and **before any setTimeout or other macrotasks**.

```jsx
function getRandomInt(max){
    return Math.floor(Math.random() * max);
}
function PromiseWithLoop(){
    return new Promise(function execution(resolve, reject){
        for (let i = 0; i < 5000000000; i++){}
        let num = getRandomInt(10);
        if (num % 2 == 0){
            resolve(num);
        }else{
            reject(num);
        } 
    });
}
let x = PromiseWithLoop();
console.log(x);
```

```jsx
function getRandomInt(max){
    return Math.floor(Math.random() * max);
}
function PromiseWithLoop(){
    return new Promise(function execution(resolve, reject){
        setTimeout(() => {
            let num = getRandomInt(10);
        if (num % 2 == 0){
            resolve(num);
        }else{
            reject(num);
        } 
        }, 10000);
        
    });
}
let x = PromiseWithLoop();
console.log(x);
console.log("Highlight");
```
This code will get started, it will go to setTimeout and take however much time it has been set to, but it will not stop ECMAScript from printing Highlight. 

That means promise [ pending ] will be printed first, and then Highlight, and when the timer finishes, it will replace [ pending ] with the value.

Once you have updated the state of the promise, you cannot update it again.