# learn-advanced-javascript

## const and let
+ `const` is used for declaring variables whose value will not change.
```js
// example
const name = "Rishu";
name = "Anand"; // this will show error in assignment to constant variable
```
+ `let` is used for declaring variables whose value could change.
```js
// example
let name = "Rishu";
console.log(name); // this will output as 'Rishu'
name = "Anand";
console.log(name); // this will output as 'Anand'
```

## Templating string
+ enclose string in backticks `` ` ``
+ use `${variableName}` to substitute value of `variableName` in string.
+ use `${validJavaScriptExpression}` to substitute result of `validJavaScriptExpression` in string.
```js
// example
const name = "Rishu";
let age = "18";
console.log(`Hi! My name is ${name} and I am ${age + 2} years old.`);
// this will output as 'Hi! My name is Rishu and I am 20 years old.'
```

## Array Methods

### forEach
 + iterates through an array.
 + runs a callback function for each value in array.
 + returns undefined.

```js
// syntax
array.forEach(function(eachArrayValue, eachIndexInArray, entireArray){
	- do something with parameters
	// order of parameter is important
	// define parameter only which is needed
	// returns nothing
})
```
```js
// example
[1, 2, 3].forEach(function(val, ind, arr){
	console.log(val, ind, arr);
})
// output
// 1 0 [1, 2, 3]
// 2 1 [1, 2, 3]
// 3 2 [1, 2, 3]
```

### map
+ creates new array.
+ iterates through an array.
+ runs a callback function for each value in array.
+ add result of that callback function into new array.
+ returns the new array.

```js
// syntax
array.map(function(eachArrayValue, eachIndexInArray, entireArray){
	- return manipulated_value
	// returns new array of manipulated values
})
```
```js
// example
[1, 2, 3].map(function(val){
	return val*2;
})
// output
// [2, 4, 6]
```

### filter
+ creates new array.
+ iterates through an array.
+ runs a callback function for each value in array.
+ if callback function returns true then that value will be added to the new array.
+ if callback function returns false then that value will be ignored.

```js
// syntax
array.filter(function(eachArrayValue, eachIndexInArray, entireArray){
	- return conditional_statement
	// returns new array with values which return true for condition
})
```
```js
// example
[1, 2, 3].filter(function(val){
	return val <= 2;
})
// output
// [1, 2]
```
### find
+ iterates through an array.
+ runs a callback function for each value in array.
+ if callback function returns true for first time for any value then iteration will stop and that value will be returned.

```js
// syntax
array.find(function(eachArrayValue, eachIndexInArray, entireArray){
	- return conditional_statement
	// returns value which returned true for first time
})
```
```js
// example
[1, 2, 3].find(function(val){
	return val > 1;
})
// output
// 2
```

### some
+ iterates through an array.
+ runs a callback function for each value in array.
+ if callback function returns true for atleast one value in array then it returns true otherwise false.

```js
// syntax
array.some(function(eachArrayValue, eachIndexInArray, entireArray){
	- return conditional_statement
	// returns true if condition is true for atleast one value otherwise returns false
})
```
```js
// example
[1, 2, 3].some(function(val){
	return val <= 2;
})
// true
```

### every
+ iterates through an array.
+ runs a callback function for each value in array.
+ if callback function returns true for every value in array then it returns true otherwise false.

```js
// syntax
array.every(function(eachArrayValue, eachIndexInArray, entireArray){
	- return conditional_statement
	// returns true if condition is true for every value otherwise returns false
})
```
```js
// example
[1, 2, 3].every(function(val){
	return val <= 2;
})
// false
```

### reduce
+ accepts a callback function and an optional second parameter.
+ iterates through a array.
+ runs a callback on each value in the array.
+ the first parameter (or accumulator) to the callback is either the first value in the array or the optional second parameter.
+ the returned value from callback becomes the new value of accumulator.

```js
// syntax
array.reduce(function(accumulator, nextValue, eachIndexInArray, entireArray){
	- return something_using_parameters_which_will_become_next_accumulator
	// returns final value of accumulator
}, optionalSecondParameter)
```
```js
// example
[1, 2, 3, 4].reduce(function(acc, nexVal){
	return acc + nexVal;
})
// output processing
//    acc   nexVal   return
// 1. 1     2        1+2=3
// 2. 3     3        3+3=6
// 3. 6     4        6+4=10
// 4. 10    null     acc
// output = 10
```
```js
// example
[1, 2, 3, 4].reduce(function(acc, nexVal){
	return acc + nexVal;
}, 50)
// output processing
//    acc   nexVal   return
// 1. 50    1        50+1=51
// 2. 51    2        51+2=53
// 3. 53    3        53+3=56
// 4. 56    4        56+4=60
// 5. 60    null     acc
// output = 60
```