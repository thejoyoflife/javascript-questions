### Miscellaneous
- typeof checking. Output?
```javascript
typeof 0;
typeof +0;
typeof -0;
typeof Math.sqrt(2);
typeof Infinity;
typeof NaN; 
typeof Number('100');
typeof Number('freeCodeCamp'); 

typeof true;
typeof false;
typeof Boolean(0);

typeof 12n;

typeof '';
typeof 'freeCodeCamp';
typeof `freeCodeCamp is awesome`;
typeof '100';
typeof String(100);

typeof Symbol();
typeof Symbol('freeCodeCamp');

typeof {blog: 'freeCodeCamp', author: 'Tapas A'};
typeof ['This', 'is', 101];
typeof new Date();
typeof Array(4);

typeof new Boolean(true); 
typeof new Number(101);
typeof new String('freeCodeCamp');
typeof new Object;

typeof alert;
typeof function () {};
typeof (() => {});
typeof Math.sqrt;

let a;
typeof a;
typeof b;
typeof undefined;

typeof null;

isNaN(0/0);
isNaN(undefined);
Number.isNaN(undefined);
```
```javascript
const arr = [2, 5, 9, 2];
console.log(arr.indexOf(9, -1)); // -1
console.log(arr.indexOf(5, -3)); // 1
console.log(arr.lastIndexOf(2, 2)); // 0
console.log(arr.lastIndexOf(2, -1)); // 3
console.log(arr.fill(0, 1, 3)); // [2, 0, 0, 2]
```
- Write a utility function that can check types correctly and can differentiate between arrays and built-in objects (Date, Map, Set, WeakMap)?
```javascript
function typeCheck(value) {
  const return_value = {}.toString.call(value); // Object.prototype.toString would also work
  const type = return_value.substring(
           return_value.indexOf(" ") + 1, 
           return_value.indexOf("]"));

  return type.toLowerCase();
}

typeCheck([]); // 'array'
typeCheck(new Date()); // 'date'
typeCheck(new String('freeCodeCamp')); // 'string'
typeCheck(new Boolean(true)); // 'boolean'
typeCheck(null); // 'null'
typeCheck(undefined); // 'undefined'
```
- `this` binding, and difference between `call`, `apply` and `bind` functions?
```javascript
// 1. Output?
const user = {
  name: 'Tyler',
  age: 27,
  languages: ['JavaScript', 'Ruby', 'Python'],
  greet() {
    const hello = `Hello, my name is ${this.name} and I know`

    const langs = this.languages.reduce(function (str, lang, i) {
      if (i === this.languages.length - 1) {
        return `${str} and ${lang}.`
      }

      return `${str} ${lang},`
    }, "")

    alert(hello + langs)
  }
}
user.greet();

// 2. Output?
'use strict' // with or without...
window.age = 27;
function sayAge () {
  console.log(`My age is ${this.age}`)
}
sayAge();
```
- Difference between slice and splice?
- Explain all the 3 parameters of JSON.stringify.
```javascript
const a = {
  name: "Shimul",
  age: 45,
  married: true,
  daughters: ["Shriya", "Ridhi"],
  numOfSons: null,
  symb: Symbol("test"),
  greet() {
    return "Hi, Shimul";
  },
  set: new Set([1, 2, 3]),
  map: new Map([[1, "one"], [2, "two"]])
};

function replace(key, val) {
  if (typeof val === 'symbol') {
    return val.toString();
  }
  if (val instanceof Set) {
    return Array.from(val);
  }
  if (val instanceof Map) {
    return Array.from(val.entries())
  }
  if (typeof val === 'function') {
    return val.toString();
  }
  return val;
}

console.log(JSON.stringify(a));
console.log(JSON.stringify(a, null, 4));
console.log(JSON.stringify(a, replace, 4));
```
- Output?
```javascript
const a = {name: "shimul", office: "SIL", addr: "Banani"};
const b = {age: 40, addr: {vill: "Modhubari", upazilla: "Lalpur"}};
const res = Object.assign(a, b);
b.addr.vill = "Bahadipur";
console.log(res === a);
console.log(res);
```
- Difference between `Object.create` and `new` (hint: `new <Function>` actually runs constructor code, whereas `Object.create` will not execute the constructor code).
```javascript
function Dog(){
    this.pupper = 'Pupper';
};

Dog.prototype.pupperino = 'Pups.';
var maddie = new Dog();
var buddy = Object.create(Dog.prototype);

//Using Object.create()
console.log(buddy.pupper); //Output is undefined
console.log(buddy.pupperino); //Output is Pups.

//Using New Keyword
console.log(maddie.pupper); //Output is Pupper
console.log(maddie.pupperino); //Output is Pups.
```
- Difference between `Object.keys` and `for-in` loop? What are the internal attributes of an object's property? - *writable*, *configurable*, *enumerable* and *value*.
```javascript
const a = {name: "shimul", office: "SIL", addr: "Banani"};
const t = Object.create(a);
t.age = 40;

for (const key of Object.keys(t)) {
  console.log(key);
}

console.log("-------------");

for (const key in t) {
  console.log(key);
}

```
- How to conditionally extend an object with addtional property and an array with addtional values?
```javascript
const a = {name: "Shimul", addr: "Banani"};
const addAge = false;

const mA = {
  ...a,
  ... (addAge && {age: 40})
}

console.log(mA)

const arr = ["Shimul", "Sohel"];
const addNoor = true;

const mArr = [
  ...arr,
  ...(addNoor ? ["Noor"] : []) // (addNoor && ["Noor"]) does't work
];

console.log(mArr);
```
### Promises
- Difference between `Promise.all`, `Promise.allSettled`, `Promise.race` and `Promise.any`. What is the structure of the settled message of `Promise.allSettled`, and error message of `Promise.any` when all the constituent promises get rejected.
```javascript
// 1. Output?
const p1 = new Promise((res, rej) => {
  setTimeout(() => rej(1), 2000);
});
const p2 = new Promise((res, rej) => {
  setTimeout(() => res(2), 3000);
});
const p3 = 3;

const p = Promise.allSettled([p1, p2, p3]);

p.then(res => console.log(res))
  .catch(err => console.error(err));

// 2. Output?
const p1 = new Promise((res, rej) => {
  setTimeout(() => rej(1), 2000);
});
const p2 = new Promise((res, rej) => {
  setTimeout(() => rej(2), 3000);
});

const p = Promise.any([p1, p2]);

p.then(res => console.log(res))
  .catch(err => console.error(err)); // the structure of the err???  
```
- Output?
```javascript
console.log('start')

const fn = () => (new Promise((resolve, reject) => {
  console.log(1);
  resolve('success')
}))

console.log('middle')

fn().then(res => {
  console.log(res)
})

console.log('end')
```
```javascript
console.log('start')

Promise.resolve(1).then((res) => {
  console.log(res)
})

Promise.resolve(2).then((res) => {
  console.log(res)
})

console.log('end')
```
```javascript
console.log('start')

setTimeout(() => {
  console.log('setTimeout')
})

Promise.resolve().then(() => {
  console.log('resolve')
})

console.log('end');
```
```javascript
console.log('start');

const promise1 = Promise.resolve().then(() => {
  console.log('promise1');
  const timer2 = setTimeout(() => {
    console.log('timer2')
  }, 0)
});

const timer1 = setTimeout(() => {
  console.log('timer1')
  const promise2 = Promise.resolve().then(() => {
    console.log('promise2')
  })
}, 0)

console.log('end');
```
- Output?
```javascript
const promiseA = new Promise( ( resolve, reject ) => {
  setTimeout( () => {
      i++;
      resolve( i );
  }, 1000 ); // resolve after 1 second
} );

promiseA
.then( ( result ) => {
  console.log( 'promiseA success:', result );
} )
.catch( ( error ) => {
  console.log( 'promiseA error:', error );
} )
.finally( () => {
  console.log('a() is done!');
} );
```
```javascript
Promise.reject( 'Reject DATA!' )
.then( ( result ) => {
    console.log( '[1] then', result ); // won't be called
    return '[2] then payload';
} )
.finally( ( ) => {
    console.log( '[1] finally' ); // first finally will be called
    return '[1] finally payload';
} )
.then( ( result ) => {
    console.log( '[2] then', result ); // won't be called
    return '[2] then payload';
} )
.catch( ( error ) => {
    console.log( '[1] catch', error );  // first catch will be called
    return '[1] catch payload';
} )
.catch( ( error ) => {
    console.log( '[2] catch', error );  // won't be called
    return '[2] catch payload';
} )
.then( ( result ) => {
    console.log( '[3] then', result ); // will be called
    return '[3] then payload';
} )
.finally( () => {
    console.log( '[2] finally' ); // will be called
    return '[2] finally payload';
} )
.catch( ( error ) => {
    console.log( '[3] catch', error );  // won't be called
    return '[3] catch payload';
} )
.then( ( result ) => {
    console.log( '[4] then', result ); // will be called
    return '[4] then payload';
} );
```
