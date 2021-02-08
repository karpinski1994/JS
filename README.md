# JS
Some helpful tips, tricks, good practices and ready-made solutions in Javascript / Typescript

# List of javascript useful practical tricks and patterns
---
&nbsp;
## Arrays
### Reduce
&nbsp;
##### Sum values of an array
&nbsp;
```
const numbers = [29.76, 41.85, 46.5];

const sum = numbers.reduce((total, amount) => total + amount);

sum // 118.11
```
&nbsp;
##### Count the average of array
&nbsp;
```
const numbers = [29.76, 41.85, 46.5];

const average = (array) => array.reduce((a, b) => a + b) / array.length;

const avg = average(numbers)
avg // 39.37

```
&nbsp;
##### Find min and max in array
&nbsp;
```
const nums = [1, 2, 3, 4, 5, 6, 7, 8];

const [min, max] = nums.reduce(
  (acc, cur) => [Math.min(acc[0], cur), Math.max(acc[1], cur)],
  [Infinity, 0]
);

// min: 1
// max: 8
```
&nbsp;
&nbsp;
##### Sum even and odd numbers in one go
&nbsp;
```
const numbers = [1, 2, 3, 4, 5];

const evenOddSum = array => array.reduce((acc, cur, id) => (acc[id & 1] += cur,acc), [0,0])

const sum = evenOddSum(numbers);
sum // [9, 6]
```
&nbsp;
##### Transform array of objects into object storing children objects by id
&nbsp;
```
const objectsArr = [
  {
    id: 1,
    name: 'Peter',
    proffesion: 'plumber',
  },
  {
    id: 2,
    name: 'Mark',
    proffesion: 'baker',
  },
  {
    id: 3,
    name: 'Greg',
    proffesion: 'firefighter',
  },
];
```
### Solution
```
const objectsByIdArr = objectsArr.reduce(
  (acc, curr) => ({ ...acc, [curr.id]: curr }),
  {}
);
```
### Result
```
objectsByIdArr {
  '1': { id: 1, name: 'Peter', proffesion: 'plumber' },
  '2': { id: 2, name: 'Mark', proffesion: 'baker' },
  '3': { id: 3, name: 'Greg', proffesion: 'firefighter' }
}
```
&nbsp;
##### 
&nbsp;
##### Filter out data from nested structure
&nbsp;

```
const data = [
  {a: 'pig', b: 'dog', c: ['apple','grape']}, 
  {a: 'cat', b: 'seal', c: ['banana','orange']}, 
  {a: 'fish', b: 'cow', c: ['coconut','pineapple']}
];

```
### Filter out fruits
### Solution
```
const fruitsOnly = data.reduce((totalFruits, obj) => {
  obj.fruits.forEach((f) => totalFruits.push(f))
  return totalFruits;
}, [])
```
### Result
```
fruitsOnly:  [
  'apple',     'grape',
  'banana',    'orange',
  'blueberry', 'raspberry',
  'coconut',   'pineapple'
]
```
### Map
&nbsp;
##### Ranges
```
const range = (from, to, including = true) => {
  const scope = including ? to - from + 1 : to - from - 1;
  return Array(scope)
    .fill(0)
    .map((_, id) => (including ? from + id : from + id + 1));
};
```

## Functional programming
##### Fire function once
```
const once = (once) => {
  let done = false;
  return (...args) => {
    if (!done) {
      done = true;
      once(...args);
    }
  };
};
```
##### Another way
```
const once = (fn) => {
  return (...args) => {
    fn && fn(...args);
    fn = null;
  };
};
```
##### Fire function once and after (for ex. warning)
```
const onceAndAfter = (once, after) => {
  let done = false;
  return (...args) => {
    if (!done) {
      done = true;
      once(...args);
    } else {
      after(...args);
    }
  };
};
```


### Memoization
&nbsp;
#### Fibonacci

```
let cache = [];

const fibo = (n) => {
  if (cache[n] === undefined) {
    if (n === 0) {
      cache[0] = 0;
    } else if (n === 1) {
      cache[1] = 1;
    } else {
      cache[n] = fibo(n - 2) + fibo(n - 1);
    }
  }
  return cache[n];
};
```
