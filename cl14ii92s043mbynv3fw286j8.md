## How Do I Copy an Array in JavaScript?

In JavaScript, when you assign a string or number variable to a new variable you get two copies of the same string or number. You probably wouldn't expect anything you do to one of those variables afterward to affect the other variable.

![let myNumber = 42;
let myNewNumber = myNumber;
console.log(myNumber); // 42
console.log(myNewNumber); // 42
myNewNumber = 80;
console.log(myNumber); // still 42
console.log(myNewNumber); // now 80](https://cdn.hashnode.com/res/hashnode/image/upload/v1647792002558/koGppebxH.png)

But, if you assign an array to a new array, it doesn't quite work that way.

![const myScores = [31, 48, 24, 19, 45];
const myNewScores = myScores;
console.log(myScores); // (5) [31, 48, 24, 19, 45]
console.log(myNewScores); // (5) [31, 48, 24, 19, 45]
myNewScores[0] = 21;
console.log(myScores); // (5) [21, 48, 24, 19, 45]
console.log(myNewScores); // (5) [21, 48, 24, 19, 45]
](https://cdn.hashnode.com/res/hashnode/image/upload/v1647794182217/YjqLmnBFp.png)

What's going on here? We made a change to `myNewScores`, but `myScores` changed too. Why would that happen?

This is because of a difference in how JavaScript treats its primitive types, like number and string, and its non-primitive types, like arrays and objects. This is often referred to as "by value" and "by reference".

As a metaphor, you can think of a number variable "holding" the number you assign to it, but an array variable "holding" directions to where to find the actual array.

So, when you assign `myNumber` to `myNewNumber`, what gets put in `myNewNumber` is the value 42.

![let myNumber = 42;
let myNewNumber = myNumber;
](https://cdn.hashnode.com/res/hashnode/image/upload/v1647795961587/pZyw7-Dv9.png)

But, when you assign `myScores` to `myNewScores`, what gets put into `myNewScores` is a reference (the directions) to where the actual array is stored.

![const myScores = [31, 48, 24, 19, 45];
const myNewScores = myScores;
](https://cdn.hashnode.com/res/hashnode/image/upload/v1647796159522/STdP7zH9I.png)

So, `myScores` and `myNewScores` are both pointing to the same place. Whichever one you access, your code is going to go to the same place to find the array.

So, if what you want is a copy of an array, and not just a copy of the directions to the array, you'll need to get the values out of the array and assign **that** to your new array. There are many ways you could do that.

One common way is to use `.slice()` on the original array. With no arguments, `.slice()` will return the whole array. A similar approach would also work with other array methods like `.map()`, `.filter()`, or `.reduce()` as long as you set the method to return the whole array.

![const myScores = [31, 48, 24, 19, 45];
const myNewScores = myScores.slice();
myNewScores[0] = 21;
console.log(myScores); // (5) [31, 48, 24, 19, 45]
console.log(myNewScores); // (5) [21, 48, 24, 19, 45]
](https://cdn.hashnode.com/res/hashnode/image/upload/v1647798620028/l1jkl8ma0.png)

You can also use the `Array.from()` static method which was introduced in ES2015 to create a new array from the old array and assign that.

![const myScores = [31, 48, 24, 19, 45];
const myNewScores = Array.from(myScores);
myNewScores[0] = 21;
console.log(myScores); // (5) [31, 48, 24, 19, 45]
console.log(myNewScores); // (5) [21, 48, 24, 19, 45]
](https://cdn.hashnode.com/res/hashnode/image/upload/v1647799349032/EbkgmDYZ_.png)

Or, you can use array literal brackets and spread syntax `...` to expand the old array into a new array and assign that.

![const myScores = [31, 48, 24, 19, 45];
const myNewScores = [...myScores];
myNewScores[0] = 21;
console.log(myScores); // (5) [31, 48, 24, 19, 45]
console.log(myNewScores); // (5) [21, 48, 24, 19, 45]
](https://cdn.hashnode.com/res/hashnode/image/upload/v1647799687590/mbnxFUieN.png)

These methods all result in "shallow" copies, which work fine for the simple arrays in these examples. But, if your original array contains nested arrays or objects, those sub-items in your new array would still be references (directions) to the original sub-items.

This idea of "by value" and "by reference" pops up in other areas too. Thinking of "by value" as "the thing" and "by reference" as "directions to the thing" is helpful to me to understand how that works.
