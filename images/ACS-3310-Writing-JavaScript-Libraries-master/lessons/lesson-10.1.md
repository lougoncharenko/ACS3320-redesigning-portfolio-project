# ACS 3310 - TypeScript Activities

## Activity: Getting started with Typescript

### Why this activity?

TypeScript is becoming more popular, and is extremely useful in large codebases. Knowing how to refactor, write, and publish TypeScript code will allow you to decide whether TypeScript is right for a project.

Writing TypeScript will also force you to think about the types you use in the code you write which will make a you a stronger programmer.

### **Activity 1** 

Write a function called **helloWorld** that takes in a name(string) as a parameter and return:

**"hello, {name}!"**

**For example:** If given 'Liya' as the parameter, your function should return "Hello, Liya!"

### **Activity 2** 

Write a function called **getSalary** that given a base salary of an employee and a number to multiply the base salary with, returns the total salary of a Person.

**For example:** 
Inputs: base salary -> 80,000
        number to multiply -> 5
Output: 400,000

### **Activity 3**

Given an input data of an employee object, return a tuple with 3 elements:
-  first name, last name and age

*INFO*: A tuple is an array of fixed length with each element a certain type.

**For example:** 

*Inputs* -> 
employeeObj : 
```js
{
  firstName: "Jane",
  lastName: "Doe",
  role: "Software Engineer",
  age: 30,
  manager: "Jorja Smith",
  getSalary: (base: number, num: number) =>  base * num
}
```
Output ->
```js
["Jane", "Doe", 30]
```

### **Activity 4**

Interfaces describe the shape of an object. 

They have the keyword 'interface'. They are the blueprints of any object of that structure that we want to make.

* Create an interface called Employee, for the employee object from Activity 3

This interface has has ```firstName, lastName, role, age, manager and getSalary``` as its data types.

- firstName, lastName, role and manager are type string
- age is type number
- getSalary is a function that takes an argument of base salary (type number) and a number (type number), and returns the total salary of an Employee


### **Activity 5**

Make ```age``` an optional property from the interface you created on Activity 4.

An interface can contain optional properties and we use **?:Type** annotation to represent them, just like the optional function parameters.


### **Activity 6**

Define an object of type Employee with 

- first name: Jane
- last name: Doe
- age: 35
- role: Data Scientist
- manager: Trevor Noah
- base salary: 5,000
- total salary is calculated by multiplying base salary by num

then store it inside a variable named 'jane'.

Calculate the total salary of Jane using the **getSalary** function and print the salary to the console

## Using enum

### **Activity 7**

Enums allow us to define or declare a collection of related values that can be numbers or strings as a set of named constants.

By default, TypeScript enums are number based. This means that they can store string values as numbers

Example:
```js
enum Weekend {
  Friday,
  Saturday,
  Sunday
}
```

In the code block above, we have an enum we call `Weekend`. The enum has three values namely: `Friday`, `Saturday` and `Sunday`. In TypeScript, just like in some other languages, enum values start from zero and increase by one for each member. They will be stored like this:

```
Friday = 0
Saturday = 1
Sunday = 2
```

#### Your task is to write  a function that takes a string as an argument and returns a weekend

if the string is 'TGIF', it should return the enum member Friday (Weekend.Friday)


### **Activity 8**

Improve your enum by making it a string enum.

String enums are enums where the member values are strings.

So instead of the members having an integer as a value, you can assign a string to them.

Example: Friday = 'FRIDAY'

