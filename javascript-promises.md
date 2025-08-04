# Understanding Promises in JavaScript

``` jsx
function getRandomInt(max){
    return Math.floor(Math.random() * max);
}

function PromiseWithLoop(){
    return new Promise(function execution(resolve, reject){
        setTimeout(() => {
            let num = getRandomInt(10);
            if (num % 2 == 0){
                resolve(num);
            } else {
                reject(num);
            } 
        }, 2000);
    });
}

let x = PromiseWithLoop();
console.log(x);

x.then(
    function fulfillment(value){ console.log("fulfilled", x); }, 
    function rejection(value){ console.log("rejected", x); }
);
```

## Explanation

-   The `.then()` function allows you to schedule tasks to execute in
    the future based on a promise's state.\
-   It takes **two parameters**:
    `(fulfillmentHandler, rejectionHandler)`.\
-   You can assign any function to be executed when the promise is
    **fulfilled**.\
-   Similarly, you can assign any function to be executed when the
    promise is **rejected**.

### Key Points

-   A *placeholder* reserves a space in memory.\
-   When the promise is done (via resolve or reject), the function
    you assigned will move to the *microtask queue*.\
-   If the promise is *rejected*, the rejection handler function will
    be moved to the *microtask queue*.\
-   The .then() function *returns a new promise* in itself.
