---
creation date: 2023-01-19 21:29
modification date: Thursday, 19th January 2023, 21:29:13
tags: today_i_leaned, engineering/functional-programming/debugging
---

# How to use print to debug functional pipeline


When trying to debug a piped functional function, let's say:
```javascript

const add1 = x => x + 1;  
const multiplyBy2 = x => x * 2;

const add1AndMultiplyBy2 = R.pipe(  
  add1,  
  multiplyBy2,  
);

add1AndMultiplyBy2('1'); // returns 22
```

I would normally have break the pipeline into a sequential function where I can put a console.log in the middle:

```javascript
function add1AndMultiplyBy2 (num) {  
  const plus1 = add1(num);  
  console.log(plus1); // logs '11'  
  const plus1Times2 = multiplyBy2(plus1);  return plus1Times2;  
}
```

This is a real PITA.

There is however a more 'functional' way to inject log output in a functional pipeline.  Ramda provides a function called `[tap](https://ramdajs.com/docs/#tap)` which runs a given function with a supplied value, then returns the value, unchanged.  This is like the *identity* function with the ability to perform some side effect.

```javascript
const add1AndMultiplyBy2 = R.pipe(  
  add1,  
  R.tap(x => console.log('WTF', x)), // logs 'WTF' and '11'  
  multiplyBy2,  
);

add1AndMultiplyBy2('1'); // returns 22
```

We can also create a new lamda that cleans things up a little bit:

```javascript
const log = msg => R.tap(x => console.log(msg, x));
```

We then end up with:

```javascript
const add1AndMultiplyBy2 = R.pipe(  
  add1,  
  log('value after add1: '), // logs "value after add1: 11"  
  multiplyBy2,  
);

add1AndMultiplyBy2('1');
```


---
#### references
[how to debug point free code using ramda](https://itnext.io/how-to-debug-your-point-free-code-with-ramda-5c46bd743781)