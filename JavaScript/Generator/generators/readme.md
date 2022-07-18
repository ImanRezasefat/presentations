# Javascript generators

**Generators** are functions that can be played and paused during execution.<br>
In order to understand how generators work you need to have an understanding of these concepts:<br>
**Symbol**:A Symbol is a unique and immutable primitive value and may be used as the key of an Object property.<br>
**prototype**:Prototypes are the mechanism by which JavaScript objects inherit features from one another.<br>
**iterators**: well generators are a kind of iterator so we go deep dive on this one so no one-line explanation.<br>
## Js Iterators
What is an iterator? Any object that implements an iterable protocol(or could be in its prototype chain). In order to implement the protocol, you will need to add a function to that object with the key [Symbol.iterator] this object performs the iteration using the next method. The result of next can be { value:result, done:false } for there is more to come and {value:result, done:true} for it is the end of iteration.
So to make a normal object to an iterable object we will do:
```sh
normalObject = {};
normalObject[Symbol.iterator] = function() {
return {
next() {
return {value:'result', done:done}; } };}
```
## Iterable objects
Arrays,maps,strings and sets are iterators so if you look into their prototype you will the property [Symbol.iterator] . If you want to check that out you can do this:
```sh
let myArray = [1];
console.dir(myArray);
//result includes Symbol(Symbol.iterator): ƒ values()
```
Lets work with the iteration obejct of an array. We can use the key [Symbol.iterator] to get the iterator object and then call next function enough times to get to done true.
```sh
const array = [1];
//used [Symbol.iterator] key to get the object and called its function so can access to next function
const iterator = array[Symbol.iterator]()
iterator.next();//first call result {value: 1, done: false}
iterator.next();//second call result {value: undefined, done: true}
```
## Iterating tools
One way to go through iterators is using next which you already saw above. You can also use spread operator and for..of with iterators.
## generators
Getting back to generators now. A generator is a kind of an iterator that is defined like this :
```sh
function* myUselesGenReturnsOneAndTwo() {
yield 1;
yield 2;
}
```
The star after function keyword indicates that this is a generator and the yield key is like the return for normal functions with the exception that it is not returned at all. What yield does is it returns the value of the first yield and pauses the function right there waiting for the next next() call causes remember it is an iterator.
The keynote about generators is that the value is calculated when it is needed so it is efficient to use generators when your iteration objects are in need of heavy calculation or need a lot of memory.
### yield* keyword
Using yield with the star is like calling spread with iterator it will go through all iterations. So careful with infinite loops.


resources:
JavaScript: The Definitive Guide
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*
https://dev.to/rfornal/use-cases-for-javascript-generators-1npc
