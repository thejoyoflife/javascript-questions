### Miscellaneous
- Output?
```javascript
const a = {name: "shimul", office: "SIL", addr: "Banani"};
const b = {age: 40, addr: {vill: "Modhubari", upazilla: "Lalpur"}};
const res = Object.assign(a, b);
b.addr.vill = "Bahadipur";
console.log(res);
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
