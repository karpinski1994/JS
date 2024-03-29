# JS
Some helpful tips, tricks, good practices and ready-made solutions in Javascript / Typescript

# List of javascript useful practical tricks and patterns

---
1. [Arrays](#arrays)
    1. [Reduce](#reduce)
          1. [Sum values](#sum_values_of_array)
          1. [Count the average](#count_average_of_array_1)
          1. [Calculate several values at once](#calculate_several_values_at_once)
          1. [Calculate items](#calculate_items_in_an_array_2)
          1. [Find min and max](#find_min_and_max_in_array)
          1. [Find min and max](#sum_even_and_odd_numbers_in_one_go)
          1. [Calculate items](#calculate_items_in_an_array_2)
          1. [Parse array of objects into an object](#parse_array_of_obj_into_an_obj)
          1. [Filter out data from a nested structure](#filter_out_data_from_nested_structure)
    1. [ReduceRight](#reduce_right)
          1. [Reverse a string](#reverse_string_reduce_rightt)
    1. [Map](#array_map)
          1. [Creating ranges](#creating_ranges)
          1. [Extracting data from objects](#extracting_data_from_obj)
          1. [Parsing to float](#parse_float)
          1. [Create an alphabet](#create_an_alphabet)
    1. [Flat](#array_flat)
          1. [Process nested arrays](#process_nested_arrays)
          1. [Extract data from nested API](#extract_data_from_nested_api)
    1. [FlatMap](#array_flat_map)
    1. [Filter](#array_filter)
          1. [Filter out falsy values](#filter_out_falsy_values)
2. [Functional programming](#functional_programming)
    1. [Currying](#currying)
    	  1. [Summing numbers](#currying_summing_numbers)
          1. [Adding vat](#add_vat)
    1. [Partial application](#partial_app)
          1. [Summing numbers](#partial_app_summing_numbers)
    1. [Recursion](#recursion)
          1. [Decrease and conquer - searching](#decrese_and_conquer_searching)
          2. [Numbers exponential](#exponention)

         

---

&nbsp;
<a name="arrays"></a>
## Arrays
<a name="reduce"></a>
### Reduce
&nbsp;
<a name="sum_values_of_array"></a>
##### Sum values of an array
&nbsp;

```
const numbers = [29.76, 41.85, 46.5];

const sum = numbers.reduce((total, amount) => total + amount);

sum // 118.11

// Other way

const sum = (acc, value) => acc + value;
const mySum = numbers.reduce(sum, 0);

```
&nbsp;
<a name="count_average_of_array_1"></a>
##### Count the average of array
&nbsp;
```
const numbers = [29.76, 41.85, 46.5];

const average = (array) => array.reduce((a, b) => a + b) / array.length;

const avg = average(numbers)
avg // 39.37


// 2nd way
const avg = array.reduce(sum, 0) / array.length;

// 3rd way
const avg2 = (sum, val, id, arr) => {
  sum += val;
  return id === arr.length - 1 ? sum / arr.length : sum;
};

```
<a name="calculate_several_values_at_once"></a>
##### Calculating several values at once
&nbsp;
```
// Object
const average = arr => {
const sumCount = arr.reduce(
  (acc, val) => ({sum: val + acc, count acc.count + 1}),
  {sum: 0, count: 0});

  return sumCount.sum / sumCount.count;
}

// Array
const average = arr => {
const sumCount = arr.reduce(
  (acc, val) => ({sum: acc[0] + val, count acc[1] + 1}),
  [0, 0]);

  return sumCount[0] / sumCount[1]
}
```
<a name="calculate_items_in_an_array_2"></a>
##### Calculate itams in an array
&nbsp;
```
const brands = ['suzuki', 'suzuki', 'mercedes', 'audi', 'mercedes'];

const brandsCount = arr.reduce(
    (acc, val) => ({ ...acc, [val]: acc[val] ? acc[val] + 1 : 1}),
    {}
  );

```
#### Result
```
{
  audi: 1
  mercedes: 2
  suzuki: 2
}
```
<a name="find_min_max_in_array"></a>
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
<a name="sum_even_and_odd_numbers_in_one_go"></a>
##### Sum even and odd numbers in one go
&nbsp;
```
const numbers = [1, 2, 3, 4, 5];

const evenOddSum = array => array.reduce((acc, cur, id) => (acc[id & 1] += cur,acc), [0,0])

const sum = evenOddSum(numbers);
sum // [9, 6]
```
&nbsp;
<a name="parse_array_of_obj_into_an_obj"></a>
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
<a name="filter_out_data_from_nested_structure"></a>
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
&nbsp;
<a name="reduce_right"></a>
### reduceRight
&nbsp;
<a name="reverse_string_reduce_rightt"></a>
##### Reverse string
```
const reverseString = str => str.split('').reduceRight((x, y) => x + y, '');
```
<a name="array_map"></a>
### Map
&nbsp;
<a name="creating_ranges"></a>
##### Ranges
```
const range = (from, to, including = true) => {
  const scope = including ? to - from + 1 : to - from - 1;
  return Array(scope)
    .fill(0)
    .map((_, id) => (including ? from + id : from + id + 1));
};
```
&nbsp;
<a name="extracting_data_from_obj"></a>
##### Extracting data from objects
```
const cities = [
  {name: 'New York', long:40.7128, lat: 74.0060},
  {name: 'Tokyo', long:25.2048, lat: 55.2708},
  {name: 'Krakow', long:50.0647, lat: 19.9450},
]

const avgLong = average(cities.map(city => city.long))
const avgLat = average(cities.map(city => city.lat))
```
&nbsp;
<a name="parse_float"></a>
##### Parse float
```
const numbers = ['4.2332', '12.221', '2131.4367'].map(parseFloat);

// Doesnt work with parseInt! which takes more args
```
&nbsp;
<a name="create_an_alphabet"></a>
##### Create alphabet
```
const ALPHABET = range('A'.charCodeAt(), 'Z'.charCodeAt()).map(code => String.fromCharCode(code));

```
<a name="array_flat"></a>
### Flat
&nbsp;
<a name="process_nested_arrays"></a>
##### Process nested arrays
```

const numbers = [1, 2, [[3, (4)[(5, 6)]][(7, 8)]]];

const oneLevelDeep = numbers.flat(1);

const twoLevelsDeep = numbers.flat(2);

const flattedTotally = numbers.flat(Infinity);


```
&nbsp;
<a name="extract_data_from_nested_api"></a>
##### Extract participants from nested api structure
```
const apiAnswer = [
  {
    id: 122232,
    name: 'John Doe',
    groups: [
      {
        groupId: 121221,
        groupName: 'Doplphins',
        participants: [{ participantId: 3846864, name: 'Max' }],
      },
    ],
  },
  {
    id: 122233,
    name: 'Marry Cohen',
    groups: [
      {
        groupId: 232131,
        groupName: 'Alaska Team',
        participants: [{ participantId: 2644487, name: 'Merry' }],
      },
    ],
  },
  {
    id: 122234,
    name: 'Christine Malone',
    groups: [
      {
        groupId: 12121221,
        groupName: 'Tigers',
        participants: [
          {
            participantId: 50720006,
            name: 'Harry',
          },
          {
            participantId: 4899911,
            name: 'Barry',
          },
          {
            participantId: 4899966,
            name: 'Lissie',
          },
        ],
      },
    ],
  },
];


```
#### Solution
```
  apiAnswer.map(x => x.groups)
  .flat()
  .map(y => y.participants)
  .flat()
```
#### Result
```
[
  {
    name: 'Max',
    participantId: 3846864,
  },
  {
    name: 'Merry',
    participantId: 2644487,
  },
  {
    name: 'Harry',
    participantId: 50720006,
  },
  {
    name: 'Barry',
    participantId: 4899911,
  },
  {
    name: 'Lissie',
    participantId: 4899966,
  },
]
```
<a name="array_flat_map"></a>
### FlatMap
&nbsp;
##### Same example as above
```
apiAnswer
  .flatMap(x => x.groups)
  .flatMap(y => y.participants)
```
<a name="array_filter"></a>
## Filter
<a name="filter_out_falsy_values"></a>
#### Filter out falsy values 
```
[1, 2, 3, 0].filter(Boolean)
// result [1, 2, 3]
```

&nbsp;
## Every
#### Make none using every (function returning true  only when non of elements pass the predicate)
```
const none = (arr, fn) => arr.every(v => !fn(v));
```

&nbsp;
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

#### Factorial by range
&nbsp;
```
const factorialByRange = n => range(1, n).reduce((x, y) => x * y, 1); 
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



### Working with objects
&nbsp;
#### Getting a property from an object

```
const cities = [
  { name: 'New York', long: 40.7128, lat: 74.006 },
  { name: 'Tokyo', long: 25.2048, lat: 55.2708 },
  { name: 'Krakow', long: 50.0647, lat: 19.945 },
];

const avgLong = average(cities.map((city) => city.long));
const avgLat = average(cities.map((city) => city.lat));
```

#### Get field value
```
const example = {
  name: 'Tom',
  age: 26,
}

const getField = attr => obj => obj[attr];

const getName = getField('name)';
const getAge = getField('age)';

getName(example) // "Tom"
getAge(example) // 26

// From previous example
cont avgLon = average(cities.map(getField('lon'))); // 38.66076666666667
cont avgLat = average(cities.map(getField('lat')));

// Also see lodash: .get, .property, .propertyOf
```


#### Logically negating a function
```
const not = fn => (...args) => !fn(...args);
```

#### Reversed filter
```
const filterNot = arr => fn => arr.filter(not(fn));
```
#### Inverting results
```
const invert = fn => (...args) => -fn(...args);
```

<a name="functional_programming"></a>
## Functional programming
<a name="currying"></a>
##### Currying
&nbsp;
```
const exampleFn = (a, b, c) => `${100 * a + 10 * b + c}`;
const exampleCurried = a => b => c => `${100 * a + 10 * b + c}`;
```
<a name="currying_summing_numbers"></a>
##### Sum numbers using currying
&nbsp;
```
// Normal way
const sumNumbers = (a, b, c, d) => a + b + c + d;
// sumNumbers(1,2,3,4) => 10

// Currying by hand

const curriedSumNumbers = a => b => c => d => a + b + c + d;
// curriedSumNumbers(1)(2)(3)(4) => 10
```

<a name="add_vat"></a>
##### Adding vat curried way
&nbsp;
```
const addVAT = (rate, amount) => amount * (1 + rate / 100); 
// addVAT(20,500) => 600

// Curried example
const addVATcurried = rate => amount => amount * (1 + rate / 100);
const addFoodVAT = addVATcurried(18);
// addFoodVAT(100) => 118
```

<a name="partial_app"></a>
### Partial application
&nbsp;

<a name="partial_app_summing_numbers"></a>
##### Sum numbers using partial application
```
// Partial application by hand
const sumNumbers = (a, b) => a + b;
const partial = (fn, ...args) => (...moreArgs) => fn(...args, ...moreArgs)
const add1 = partial(sumNumbers, 1);
// add1(2) => 3

// Using js bind
const sumNumbers = (a, b, c, d) => a + b + c + d;
const partiallyAppliedSumNumbers = sumNumbers.bind(null, 1, 2);

// partiallyAppliedSumNumbers(3,4) 10

const otherPartiallyAppliedSumNumbers = partiallyAppliedSumNumbers.bind(null, 3);
// otherPartiallyAppliedSumNumbers(4) => 10

```

<a name="recurion"></a>
### Recursion
<a name="recurion"></a>
##### Decrease and conquer - searching
<a name="decrese_and_conquer_searching"></a>
##### Checking if the value is in array
&nbsp;
```

const isInArray = (arr, key) => {
  if (arr.length === 0) {
  	return false;
  } else if (arr[0] === key) {
  	return true;
  } else {
  	return isInArray(arr.slice(1), key);
  }
}

const numberArr = [1, 3, 4];

// isInArray(numberArr, 3) => true
// isInArray(numberArr, 3) => false

const isInArray2 = (arr, key) => arr.length === 0 ? false : arr[0] === key || isInArray2(arr.slice(1), key);

const arra = [1, 3, 4];

// isInArray(arra, 3) => true
// isInArray(arra, 2) => false

const isInArray3 = (arr, key) => arr.length && (arr[0] === key || isInArray2(arr.slice(1), key))
// this will return 0 (array length) if there's no searched value
```

<a name="exponention"></a>
##### Exponentiation of numbers
&nbsp;
```
const powerN = (base, power) => {
	if(power === 0) {
  	return 1;
  } else if (power % 2) {
  	return base * powerN(base, power-1);
  } else {
  	return powerN(base * base, power / 2);
  }
}

// powerN(2, 10) => 1024
```

