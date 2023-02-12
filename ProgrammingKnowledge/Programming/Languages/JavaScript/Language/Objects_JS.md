# Objekte
[Referenz](https://javascript.info/object-methods)


# this Referenz

>The value of `this` is the object “before dot”, the one used to call the method.


``` javascript
let user = { 
	name: "John", 
	age: 30, 
	sayHi() { 
		// "this" is the "current object" 
		alert(this.name);
	} 
}; 

user.sayHi(); // John

```


# The consequences of unbound `this`
 
>If you come from another programming language, then you are probably used to the idea of a "bound `this`", where methods defined in an object always have `this` referencing that object.
>In JavaScript `this` is “free”, its value is evaluated at call-time and does not depend on where the method was declared, **but rather on what object is “before the dot”.**
>The concept of run-time evaluated `this` has both pluses and minuses. On the one hand, a function can be reused for different objects. On the other hand, the greater flexibility creates more possibilities for mistakes.
>Here our position is not to judge whether this language design decision is good or bad. We’ll understand how to work with it, how to get benefits and avoid problems.


# Constructor
