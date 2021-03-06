# Functions: Terms & Behavior in JavaScript

<a style={{color:"blue"}} href="https://forum.burlingtoncodeacademy.com/t/discussion-reusing-procedures-with-functions/269">Discuss in Forum</a>

![functions](https://res.cloudinary.com/btvca/image/upload/c_scale,w_1080/v1599680156/functions_title_card_ftkut4.jpg)

Functions are an essential piece of the JavaScript puzzle. Without them, our code would run wild and overgrown. Our applications would accrue [code debt](https://en.wikipedia.org/wiki/Technical_debt) at an unmanageable rate. We would constantly repeat ourselves. We would constantly repeat ourselves. Civilzations would crumble.

...scratch that last part.

But the point remains; functions are crucial when it comes to organizing your code into *modular*, reusable bits. They're the tool used to write the tools used to make your code work how you want it. 

So, what are they exactly? 

> Functions are pieces of code that can accept an input and return an output where there is some clear relationship between the two.

 There are edge cases, as there always are in programming, but that's the gist. 

 So what's that mean? Let's break it down.

## A simple example

Say we want to write a function that checks to see if a number is even. Going off of the previous definition, it would accept a number as an *input*, and would return a boolean as its *output*. `true` if the number is even, `false` if it's odd. 

 Here is a ***function definition*** AKA ***function declaration*** AKA ***function statement***, that expects a number as a *parameter*, and will do just that.

 ```javascript
function isEven(number){
    if (number % 2 === 0){
        return true
    } else {
        return false
    }
}
isEven(4) // output: true
 ```

 Immediately after the function is declared, it is *called*, with `4` passed in as the *argument*.

# Terms

![dictionary](https://res.cloudinary.com/btvca/image/upload/c_scale,w_1080/v1599683181/dictionary-3163569_1920_hkwpe3.jpg)

That was a lot of new words, so let's answer some questions you might have.

**What's a function definition/declaration?**

A function definition, as the name implies, defines the behavior of a function in relation to the expected parameters (if any are provided). It is done so by using the `function` keyword, followed by a name for the function. In JavaScript, using [camel case](https://en.wikipedia.org/wiki/Camel_case) is the convention. 

In this case, the definition is pretty much the whole thing:

```javascript
function isEven(number){
    if (number % 2 === 0){
        return true
    } else {
        return false
    }
}
```

**What's a parameter?**

In the above example, the *variable* `number` has no value yet, but is rather a placeholder that tells the function what to do with it when a value is provided. That placeholder is called a *parameter*. **It will be replaced with an argument when the function is called**.

**What is an argument?**

An argument is a concrete value (or identifier that equates to a concrete value) that will replace the *parameter* used in the definition of a function. In the above example, `number` is the parameter and `4` is the argument. Only the *function call* will actually run the code, using the *argument* as the input. 

```javascript
isEven(4) // 4 is the argument
```

**What is "calling" a function?**

After a function is defined, whenever it is used in your code, that is what is known as *calling* the function. This is done so with open and closed parentheses, with any *arguments* being inside of them, separated by commas (yes, you can create functions that expect more than one parameter!). 

```javascript
isEven(4) // isEven is called
```
**What is the significance of return?**

`return` is an extremely important keyword and is tied directly to the *input* and *output* relationship of a function's definition. `return`, when encountered in a function, will end that function's execution. Whatever is to the right of that `return` keyword, then, will be the value that the function will equate to when called. Think of `return` as the *output* of a function. 

For example, `isEven` has two choices for a `return` value: `true` or `false`. Depending on the *argument* passed in, that function will `return` one of those two values. That value, then can be stored in a variable and used elsewhere!

```javascript
let returnValue = isEven(4)
console.log(returnValue) //will print true
returnValue === false // will be false
```

Let's tie it all together with another exampe:


## A Summarized Example

```javascript
// a)
function doubleIt(num){
    return (num*2)
}
// b)
doubleIt(100) // output: 200
```
a) 
- is the function declaration
- is named `doubleIt`
- expects `num` as a **parameter**
- returns a value `num*2`

b)
- is the function call
- accepts `100` as the **argument**
- returns an *actual* value `200`
    


# Behavior

Functions are a little opinionated when it comes to where information must live in order to be seen.  In other words, depending on where a piece of data's *identifier** has been defined, the function may or may not know what the heck you're talking about.

This will come in the form of a **reference error**, which like it sounds, is an error based on not knowing what the program is trying to refer to. 

**identifiers* are sets of characters that are used to *identify* a variable, function or property. It's the "word(s)" you use to refer to something.  


![narrow alleyway](https://res.cloudinary.com/btvca/image/upload/c_scale,w_1080/v1599683061/alley-401540_640_gpylkt.jpg)

> NOTE: In terms of declarations, you may have encountered the `var` keywork in one form or another. In 2015, a really big change came to JavaScript that has proved `var` to be more or less obsolete. When discussing general behavior of functions in this lesson, it is under the assumption that we are using `let` in its place. 

## Narrow-minded

Take this example:

```javascript
function subtractFive(num){
    let newNum = num - 5
    return newNum
}
console.log(newNum) // will throw a reference error
```

The function above, while not very useful from an application's standpoint, does serve to demonstrate a big pain point in functions:

> *identifiers* defined *within* a function are unavailable to anything outside of it. 

This is good! Functions are only truly concerned with the bottom line: a `return` value. Whatever logic is run and whatever *identifiers* are defined, the function is handling them on a call-by-call basis, creating a new *instance* of that code being run.

The identifiers are used in context of the function, and no further. This is referred to as *scope*, and more specifically *local scope*. More on that in future lessons. For now, just remember that identifiers declared within a function will not be accessible outside of it.


## Down but not up
![jumping](https://res.cloudinary.com/btvca/image/upload/c_scale,w_1080/v1599686317/base-jump-1600668_1280_mrkmam.jpg)
**What about functions within functions?**

When a function is part of another function, the inner function has access to all of the identifiers located within it's parent function(s).

Let's take a look at the previous example, with a twist:

```javascript
function subtractFive(num){
    // the function definition 
     function timesThree(){
        return newNum * 3
    }
    // the code being run
    let newNum = num - 5
    return timesThree()

   
} 
subtractFive(10) // output: 15
```

So, what's happening here? There's a function declaration within a function declaration?

Yep!

Here, we've introduced a *second* function that has been *declared* within the first. `timesThree` is a function that has NO parameters, but when called, refers to the variable `newNum` that has been defined within view of its encasing function, `subtractFive`. 

`timesThree` can see what `newNum` is because it lives within the parent function and has a stated `return` value, `newNum * 3`. So, by calling `subtractFive` and passing `10` as an argument to it, `newNum` is defined relative to the argument 10:

```javascript
let newNum = num - 5 // when num is 10
```

And then, due to being defined within the function, `timesThree` knows what `newNum` is. So, it returns:

```javascript
newNum * 3
```
Note that the main function, `subtractFive` is returning the value that `timesThree()` equates to, and `timesThree` has been defined to `return` a number 3x `newNum`:

```javascript
// this function returns a value that is then returned by subtractFive
return timesThree()
```

**So, what's our takeaway?**

> Identifiers are visible to the functions that are *nested* within a given function, given the initial identifier has been declared inside the intiial function.

Thus the title of this section, **down, but not up**.

**But what if an identifier is declared on the top level?**

Happens all the time! These variables, functions, whatever they wind up being, are referred to as being in the *global* scope. This means they're available to anything in your program. There are benefits and downsides to this that go far beyond the scope (hah) of this article, so for now, just remember:

**Down, but not up.**

# Final Musings

Functions have a lot more to do in JavaScript than what's been covered in this article. This is not a be-all end-all resource, but rather an attempt at an easy read to get you familiarized with the language surounding functions in a smooth and simple way. 

Here are some takeaways I'd like to leave you with:

- functions can be *declared* with the `function` keyword
- *parameters* are (optional) placeholder variables used in the function *definition*/*declaration*
- *arguments* are the real values given to the function when called. They replace the *parameters*.
- *Calling* a function means running the code in its *definition* with the *arguments*.
- *identifiers* are available for use in functions only when they exist on or "below" the level at which they were defined. 

Happy coding :)

-Paul

## Exercises

The function below determines if a string is long enough to be a password

```js
function verifyPassword(string){
    if (string.length >= 8){
        return true
    } else{
        return false
    }
}
```
What changes would removing the `else` and corresponding `{}` introduce?

<details>
<summary>Answer</summary>
None at all!
</details>

<br/>

Write a function that takes 2 numbers as arguments, and returns `3 times` the larger of those 2 numbers. 

```js
threeTimesLarger(2,3) // output: 9
threeTimesLarger(20,5) // output: 60
```

<details>
<summary>Answer</summary>

```js
function threeTimesLarger(a,b){
    if(a > b){
        return 3*a
    } else{
        return 3*b
    }
}
```
</details>
<br/>
Write a function `factorial(x)` that takes a positive integer and returns the product of that integer and every other integer between it and 1.

In other words, `factorial(5)` will yield `5*4*3*2*1`, or `120`.

<details>
<summary>Answer</summary>

```js
function factorial(x){
    let result = x

    while (x>1){
        x--
        result = result * x
    }
    console.log(result)
}
```
</details>