# JavaScript

JavaScript (JS) is a lightweight, interpreted, or just-in-time compiled programming language with first-class functions. While it is most well-known as the scripting language for Web pages, many non-browser environments also use it, such as Node.js, Apache CouchDB and Adobe Acrobat. JavaScript is a prototype-based, multi-paradigm, single-threaded, dynamic language, supporting object-oriented, imperative, and declarative (e.g. functional programming) styles.

Do not worry if that definition sounds like a lot of jargon, you do not need to understand every word to start writing JavaScript. Just to unpack one term you will hear often: *single-threaded* simply means JavaScript does **one thing at a time**, like a single cook working through orders one after another instead of many cooks at once. We will not dwell on this now; it becomes relevant much later when we talk about asynchronous code.

**JavaScript** and **Java** are entirely different programming languages.

## Module Content

- [**JavaScript Pros and Cons**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-3/README.md#javascript-pros-and-cons)
- [**JavaScript Data Types**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-3/README.md#javascript-data-types)
- [**HTML and JavaScript**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-3/README.md#html-and-javascript)
- [**JavaScript Strings**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-3/README.md#strings)
- [**JavaScript Arrays**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-3/README.md#arrays)
- [**Exercises & Challenges**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-3/README.md#exercises--challenges)
- [**Sources**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-3/README.md#sources)

## JavaScript Pros and Cons

First of all, in terms of syntax, JavaScript will feel familiar to you if you already have any knowledge on C, C++ or even C#. Function (method) declaration is very similar, as well as conditional and loop statements and even the logic operators like **&&**, **==**, **!=**, etc.

One of the bases of **JavaScript** is the lack of **types**. You will probably be familiar with **types** if you have programming experience. If not, is a way to reserving memory for the information that we are going to store. Depending on the **type** of information that we are storing, is how much memory will use. Also, the **types** are used for confirming that some piece of information, is the one we are expecting. Some well-known **types** in the programming world are:

- **int** (integer, represents a number)
- **float** (precision number)
- **char** (represents a character)
- **string** (represents a group of characters)

However **JavaScript is not a typed language**. So you won't have to specify the type when declaring variables. We can take a look to some examples:

1. Example in **C** programming language.
```
void PrintMessage()
{
  int i = 0;
  char message[13] = "Hello world!";
  for (i; i < 12; i++)
  {
    printf("%c", message[i]);
  }
}
```

In here, you can see that we are using the types **int** and **char** for being explicit.

2. Example in **Python** programming language.

```
def print_message():
    message = "Hello world!"
    for i in range(len(message)):
        print(message[i], end="")
```

Python, like JavaScript, does not make us write the type of the variable, we just say `message = "Hello world!"`.

3. Example in **JavaScript**.

```
const printMessage = () => {
  let i = 0;
  let message = ['H', 'e', 'l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd', '!'];
  for (i; i < message.length; i++){
    console.log(message[i]);
  }
};
```

As you can see, we just used the word 'let' for letting **JavaScript** know that we are declaring a variable, instead of using **types**.

**Notice the important idea here:** all three programs do **the exact same thing**, go through the characters of "Hello world!" and print them one by one. Only the *spelling* of the language changes: C forces us to declare types (`int`, `char`), while Python and JavaScript let us skip them. The **logic and the ideas** (a variable holding text, a loop that walks through each character, printing each one) are the same everywhere. That is the real skill you are building: once you can *think* through a problem as steps, you can express those steps in almost any programming language, only the syntax changes.

At first sight, might seem like **JavaScript** is easier, since we do not have to define **types** for our code and at some point, it is **true**. Let's see the following example:

```
const exampleFunction = async (example) => {
  const response = await getAPIcallData(example);
  console.log(response);
};
```

In this case, we don't know what we are receiving as example, and later we don't know what information we are receiving as a response. In this case we only want to display the received data, so we don't mind about the content. As we don't mind, we don't have to declare any explicit type so we could say this is *less work*. **JavaScript** give us this amount of freedom. But in my personal experience this is also its ***worst feature***. Since by not knowing the type, our application might result in total chaos.

## JavaScript Data Types

We just said JavaScript does not force us to *declare* a type. But the types still **exist**, JavaScript simply figures them out for us based on the value we give a variable. So it is worth knowing the main ones you will meet.

A helpful way to picture a variable: think of it as a **labeled box in memory**. The **label** is the variable name, and inside the box we store a **value**. The *type* just tells us what kind of thing is in the box (a number? some text? a yes/no?), which is roughly how much and what shape of memory it needs.

```
   name ─┐            age ─┐            isStudent ─┐
         ▼                  ▼                        ▼
   ┌───────────┐      ┌───────────┐          ┌───────────┐
   │  "Anna"   │      │    30     │          │   true    │
   └───────────┘      └───────────┘          └───────────┘
     (string)           (number)              (boolean)
```

The most common types in JavaScript are:

- **string** → text, always written in quotes. `"Anna"`, `'hello'`, `` `hi` ``.
- **number** → any number, whole or decimal. `30`, `3.14`, `-7`. (Unlike some languages, JavaScript does not separate `int` and `float`, a number is just a number.)
- **boolean** → a simple yes/no value: `true` or `false`. Perfect for questions like "is the user logged in?".
- **undefined** → a box that exists but has **nothing** put in it yet.
- **null** → an *intentional* "empty on purpose" value, we deliberately say "there is nothing here".
- **array** → an **ordered list** of values in a single box, written with `[ ]`. `["red", "green", "blue"]`. (We dedicate a whole section to these below.)
- **object** → a box that groups **related values together with labels**, written with `{ }`. `{ name: "Anna", age: 30 }`.

**Example:**

```
let name = "Anna";        // string
let age = 30;             // number
let isStudent = true;     // boolean
let favoriteColors = ["red", "green"]; // array
let person = { name: "Anna", age: 30 }; // object
```

Notice we never wrote the type, we just assigned a value and JavaScript understood the rest. There is even a built-in way to *ask* JavaScript what type a value is, using `typeof`:

```
console.log(typeof "Anna");  // "string"
console.log(typeof 30);      // "number"
console.log(typeof true);    // "boolean"
```

Do not feel you must memorize all of this now, you will get comfortable with each type as we use them. The key takeaway: even in a "typeless" language, values still have types, and knowing them helps you avoid the "total chaos" we warned about above.

## HTML and JavaScript

Going back to our last lessons, we have seen two main concepts about web development:

1. **HTML** (page structure, information organization).
2. **CSS** (styling to each HTML element).

However, when we think about **web development** we know that for most of the *useful* apps, these are not the only features that we need. We can picture often **forms** these places where we type and submit information. Or for example, when we think about a social applications, we can notice that there are many interactions that define different behaviours: liking or sharing a post, storing user information, uploading media and some others. This kind of things can't be done exclusively with **HTML and CSS**, which is why we need a **scripting language (JavaScript)**.

So far, in the examples that we have seen that use **HTML and CSS** we use **static data** (data that does not change), which when we think about a web application is not the only thing that we need. For example, we might want to show the user name or user picture.

**Previous HTML and CSS example:**

```
<div style="background-color: red">
  <p>Some cool text</p>
</div>  
```

![static-example](https://user-images.githubusercontent.com/58167190/180062050-f7697bb2-1acc-4973-9172-f94d943ea22f.png)

What about showing a different text from *Some cool text*? We should use **JavaScript**. 

The first thing that we need to work with **JavaScript** in these exercises, is to create a **JavaScript** (`.js`) file. Let's go to our favorite **editor** for working with **JavaScript**. Let's use [**Code Sandbox**](https://codesandbox.io) for our example. Let's create a new folder called `js` and inside of it, lets create a `script.js` (this example assumes that you already have your HTML file).

![image](https://user-images.githubusercontent.com/58167190/180932184-7d693b1d-0ff4-4a0f-9a11-3ed65827f0bc.png)

**`index.html`**

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>JS</title>
    <!-- Call a program -->
    <script src="js/script.js"></script>
  </head>
  <body onload="main()"></body>
</html>
```

**`script.js`**

```
// Function for returning a full name from a first name
// and a last name.
const getFullName = (firstName, lastName) => {
  return firstName + " " + lastName;
};

// Main function for calling another functions
const main = () => {
  getFullName("John", "Doe");
};
```

Notice that this `script.js` does **not** call `main()` at the bottom. That is because the HTML already runs it through `<body onload="main()">`, which waits until the page (the `<body>` and its contents) has loaded before executing. This matters: because the `<script>` is in the `<head>`, it is read **before** the `<body>` exists. If we called `main()` directly at the bottom of the script and that function tried to read an HTML element (as we will do later), the element would not exist yet and the program would fail. Letting `onload` trigger `main()` avoids that problem.

Firstly, in the **HTML** file you might have noticed a new **tag** **`<script>`**. The first thing to know, is that this tag is not *self-closing*, this means that we **could not** make something like this: **`<script />`**. Also is important for you to know, that we could actually write our **JavaScript** code inside of the `<script>` tag. However, **it is not the recommended way to proceed**. Just to clarify, here is an example:

```
<script>
const getFullName = (firstName, lastName) => {
  return firstName + " " + lastName;
};

getFullName("John", "Doe");
</script>
```

This would be technically correct, and the browser would recognize it. But as said **is not the best practice**. This is the reason about why we use the property `src` in the `<script>` tag as in the `.html` example (`<script src="js/script.js"></script>`) which tells the browser use the file `script.js`, located in the folder `js` as the script for this file. In most of the sources that you might find, it is **recommended to isolate the scripts from the html**.

Now, you may have noticed that the **`<body>`** tag has an **`onload`** property. This property tells the browser to load the mentioned function as soon as the body loads, so that is the first thing that we would execute. In the example that is referenced, we use the function `main()` in the **`onload`** tag. That means that main() is the first thing to be executed inside the `script.js` file. As we can see, our `main()` function calls the `getFullName()` function, that receives two parameters and return them to the place where is called.

Is very likely that if you have programmed before, you might have used *printing functions*, like `printf()` for `C`, `System.WriteLine()` in `C#`, `print()` in `Python` and so on. These printing functions allow us to show in the screen something that we want, like a message, options or the values of different variables. So *JavaScript* also has its printing function which is:

`console.log()`

Some of the greatest features of this function in `JavaScript` is that receives virtually anything as a parameter.

Let's put this in practice.

In our `script.js` file we will perform some modifications.

```
const getFullName = (firstName, lastName) => {
  return firstName + " " + lastName;
};

// Main function for calling another functions
const main = () => {
  let fullName = "";
  fullName = getFullName("John", "Doe");
  console.log(fullName);
};
```

With these modifications we are doing the following:

1. Create a `fullName` variable initialized to an empty string (`""`).
2. Assigning the response of the `getFullName()` function to this variable by sending two parameters (`"John", "Doe"`).
3. Showing in the browser console the value of the `fullName` variable.

Let's see how does this look in our **CodeSandbox** project:

![image](https://user-images.githubusercontent.com/58167190/181112162-de4925b1-45ac-48b2-8a51-f073516472c8.png)

You might be wondering where is the output of our function.

If you go down in the UI of **CodeSandbox**, you will find a **console** button. Just click and bingo!

![image](https://user-images.githubusercontent.com/58167190/181112448-af0a3fe0-7b40-45bc-8b1e-f43229bc3d3a.png)

In a regular browser, like **Chrome**, **Firefox** or **Edge** you can show the content of this console by pressing **`F12`** on your keyboard. Of course, this console is way more robust and have many features, but still, can be used for testing purposes.

![image](https://user-images.githubusercontent.com/58167190/181112734-843a4dd4-f361-48dd-8135-342daa258899.png)

Example of **Microsoft's Chromium Edge** console.

Okay, we have already used some functions in here, but... **What are functions?**

**Functions** are a special programming structure meant to perform a defined operation or task. We used our `main()` and `getFullName()` function, from which objectives were to call other functions and printing and returning a full name from a first name and a last name, respectively.

In **JavaScript**, functions are defined in two different ways:

1. By the **arrow function `() => {}`** notation.
2. By using the reserved word **function**.

The syntax of the function would look like this:

```
const myNewFunction = (myParameter1, myParameter2, ..., myParameterN) => {
  // Content of the function
  // Perhaps a return
};
```

Or probably like this:

```
function myNewFunction (myParameter1, myParameter2, ..., myParameterN) {
  // Content of the function
  // Perhaps a return
};
```

If well both ways are correct, at least for this course, we will be using the **arrow function `() => {}`** notation.

Did you notice the slashes (`//`) so far in the code? As in many different programming languages, we can use some symbols to indicate in our program that some section of the code should not be taken as statements. Probably we just want to document, take notes or say something useful about our code. For that matter, in **JavaScript**, the `//` and `/**/` symbols are used.

**Examples:**

```
// This is a test function
const myFunction = (text) => {
  return text + " another text";
};
```

```
/*
 * Function test meant for performing some operation. Please
 * notice that this is an option for multiline commentaries
 * inside of the code.
 */
const myFunction = (text) => {
  return text + " another text";
};
```

As shown in the examples, we called our **main** function `main()`, trying to emulate a main function that is used in other programming language and having that name for clarity. However, the function can take any name that we define.

```
const thisIsADumbNameFunctionThatIsNotRelatedToItsFunctionality = (number1, number2) => {
  return number1 + number2;
};
```

Of course makes any sense to call a function with a different name from one that describes functionality, so correcting the example, we would have:

```
const numberAddition = (number1, number2) => {
  return number1 + number2;
};
```

As already said, **JavaScript** give us a lot of freedom when coding, so also, we can call the **received parameters** of the function any way we want. Using the last example:

```
const numberAddition = (ball1, yellowJacketAndJohn) => {
  return ball1 + yellowJacketAndJohn;
};
```

But again, for clearance and to follow the best practice, the best choice is to give the parameters names that are actually related to their use in a given function.

Let's quickly try to change our original HTML + **JavaScript** example a little and test it. We will be using the `numberAddition()` example function. in our **`script.js`** example we will have:

```
const getFullName = (firstName, lastName) => {
  return firstName + " " + lastName;
};

const numberAddition = (number1, number2) => {
  return number1 + number2;
};

// Main function for calling another functions
const main = () => {
  let additionResult = 0;
  additionResult = numberAddition(7, 12);
  console.log(additionResult);
};

main();
```

Our console now should show us the following:

![image](https://user-images.githubusercontent.com/58167190/181134261-009dae52-b52c-4fe9-9200-6be2d1922306.png)

Also notice, that for these examples we are using variables for being clear about the examples, however, we could get the same output without even having to declare a variable by simply doing:

```
const getFullName = (firstName, lastName) => {
  return firstName + " " + lastName;
};

const numberAddition = (number1, number2) => {
  return number1 + number2;
};

// Main function for calling another functions
const main = () => {
  console.log(numberAddition(7, 12));
};

main();
```

With this last implementation, we are *"chaining functions"*. This means, using the result of a function, as a parameter for a different function. This can be simply done, but remember that for this to work **we have to keep track of the types that we are using**.

So far so good, right? Right now we are experts on creating different functionalities for our **JavaScript** code and we perfectly understand how to **call functions**, **send parameters** and **printing the results**. But...

![image](https://user-images.githubusercontent.com/58167190/181134772-54d71e0b-20c9-41be-94d5-2d1f7bc6a92a.png)

Of course... Whats does anything of this has to do with **HTML and CSS**?

That's a great question. So far, we tell **HTML** to load and execute a script. The script does an isolated task and that's it. But when we think about a decent website, the user interactions usually represents specific behaviour like increasing a like count, changing the site theme, moving between pages and so on. Now, our next step is to **Program JavaScript for interacting with HTML**.

The great magic word for this is **`document.getElementById()`**, which gets a reference to an HTML element through its id. But... What is an id?

Well, in HTML, the tags have the **`id`** attribute, that as the name says, is used to identify each element. An **id must be unique**: no two elements on the same page should share the same id. Reusing an id is invalid HTML and leads to unpredictable results (for example, `document.getElementById` will only ever hand you back one of them). If you need to label several elements together, use a **class** instead (as we saw in the CSS lesson). This **id** is recommended to be related to the element itself. For example **`id=awesome-header-1`**. Let's see an example:

```
<h1 id="header1">Hi there!</h1>
```

What about if we would like to **programmatically** change the children of a HTML tag? In the last example we can see that `Hi there` is the children of h1. Like we said, this is static. Let's make the children change, based on the **JavaScript** program.

```
const main = () => {
  let header1 = document.getElementById("header1");
  header1.innerHTML = "Bonjour";
};
```

In this piece of code, we are assigning the content of the HTML tag with the **identifier** `header1` to the *`header1`* variable. Now, the **`header1`** variable, is like an HTML element, with all of its properties, but as a **program entity**. Now is not only a tag, but an object in the memory containing the information of such tag. In this order of ideas, *`innerHTML`* represents the children of the HTML tag. So, by doing ` header1.innerHTML = "Bonjour";` we are telling our browser to assign `"Bonjour"` as the children of the `<h1>` tag.

If we take a look to our **CodeSandbox** browser, we should be seeing something like the following:

![image](https://user-images.githubusercontent.com/58167190/181389713-f06879fe-dc43-464e-b5a3-8915db16d393.png)

Great! Now we are capable of affecting the content of the HTML based on our **JavaScript** program. But... What about CSS? Well, in a similar manner, we can change the style property of any element **programmatically**. Let's take a look:

```
const main = () => {
  let header1 = document.getElementById("header1");
  header1.innerHTML = "Bonjour";
  header1.style.backgroundColor = "blue";
};
```

In this example, just with accessing the `.style.backgroundColor`, we are capable of changing such property in the HTML output through **JavaScript**. This same logic can be applied to basically any property of the style. Now, our output should look like this:

![image](https://user-images.githubusercontent.com/58167190/181390224-065da5d3-fff5-482e-ae38-57513ecab302.png)

Now... Let's make this more interesting. As I have been saying, in a **professional application** the user interactions are those that make things happen. So practically one of the most common interactions, is a **click**. And... How do we perform a click? Well, for that, we need a button, which is declared in **HTML** through the `<button>` tag. Let's go coding.

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>JavaScript Example</title>
    <script src="js/script.js"></script>
  </head>
  <body onload="main()">
    <h1 id="header1"></h1>
    <button onclick="handleOnClick()" id="magic-button">Magic Click!</button>
  </body>
</html>
```

Our **HTML** should look like this now. Please notice the use of `<button>` tag, that has as children the `string` "Magic Click!". Also, this tag has a `onclick` property, which requires a function that is going to be triggered anytime the **event is detected**. For this to make sense, let's change our **JavaScript** too.

```
var headerColor = "red";

const handleOnClick = () => {
  let header1 = document.getElementById("header1");
  if (headerColor === "red") {
    headerColor = "blue";
  } else {
    headerColor = "red";
  }
  header1.style.backgroundColor = headerColor;
};

const main = () => {
  let header1 = document.getElementById("header1");
  header1.innerHTML = "Bonjour";
  header1.style.backgroundColor = "blue";
};
```

In here, we defined the **`handleOnClick()`** function, which receives any parameter. It makes a reference to our header1 element (`<h1>`) now, it use a **conditional statement**. What is this? Nothing but a way to control the flow of our program. It basically says *'if this condition is met, then, do this'*. So in here, we are saying, if the `headerColor` is equal to `"red"`, change the value of the `headerColor` variable to `"blue"`. But we also can see an **`else`** statement which controls what to do if the **`if`** condition is not met. In this case, we would be saying in the whole expression *'if headerColor is equal to red, change it to blue. Otherwise, change it to red'*. This means, that every time the user clicks on the button, the color will change. 

#### Why `===` and not `=`?

You may have noticed we wrote `headerColor === "red"` with **three** equal signs, not one. This trips up almost every beginner, so let's clear it up:

- **`=`** (one equals) **assigns** a value. `headerColor = "red"` means *"put the text 'red' into the variable `headerColor`"*.
- **`===`** (three equals) **compares** two values and answers `true` or `false`. `headerColor === "red"` means *"is `headerColor` equal to 'red'?"*.

So inside an `if (...)` we almost always want `===`, because we are **asking a question**, not assigning.

But what about `==` (two equals)? It also compares, but it is more permissive: before comparing, it will quietly **convert** the values to the same type. That sounds helpful, but it causes surprising results:

```
console.log(5 === "5"); // false  -> a number is NOT the same as a text "5"
console.log(5 == "5");  // true   -> == converts "5" into 5 first, then compares
```

The `==` version says a number and a piece of text are "equal", which is rarely what you mean and is a classic source of bugs. **Rule of thumb for this course: always use `===` (and `!==` for "not equal").** It compares both the value *and* the type, so there are no surprises.

Also notice that at the top of our `js` file now we have a variable defined through `var`. By using `var` we are indicating to the browser that this variable can be accessed in many places and not only the place where is defined. Also notice that this variable, `headerColor` is outside of any function, which turns it into a **global variable**. A **global variable** is a special type of variable that can be accessed in practically any place. By following the last steps, we should have something like the following:

#### A word about `var` (and hoisting)

You may be wondering why we suddenly used `var` here instead of `let` or `const`. The short version:

- **`const`** → a variable you will **not** reassign.
- **`let`** → a variable you **may** reassign later.
- **`var`** → an older way of declaring variables. It is **function-scoped** (it lives in the whole function, not just the block it was written in) and it is **hoisted**. Modern code usually prefers `let` and `const`, but `var` still has valid uses when you specifically want that hoisting / function-scope behavior.

**So what is "hoisting"?** (Explained for babies 🍼) Imagine you are reading a recipe out loud, and before you even start cooking, someone quietly writes down the *names* of all the ingredients you are going to mention, so those names already "exist" from the very first line. JavaScript does something similar: before running your code, it takes all the `var` declarations and **moves their names to the top** of the function. The *name* exists early (with a temporary value of `undefined`), even though the *value* is only assigned later where you actually wrote it.

Let's imagine we want to do this:

```
const main = () => {
  console.log(message); // This does NOT crash. It prints: undefined
  var message = "Hello!";
  console.log(message); // Now it prints: "Hello!"
};

main();
```

The first `console.log` does not error out, even though `message` seems to be declared *after* it. That is hoisting at work: JavaScript already knew the *name* `message` existed (as `undefined`) from the top of the function. This "use it before you declare it" tolerance is a behavior of `var`, and it is the kind of thing `var` allows that `let`/`const` do not (with `let`/`const`, reading the variable before its declaration line throws an error instead). So when you *specifically* want that flexible, hoisted, function-scoped behavior, `var` is the tool for it.

> **Note:** Hoisting is a **mid/advanced topic** and is **not mandatory** for this course. You can safely stick to `let` and `const` for everything and be perfectly fine. We mention it only so the `var` above does not look like magic. If you want to dive deeper, see Mozilla's explanation: [**MDN — Hoisting**](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting).

Before the user click:

![image](https://user-images.githubusercontent.com/58167190/181391669-f58fd766-0e8d-4278-a18c-4c9c0560d9dc.png)

After the user click:

![image](https://user-images.githubusercontent.com/58167190/181391694-a0be5213-dd94-4d76-8f5e-628a8a3fcc45.png)

And clicking again:

![image](https://user-images.githubusercontent.com/58167190/181391738-92b92d65-5c2f-48c3-a888-409eea7fb661.png)

So with this, now we have reviewed the concepts together: **HTML**, **JavaScript** and **CSS**.

## Strings

The **JavaScript** **String** object is used to represent a sequence of characters (**e.g.**: `a`, `c`, `2`, etc). These are useful for holding data that can be represented as **text**. 

### String creation

We have several ways to **create strings**:

```
const stringA = "I am a string";
const stringB = 'I am another string';
const stringC = `I am yet another string`. // Template literal
const stringD = new String("I am a string object");
```

### Character access

As the strings are sequences of characters, we might want to access individual characters from a single string. To do so, we have two choices:

- `"I am a string".charAt(2); // Which returns 'a'`
- `"I am a string"[2]; // Which returns 'a'`

### Main Methods

**JavaScript** has built-in methods for manipulating strings which allow us to achieve several things when dealing with texts. Here we review some of the most common and widely-used ones.

#### concat

The `concat()` methods **concatenates** all the passed strings and returns a new one. In other words, it merges the passed strings into a different one.

**Example**:

```
const stringA = "Hello";
const stringB = "World!";
const spacedString = " ";

const stringC = stringA.concat(spacedString, stringB);
console.log(stringC); // Expected output: "Hello World!"
```

#### includes

The `includes()` method performs a **case-sensitive** search to determine whether a given string can be found within the string that invokes `includes()` method. This method return a `boolean` (`true` or `false`).

**Example**:

```
const text = "What does the fox say?";

const searchTerm = "fox";

console.log(text.includes(searchTerm)); // The output should be `true`

```

### replace

The `replace()` method of a string returns a new string with one, some or all matches of a **pattern** replaced by a **replacement**, where the **pattern** can be either a string or a **regular expression**. If a **string** is used instead of a regular expression, only **the first match** will be replaced. The original string keeps **unaltered**.

**Example**: 

```
const text = "Anakin Skywalker is very powerful, but Anakin Skywalker is not a master";

console.log(text.replace("Anakin Skywalker", "Darth Vader")); // Expected output: "Darth Vader is very powerful, but Anakin Skywalker is not a master"

console.log(text.replace(/Anakin Skywalker/g, "Darth Vader")); // Expected output: "Darth Vader is very powerful, but Darth Vader is not a master"
```

## Arrays

An **array** is an **ordered list** of values stored in a single variable. Instead of creating one box per value, we keep many values lined up inside one box, each in its own numbered slot. We write arrays with **square brackets** `[ ]`, separating the values with commas.

```
const colors = ["red", "green", "blue"];
```

You actually already saw an array earlier in this lesson, remember the `message` variable full of single characters? That was an array too.

### Accessing items (indexes)

Each item has a position number called its **index**. A very important detail: **indexes start at `0`, not `1`**. So the first item is at index `0`, the second at index `1`, and so on.

```
const colors = ["red", "green", "blue"];

console.log(colors[0]); // "red"
console.log(colors[1]); // "green"
console.log(colors[2]); // "blue"
```

A quick picture:

```
   index:     0         1         2
           ┌───────┬─────────┬────────┐
   colors: │ "red" │ "green" │ "blue" │
           └───────┴─────────┴────────┘
```

### How many items? (`length`)

Every array knows its own size through its `length` **property** (notice: no parentheses, it is not a function):

```
const colors = ["red", "green", "blue"];
console.log(colors.length); // 3
```

### Some common array methods

Just like strings, arrays come with built-in helpers. A few you will use constantly:

- **`push`** → adds an item to the **end** of the array.

```
const colors = ["red", "green"];
colors.push("blue");
console.log(colors); // ["red", "green", "blue"]
```

- **`pop`** → removes and returns the **last** item.

```
const colors = ["red", "green", "blue"];
const removed = colors.pop();
console.log(removed); // "blue"
console.log(colors);  // ["red", "green"]
```

- **`includes`** → asks whether a value is in the array, returning `true` or `false`.

```
const colors = ["red", "green", "blue"];
console.log(colors.includes("green")); // true
console.log(colors.includes("pink"));  // false
```

### Walking through an array (loop)

Because an array is an ordered list, we often want to visit each item one by one. We can reuse the loop idea from the very beginning of this lesson, going from index `0` up to `length - 1`:

```
const colors = ["red", "green", "blue"];

for (let i = 0; i < colors.length; i++) {
  console.log(colors[i]);
}
// Prints: red, then green, then blue
```

Arrays are everywhere in real applications: a list of products, the messages in a chat, the songs in a playlist, all naturally live inside arrays.

## Module Activity

We are going to build a basic functional calculator with HTML + CSS and JavaScript. It must have the addition, subtraction, division and multiplication capabilities. Free layout.

Remember the calculator you designed back in the **CSS lesson** (lesson 2)? That one only *looked* like a calculator, the buttons did nothing when clicked. Now is the moment to bring it to life: reuse that same HTML + CSS layout and, with everything you learned in this lesson (`getElementById`, events like `onclick`, functions and conditionals), make the buttons actually perform the math. In other words, we are turning the *static* calculator from lesson 2 into a *working* one.

## Exercises & Challenges

Below is a collection of exercises drawn from the live sessions, grouped by topic and ordered from easier to harder. Try each one **before** opening the solution, that struggle is where the learning happens.

### Strings

#### Reverse a string

Write a function that takes a string and returns it reversed. `reverseString("hello")` should return `"olleh"`.

**Hint.** `split`, `reverse`, and `join` turn this into a one-liner.

<details>
<summary>Solution</summary>

```js
const reverseString = (input) => input.split("").reverse().join("");

console.log(reverseString("hello")); // "olleh"
```
</details>

#### Capitalize the first letter

Return a word with its first letter capitalized. `capitalizeWord("javascript")` should return `"Javascript"`.

<details>
<summary>Solution</summary>

```js
const capitalizeWord = (input) => {
  const firstLetter = input.charAt(0).toUpperCase();
  const rest = input.slice(1);
  return firstLetter.concat(rest);
};

console.log(capitalizeWord("javascript")); // "Javascript"
```
</details>

#### Censor a bad word

Write a function that replaces every occurrence of a forbidden word in a message with `"***"`. Make it case-insensitive.

**Hint.** `replace` with a regular expression and the `gi` flags (global + insensitive) replaces *all* matches.

<details>
<summary>Solution</summary>

```js
const censorMessage = (message, badWord) => {
  const pattern = new RegExp(badWord, "gi");
  return message.replace(pattern, "***");
};

console.log(censorMessage("You are a Sith and a Sith again", "sith"));
// "You are a *** and a *** again"
```
</details>

#### Enforce a tweet character limit

Given a message, return `true` if it is within a 280-character limit, `false` otherwise.

<details>
<summary>Solution</summary>

```js
const fitsInTweet = (message) => message.length <= 280;

console.log(fitsInTweet("Hello there!")); // true
```
</details>

#### Trim surrounding spaces

A username came in with spaces at the start and end. Remove them.

<details>
<summary>Solution</summary>

```js
const cleanUsername = (input) => input.trim();

console.log(cleanUsername("   luke_skywalker   ")); // "luke_skywalker"
```
</details>

#### Palindrome checker

Write a function that returns `true` if a phrase reads the same forwards and backwards, ignoring case and spaces. Test it with `"Anita lava la tina"`.

<details>
<summary>Solution</summary>

```js
const isPalindrome = (phrase) => {
  const clean = phrase.toLowerCase().replace(/ /g, "");
  const reversed = clean.split("").reverse().join("");
  return clean === reversed;
};

console.log(isPalindrome("Anita lava la tina")); // true
console.log(isPalindrome("hello"));              // false
```
</details>

### Operators

#### Guard against division by zero

Write a function that divides two numbers but never lets the program crash on a zero divisor. Use `try` / `catch` / `finally`.

<details>
<summary>Solution</summary>

```js
const safeDivide = (a, b) => {
  try {
    if (b === 0) throw new Error("You can't divide by zero");
    return a / b;
  } catch (error) {
    console.log(error.message);
    return null;
  } finally {
    console.log("Operation completed");
  }
};

console.log(safeDivide(10, 2)); // 5
console.log(safeDivide(10, 0)); // logs the error, returns null
```
</details>

### Functions

#### Area of a circle

Write a function that returns the area of a circle given its radius. Use `Math.PI` and `Math.pow`.

<details>
<summary>Solution</summary>

```js
const getCircleArea = (radius) => Math.PI * Math.pow(radius, 2);

console.log(getCircleArea(2)); // 12.566...
```
</details>

#### Sum two fractions (compose functions)

Add two fractions `n1/d1 + n2/d2` and return an object with the resulting `numerator`, `denominator`, and `decimal`. Reject a zero denominator. Design the pseudocode first: `denominator = d1 * d2`, `numerator = n1*d2 + n2*d1`.

<details>
<summary>Solution</summary>

```js
const sumFractions = (n1, d1, n2, d2) => {
  if (d1 === 0 || d2 === 0) {
    console.log("You can't divide by zero");
    return;
  }
  const numerator = n1 * d2 + n2 * d1;
  const denominator = d1 * d2;
  return { numerator, denominator, decimal: numerator / denominator };
};

const r = sumFractions(3, 4, 7, 9);
console.log(`${r.numerator}/${r.denominator} = ${r.decimal}`);
// "55/36 = 1.5277777777777777"
```
</details>

<!-- repaired: the recorded quadratic-equation exercise never reached a correct result on camera (operands mislabeled, then abandoned). This is a clean version preserving the intent (quadratic formula with Math.pow/Math.sqrt returning both roots). -->
#### Solve a quadratic equation (both roots)

Given `a`, `b`, `c`, return both roots of `ax² + bx + c = 0` using the quadratic formula.

<details>
<summary>Solution</summary>

```js
const solveQuadratic = (a, b, c) => {
  const discriminant = Math.pow(b, 2) - 4 * a * c;
  if (discriminant < 0) return "No real roots";
  const root = Math.sqrt(discriminant);
  return {
    x1: (-b + root) / (2 * a),
    x2: (-b - root) / (2 * a),
  };
};

console.log(solveQuadratic(1, -3, 2)); // { x1: 2, x2: 1 }
```
</details>

### Arrays

#### Double every value

Given an array of numbers, return a new array with each value doubled, using `map`.

<details>
<summary>Solution</summary>

```js
const doubleValues = (nums) => nums.map((n) => n * 2);

console.log(doubleValues([1, 2, 3, 4])); // [2, 4, 6, 8]
```
</details>

#### Word lengths

Given an array of words, return an array with the length of each word.

<details>
<summary>Solution</summary>

```js
const wordLengths = (words) => words.map((word) => word.length);

console.log(wordLengths(["apple", "cat", "banana"])); // [5, 3, 6]
```
</details>

#### Sum the elements of an array

Return the sum of an array's numeric elements using `forEach` and an accumulator.

<details>
<summary>Solution</summary>

```js
const arraySum = (array) => {
  let sum = 0;
  array.forEach((element) => {
    sum = sum + element;
  });
  return sum;
};

console.log(arraySum([1, 2, 3])); // 6
```
</details>

### Objects

#### Access nested properties

Build a `user` object containing a nested `social` object (e.g. an `instagram` object with a `followers` count), then read the follower count with dot notation.

<details>
<summary>Solution</summary>

```js
const user = {
  name: "Luke",
  social: {
    instagram: { followers: 1200, following: 421 },
  },
};

console.log(user.social.instagram.followers); // 1200
```
</details>

#### Copy an object safely with spread

Objects assigned directly are copied *by reference*, mutating the copy mutates the original. Prove it, then fix it with the spread operator so a customized copy leaves the default untouched.

<details>
<summary>Solution</summary>

```js
const defaultCharacter = { level: 1, class: "warrior", mana: 0 };

const customCharacter = { ...defaultCharacter };
customCharacter.class = "wizard";

console.log(customCharacter.class);  // "wizard"
console.log(defaultCharacter.class); // "warrior" (unchanged)
```
</details>

#### Omit a property with destructuring

You are about to store a new user in the database but must never persist their `password`. Build a copy that excludes it.

**Hint.** `const { password, ...rest } = user;` pulls out `password` and gathers everything else into `rest`.

<details>
<summary>Solution</summary>

```js
const newUser = {
  id: 1234,
  name: "Luke",
  email: "luke@rebels.org",
  password: "abc1234",
};

const { password, ...userToStore } = newUser;

console.log(userToStore); // no password property
```
</details>

#### Object.keys / values / entries

Given an object, get (1) its property names, (2) its values, and (3) its `[key, value]` pairs.

<details>
<summary>Solution</summary>

```js
const user = { id: 1234, name: "Luke", email: "luke@rebels.org" };

console.log(Object.keys(user));    // ["id", "name", "email"]
console.log(Object.values(user));  // [1234, "Luke", "luke@rebels.org"]
console.log(Object.entries(user)); // [["id",1234],["name","Luke"],["email","luke@rebels.org"]]
```
</details>

### Algorithms & mini-projects

#### Repeat a string N times

Write a function that returns a string repeated `n` times. `repeatString("abc", 3)` → `"abcabcabc"`.

<!-- repaired: the live solution got stuck and was taken home as homework; this is a clean version of the demonstrated "map over a dummy array" approach. -->
<details>
<summary>Solution</summary>

```js
const repeatString = (input, n) =>
  new Array(n).fill(0).map(() => input).join("");

console.log(repeatString("abc", 3)); // "abcabcabc"
```
</details>

#### Time-of-day greeting

Return `"day"`, `"afternoon"`, or `"night"` based on the current hour (24-hour clock), using conditionals and the `Date` object.

<!-- repaired: the recorded hour boundaries overlapped/left gaps; these ranges are clean and gap-free while preserving the day/afternoon/night intent. -->
<details>
<summary>Solution</summary>

```js
const getGreeting = () => {
  const hour = new Date().getHours();
  if (hour >= 5 && hour < 12) return "day";
  if (hour >= 12 && hour < 20) return "afternoon";
  return "night";
};

console.log(`Have a great ${getGreeting()}!`);
```
</details>

#### Calculator building blocks

The Module Activity above asks you to build a working calculator. These two functions are the core building blocks, note the **divide-and-conquer** pattern: one function does the math, another builds the message.

<details>
<summary>Solution</summary>

```js
const getSum = (n1, n2) => n1 + n2;

const printResult = (n1, n2) => {
  const sum = getSum(n1, n2);
  return `The operation is ${n1} + ${n2}. The result is ${sum}`;
};

console.log(printResult(5, 4)); // "The operation is 5 + 4. The result is 9"
```
</details>

## Sources

- [**Mozilla**](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
