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
let age = 18;
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

## Fat-Arrow Function
+ instead of writing `function` keyword use fat-arrow `=>`
```js
// old syntax
let myFunction = function (number){
	return 2*number;
}
// new syntax
let myFunction = (number) => {
	return 2*number;
}
```
+ can remove `return` keyword and curley brackets `{}` if function block has single line of code.
```js
// old syntax
let myFunction = (number) => {
	return 2*number;
}
// new syntax
let myFunction = (number) => 2*number;
```
+ can remove round brackets `()` from function argument list if and only if there is one argument.
```js
// old syntax
let myFunction = (number) => 2*number;
// new syntax
let myFunction = number => 2*number;
// Or
let myFunction = (number => 2*number);
// semicolon restricted placement
let myFunction = (number => 2*number;)
```
+ fat arrow function lexically bind `this` value that is calling a member function using `this` always refers to the enclosing `this`
```js
// unexpected output
let team = {
	members: ["Rishu", "Anand"],
	teamName: "REU",
	summary: function(){
		return this.members.map(function(member){
			return `${member} is on team ${this.teamName}`;
		});
	}
}
team.summary(); // Cannot read property teamName of undefined
```
```js
// correct using self reference
let team = {
	members: ["Rishu", "Anand"],
	teamName: "REU",
	summary: function(){
    let self = this;
		return this.members.map(function(member){
			return `${member} is on team ${self.teamName}`;
		});
	}
}
team.summary(); // ["Rishu is on team REU", "Anand is on team REU"]
```
```js
// correct using function.prototype.bind(this)
let team = {
	members: ["Rishu", "Anand"],
	teamName: "REU",
	summary: function(){
		return this.members.map(function(member){
			return `${member} is on team ${this.teamName}`;
		}.bind(this));
	}
}
team.summary(); // ["Rishu is on team REU", "Anand is on team REU"]
```
```js
// correct using fat-arrow function
let team = {
	members: ["Rishu", "Anand"],
	teamName: "REU",
	summary: function(){
		return this.members.map(member => `${member} is on team ${this.teamName}`);
	}
}
team.summary(); // ["Rishu is on team REU", "Anand is on team REU"]
```

## Object literals
+ `keyValue: keyValue` is equivalent to `keyValue`
+ `keyValue: function(){}` is equivalent to `keyValue(){}`
```js
// old syntax
let a = 1, b = 2, num = 3;
let o = {
	a: a,
	b: b,
	c: num,
	d: function(){
		return this.a + this.b === this.c;
	}
};
console.log(o); // {"a":1,"b":2,"c":3}
console.log(o.d()); // True

// new syntax
let a = 1, b = 2, num = 3;
let o = {
	a,
	b,
	c: num,
	d(){
		return this.a + this.b === this.c;
	}
};
console.log(o); // {"a":1,"b":2,"c":3}
console.log(o.d()); // True
```

## Default function argument
+ if function is called without argument than default argument value is used.
```js
// old syntax
function print(name){
	if(!name){
		name = "Hello World";
	}
	return name;
}
console.log(print()); // Hello World
console.log(print("Rishu Anand")); // Rishu Anand

// new syntax
function print(name = "Hello World"){
	return name;
}
console.log(print()); // Hello World
console.log(print("Rishu Anand")); // Rishu Anand
```

## Promise and Async-Await
+ promise object represents the eventual completion (or failure) of an asynchronous operation, and its resulting value.
+ asynchronous function operates asynchronously via the event loop, using an implicit Promise to return its result.
+ syntax and structure of using async functions is much more like using standard synchronous functions.
+ async function contains await expression that pauses the execution of the async function and waits for the passed Promise's resolution, and then resumes the async function's execution.
```js
// example 1

// callback
getData(id, (foundedData, error) => {
	if (!error) {
		updateData(foundedData, changes, (updatedData, error) => {
			if (!error) {
				console.log(updatedData);
			} else {
				console.log(error);
			}
		});
	} else {
		console.log(error);
	}
});

// promise
getData(id)
	.then(foundedData => updateData(foundedData, changes))
	.then(updatedData => console.log(updatedData))
	.catch(error);
// OR
let foundedData = getData(id)
	.catch(error);
let updatedData = updateData(foundedData, changes)
	.catch(error);
console.log(updatedData);

// async-await
async function findAndUpdateData(id, changes) {
	try {
		let foundedData = await getData(id);
		let updatedData = await updateData(foundedData, changes);
		console.log(updatedData);
	} catch (error) {
		console.log(error);
	}
}
```
```js
// example 2
// syntax comparison for printing in order

// setTimeout is acting like a function which takes
// t seconds to print the string where t = length of string

// calling order
// print("hello world");
// print("hello");
// console.log("done");

// result order wanted
// hello world
// hello
// done
```
```js
// sync
function syncPrint(str) {
    setTimeout(() => {
        console.log(str);
    }, str.length*1000);
}
syncPrint("hello world");
syncPrint("hello");
console.log("done");

// result
// done
// hello
// hello world

// "hello world" waits for 11 seconds
// "hello" waits for 5 seconds
// "done" waits for nothing
// that is expected order of result but not what we wanted
```
```js
// promise
function promisePrint(str) {
    return new Promise(resolve => {
        setTimeout(() => {
            console.log(str);
            resolve();
        }, str.length*1000);
    });
}
promisePrint("hello world")
	.then(() => promisePrint("hello"))
	.then(() => console.log("done"));

// result
// hello world
// hello
// done

// result is what we wanted but code looks almost like
// callback hell with more indentations
```
```js
// async
function asyncPrint(str) {
    return new Promise(resolve => {
        setTimeout(() => {
            console.log(str);
            resolve();
        }, str.length*1000);
    });
}
async function forAyncPrint() {
    await asyncPrint("hello world");
    await asyncPrint("hello");
    console.log("done");
}
forAyncPrint();

// result
// hello world
// hello
// done

// result is what we wanted, code looks almost like sync
// and with less indentations but await is valid only in
// async functions and hence needs an extra calling
// function, still its useful because calling function
// also returns promise if called function has return
// statement
```
```js
// example 3
// fetching and logging as per need

const data = [
  { info: 'first', wait: 3000 },
  { info: 'second', wait: 2000 },
  { info: 'third', wait: 1000 }
];

// to get info with some delay
function getInfo(d) {
  return new Promise(resolve => {
    setTimeout(() => resolve(d.info), d.wait);
  });
}

// result of logInOrder
// first
// second
// third

// result of logOutOfOrder
// third
// second
// first
```
```js
// log in order using promises
// promises are resolved in parallel
// but logged in order using reduce chain
function logInOrderPromise(data) {
  // get all infos
  const infoPromises = data.map(d => getInfo(d));
  // log them in order
  infoPromises.reduce((chain, infoPromise) => {
		return chain.then(() => infoPromise)
			.then(info => console.log(info));
  }, Promise.resolve());
}
logInOrderPromise(data);
```
```js
// log in order using async await
// promises are resolved and logged one by one
async function logInOrderAsync(data) {
  for (const d of data) {
    console.log(await getInfo(d));
  }
}
logInOrderAsync(data);
```
```js
// log in order using async await
// promises are resolved in parallel
// but logged in order using await in standard for loop
async function logInOrderAsyncParallel(data) {
  // get all infos
  const infoPromises = data.map(async d => await getInfo(d));
  // log them in order
  for (const infoPromise of infoPromises) {
    console.log(await infoPromise);
  }
}
logInOrderAsyncParallel(data);
```
```js
// log which resolves first using promises
function logOutOfOrderPromise(data) {
  data.forEach(d => getInfo(d).then(info => console.log(info)));
}
logOutOfOrderPromise(data);
```
```js
// log which resolves first using async await
function logOutOfOrderAsync(data) {
  data.forEach(async d => console.log(await getInfo(d)));
}
logOutOfOrderAsync(data);
```