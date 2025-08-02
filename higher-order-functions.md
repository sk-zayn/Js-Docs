# IIFE — Immediately Invoked Function Expression

An IIFE is a function that runs as soon as it is defined.

---

# Higher Order Functions (HOF)

Functions that **take another function as an argument** or **return a function** are called **Higher Order Functions**. They rely on or work with other functions.

---

## 🔹 `map()` Function

- `map()` is a HOF available on arrays.
- It:
  - Takes a function as an argument.
  - Returns a **new array**.
  - Does **not mutate** the original array.

```js
// Example: Squaring each element
function square(f) {
  return f * f;
}
let arr = [1, 2, 3, 4, 5];
let result = arr.map(square);
console.log(result);

// Example: Even or Odd
function isEvenOrOdd(x) {
  return x % 2 === 0 ? "Even" : "Odd";
}
let isevenorodd = arr.map(isEvenOrOdd);
console.log(isevenorodd);
```

The callback function receives:

First argument: the current element.

Second argument: the index of the element.

```js
const newArr = [9, 8, 7, 6, 5];

function print(element, indx) {
  return `Element at index ${indx} is ${element}`;
}

const result = newArr.map(print);
console.log(result);
```

## 🔹 `customMapper()` — Custom Implementation of `map()`

```js
const newArr = [9, 8, 7, 6, 5];

function print(element, idx) {
  return `Element at index ${idx} is ${element}`;
}

function customMapper(arr, func) {
  let result = [];
  for (let i = 0; i < arr.length; i++) {
    result.push(func(arr[i], i));
  }
  return result;
}

const value = customMapper(newArr, print);
console.log(value);
```

###  Sort function
sort function do lexico graphical scoping by default. lexico graphical scoping means the way you sort words in dictionary.  
    
This is lexico scoping…………
```js
let a = [1, 3, 110, 14, 2, 87, 96,34,75, 75, 45, 34, 1100];
a.sort();
console.log(a);
```
To avoid this use we can use function in sort method.  as sort method is HOF, which will then print the value in increasing order.

```js
 let a = [1, 3, 110, 14, 2, 87, 96,34,75, 75, 45, 34, 1100];
 //if a < b --> a-b will be negative --> if cmp function gives negative then a is placed before b (a<b)
 //if a > b --> a-b will be positive --> if cmp function gives positive then a is placed after b (a>b)
 a.sort cmp(function(a,b){
     return a-b;
 })
 console.log(a);
 ```

## Filter function
    
Filter function is also a HOF.
    
Filter also loops over the array element. There is one special thing about the filter i.e., the argument function ( f ), which we have to pass inside the filter, should always return a boolean; otherwise output will be converted to a boolean.

```js
let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
function oddOrEven(x){
    return (x %2 == 0);
}
const result = arr.filter(oddOrEven)
console.log(result);
```

## Reduce function
    
Reduce is a higher-order function available for arrays, Reduce also takes a function f as an argument, it takes two arguments and first will be the previous, and second will be current. It adds the previous and current together which will then become previous and the current value will be updated.
    
 ```js
    const arr = [1, 2, 3, 4, 5, 6];
    function sum (previousResult, currValue){
        return previousResult + currValue;
    }
    //previous value 1 + current value 2 = 3
    //previous value 3 + current value 3 = 6
    //previous value 6 + current value 4 = 10
    //previous value 10 + current value 5 = 15
    //previous value 15 + current value 6 = 21 
    
    //output will be = 21 
    const result = arr.reduce(sum);
    console.log(result);
```

## Callback function
    
The function that you pass in the HOF are callback funcions.
    
```js
function fun(x, fn){
    for(let i = 0; i < x ; i++){
        console.log(i);
        // return i;
    }
    fn();
}
fun(10, function ecept(){    //this is callback function
       console.log("i am executed here");
})
```