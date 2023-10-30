<!-- .slide: data-background="./Images/header.svg" data-background-repeat="none" data-background-size="40% 40%" data-background-position="center 10%" class="header" -->
# ACS 3310 - Lesson 11

<small style="display:block;text-align:center">Writing in TypeScript</small>

<!-- ([slides](https://docs.google.com/presentation/d/1ovt7YeAfqaiN8duWjwhYxldTwvca382QTHYyBUFZZ_8/edit)) -->

In this class, you will begin learning to use Typescript to solve more advanced problems.

<!-- Put a link to the slides so that students can find them -->

<!-- ➡️ [**Slides**](/Syllabus-Template/Slides/Lesson1.html ':ignore') -->

<!-- > -->

## Learning Objectives

1. Define instance properties and their types
1. Use enums
1. Use generics
1. Write types for functions

<!-- > -->

# Review 

Download the examples here: https://github.com/Tech-at-DU/typescript-intro

Take a look at `example-8.ts` and `example-9.ts` add the types and compile it. 

<!-- > -->

# Classes 

<!-- > -->

Classes are used to create instances of objects. Objects store values as properties. These properties have types!

<!-- > -->

Consider the Person class below. It needs some types. 

```JS
class Person {
	constructor(name, age) {
		this.name = name 
		this.age = age
	}
}
```

<!-- > -->

In typescript the syntax for a class looks like this: 

```JS
class Person {
	name: string // instance variables!
	age: number  // set types here!

	constructor(name: string, age: string) {
		this.name = name 
		this.age = age
	}
}
```

<small>Person stores `name` a string, and `age` a number.</small>

<!-- > -->

Class methods are defined like functions: 

```JS
class Person {
	...
	describe(): string {
		return `${this.name} is ${this.age}`
	}

	setAge(newAge: number) {
		this.age = newAge
	}
}
```

<!-- > -->

Try `example-10.ts` and `example-11.ts`

<!-- > -->

# Enumerations 

<!-- > -->

An enumeration is a named set values. These act like constants you might define to describe all of the possible choices that are be avaiable. 

<!-- > -->

Use enumerations, enum for short, to name the possible choices. 

For example: 

- Units - Metric, Standard, Imperial
- Direction - North, South, East, West

<!-- > -->

Why use an enum? 

- More reliable than strings 
- Descriptive choices
- Prevents erroneous values

<!-- > -->

Consider this typical scenario: 

```JS
function getWeather(zip, apikey, unit = 'metric') {
  // ...
}
```

Using a string to represent a range of possible values for unit.

```JS
getWeather(zip, apikey, 'millimeters') 
```

What could go wrong? 

<!-- > -->

**Constants**: Defining contants is good but doesn't show that these values work together. Your constants are in a pool of other variables. 

```JS
const METRIC = 'metric'
const IMPERIAL = 'imperial'
const STANDARD = 'standard'
const KEY = '123456'

function getWeather(zip, apikey, unit = METRIC) {
  // ...
}
```

Better, but what is STANDARD? What is KEY could it be a unit? 

<!-- > -->

Another possible choice might be an **object**: 

```JS
const Units = {
  metric: 'metric',
  imperial: 'imperial',
  standard: 'standard'
}

function getWeather(zip, apikey, unit = Units.metric) {
  // ...
}
```

This is getting better but not perfect. 

```JS
Units.millimeters = 'mm'
```

<!-- > -->

With typescript you can define an enum! 

```TS
enum Unit {
  metric,
  imperial,
  standard
}

function getWeather(
	zip: string, apikey: string, unit: Unit = Unit.metric) {
  // ...
}
```

<!-- > -->

These are the possible choices for units in the openweathermap API. Unlike the methods above TypeScript would check against the enum and would show an error if we used a value not on the list! 

<!-- > -->

In many situations you have a limited set of choices and your program should always choose from that set. An enum guarantees that you will always choose from the possible choices! 

<!-- > -->

Under the hood enums are just objects with keys. You could have done this but TypeScript does it for you and adds error checking! 

<!-- > -->

Imagine you are making a game or mapping app. It needs to work with the compass directions.

```TS
// Define an enum that represents the possible directions 
enum Direction {
	North, South, East, West
}
```

<!-- > -->

An enum can be used as a value and a type. The function takes the `Direction` enum as the parameter and check it against possible cases in the switch block. 

```TS
function move(direction: Direction) { // direction is enum type
	switch(direction) {
		case Direction.E:
			// Go East
		case Direction.W:
			// Go West
		case Direction.N:
			// Go North
		case Direction.S: 
			// Go South
	}
}
```

<!-- > -->

So what's the value of an enum? 

```TS
console.log(Direction.N) // 0
```

Under the hood an enum is an array and each of the cases is just the index of that case. 

<!-- > -->

Some times it's useful to assign a value to each case of an enum. For example maybe our program needs to print the direction.

<!-- > -->

With the current code this `printDirection` function is not very useful.

```TS
let currentDirection = Direction.N

function printDirection() {
	console.log(`You are travelling ${currentDirection}`)
}

printDirection()
```

The output here is: `You are travelling 0` which isn't very useful. 

<!-- > -->

Each case for an enum can also be a value.

```TS
enum Direction {
	N = 'North', // Set each case to a string
	S = 'South',
	E = 'East',
	W = 'West',
}
```

With this change everything works the same as before but the value of the enum is represented as the strings you defined: 

```TS
console.log(Direction.N) // 'North'
printDirection() // You are travelling North
```

<!-- > -->

Try the challenges in `example-12.ts`

<!-- > -->

Read more about enums here: 

- https://www.typescriptlang.org/docs/handbook/enums.html
- https://2ality.com/2020/01/typescript-enums.html
- https://en.wikipedia.org/wiki/Enumerated_type

<!-- > -->

## Functions as Types

<!-- > -->

In Typescript functions are also expressed as types. 

A function that receives a function as a parameter or returns a function must describe that function as a type.

<!-- > -->

```TS
const add: (number, number) => number = (a: number, b: number ) => {
	return a + b
} 
```

<!-- > -->

For example: 

```JS
// This function returns a function that returns a string
function sayHello(): () => string {
	return () => 'Hello'
}
// This variable contains a function that returns a string
const hello = sayHello()
// Calling the function returns the string
console.log(hello())
```

Challenge modify the function above to take a string: Name as input and combine that with the output. The output of the returned function should read: `Hello ${name}`.

<!-- > -->

Let's try that again. Write a function that takes a number as input and returns a function. The returned function should return value multiplied by the input number. 

```JS 
function mathematizer(n: number): (number) => number {
	let sum = n
	return (x) => x * n
}

const m = mathematizer(3)
console.log(m(3))   // 9
console.log(m(2))   // 6
console.log(m(10))  // 30
console.log(m(111)) // 333

// Challenge - Write a function that takes a function doLater(). It should
// take a callback and a time in milliseconds. It should run the callback 
// after the time.

function doLater() {

}

doLater(() => {}, 2000) // executes the callback in 2 secs.
```

<!-- > -->

Try the challenges in `example-13.ts` and `example-14.ts`

<!-- > -->

## Generic types 

Generic types solve the situation where you have a function that defines a parameter that can take an argument of different types.

<!-- > -->

Imagine the following: 

```JS
const a = 22
const b = 'Zen'
const c = { name: 'Yin', age: 44 }

function sendItBack(thing: any): any {
	return thing
}

console.log(sendItBack(a))
console.log(sendItBack(b))
console.log(sendItBack(c))
```
How can you make this type safe?


<!-- > -->

There is something subtle going on here. The function above takes any type as an input and returns any type as an ouput. 

🔬

<!-- > -->

So what's the problem? There is no guarantee that the input will match the output! 

🍎 ➡️ 🍎

🍊 ➡️ 🍊

🍐 ➡️ 🍓 😱

<!-- > -->

Using `any` here works but it's not type safe. What if the function transformed the input into another type? 

<!-- > -->

While this example seems contrived, because it is, it is more common than you might think! 

Think of some examples where this might occur?

<!-- > -->

Where generics come into play often is Arrays. 

Think about functions like: `push`, `slice`, `splice` and `reverse`.

<!-- > -->

```JS
function sendItBackString(thing: string): string {...}
function sendItBackNumber(thing: number): number {...}
function sendItBackBoolean(thing: boolean): boolean {...}
// ... this tedious and impossible
```

Thisa is not a scalable solution! 

<!-- > -->

Solve this problem with a generic:

```JS
// Solve sendItBack with a generic type <T>
// Challenge - replace any with a generic type T
function sendItBack<T>(thing: T): T {
	return thing
}
```

The generic type is expressed as `<T>` and you'll use `T` where that type is needed. Here `thing` is type `T` and the function returns something of type `T`. 

<!-- > -->

Imagine you have a function that takes in an array, of any type, and it prints the type of each item in the array: 

```JS
const numbers = [1, 43, 6, 71, 8]
const names = ['Ann', 'Bob', 'Cen', 'Dan']
const objs = [{ name: 'Eun', age: 23 }, { name: 'Fin', age: 32 }]

function getTypes<T>(arr: T[]) {
	arr.forEach(thing => console.log(typeof thing))
}

// One function can handle an array of any type! 
getTypes(numbers) // number, number, number, number, number
getTypes(names)   // string, string, string, string
getTypes(objs)    // object, object
```

Again this is a contrived example but it does something that is not possible without generics.

<!-- > -->

Consider this example. The function here reverses an array, nevermind that Array.reverse() is a thing! For the function below to work it needs to know the type of the input array and the type of the output array. 

```JS
const numbers = [1,2,3,4]

function reverse<T>(arr: T[]): T[] {
	const rra: T[] = [] // new array of type T
	arr.forEach(item => rra.unshift(item))
	return rra
}

console.log(reverse(numbers)) // 4,3,2,1 
```

<!-- > -->

What's going on there? The function takes an array of type `T` and returns an Array of type `T`. Inside the function we declare an array `rra` of type `T` and return this. 

<!-- > -->

Consider this idea. You need to create a function that returns the next item from an array. The function needs to take in an array of any type, and return a function that returns a value that matches the type of the input array. 

<!-- > -->

```JS
function iterate<T>(arr: T[]): () => T {
	let i = -1
	return () => {
		i += 1
		return arr[i]
	}
}

const nextNumber = iterate([3,6,4,1,7,9])
const nextName = iterate(['An', 'Bo', 'Cy', 'De'])

console.log(nextNumber()) // 3
console.log(nextNumber()) // 6
console.log(nextName())   // An
console.log(nextName())   // Bo
```

Here the type of the input array needs to be known and the type of the the return value for the function that is returned. 

<!-- > -->

What if you need more than one generic type? 

<!-- > -->

Consider this: 

```TypeScript
function thing<T, U>(it: T, other: U): { a: T, b: U } {
	return { a: it, b: other }
}
```

Here there are two generic types T and U. 

<!-- > -->

- https://www.typescriptlang.org/docs/handbook/generics.html

<!-- > -->

## Typescript Lab

Continue solving the Typescript Exercisms. 

<!-- > -->

### Homework

<!-- [Assignment 8 - Typescript](../assignments/assignment-08.md) -->

Continue working your final project. 

<!-- > -->

## Additional Resources

1. https://exercism.io/my/tracks/typescript
1. https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html

<!-- > -->
<!-- 
## Minute-by-Minute [OPTIONAL]

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Objectives                |
| 0:05        | 0:15      | Overview                  |
| 0:20        | 0:30      | In Class Activity I       |
| 0:50        | 0:10      | BREAK                     |
| 1:00        | 0:45      | In Class Activity II      |
| 1:45        | 0:05      | Wrap up review objectives |
| TOTAL       | 1:50      | -                         | -->

