# JavaScript

JavaScript (JS) is a lightweight, interpreted, or just-in-time compiled programming language with first-class functions. While it is most well-known as the scripting language for Web pages, many non-browser environments also use it, such as Node.js, Apache CouchDB and Adobe Acrobat. JavaScript is a prototype-based, multi-paradigm, single-threaded, dynamic language, supporting object-oriented, imperative, and declarative (e.g. functional programming) styles.

**JavaScript** and **Java** are entirely different programming languages.

## Module Content

- [**JavaScript Pros and Cons**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-3/README.md#javascript-pros-and-cons)
- [**HTML and JavaScript**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-3/README.md#html-and-javascript)
- [**Sources**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-3/README.md#sources)

## JavaScript Pros and Cons

First of all, in terms of syntaxis, JavaScript will feel familiar to you if you already have any knowledge on C, C++ or even C#. Function (method) declaration is very similar, as well as conditional and loop statements and even the logic operators like **&&**, **==**, **!=**, etc.

One of the bases of **JavaScritpt** is the lack of **types**. You will probably be familiar with **types** if you have programming experience. If not, is a way to reserving memory for the information that we are going to store. Depending on the **type** of information that we are storing, is how much memory will use. Also, the **types** are used for confirming that some piece of information, is the one we are expecting. Some well-known **types** in the programming world are:

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
  for (i; i < 14; i++)
  {
    printf(message[i]);
  }
}
```

In here, you can see that we are using the types **int** and **char** for being explicit.

2. Example in **JavaScript**.

```
const printMessage = () => {
  let i = 0;
  let message = ['H', 'e', 'l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd', '!'];
  for (i; i < message.length(); i++){
    console.log(message[i]);
  }
};
```

As you can see, we just used the word 'let' for letting **JavaScript** know that we are declaring a variable, instead of using **types**.

At first sight, might seem like **JavaScript** is easier, since we do not have to define **types** for our code and at some point, it is **true**. Let's see the following example:

```
const exampleFunction = async (example) => {
  const response = await getAPIcallData(example);
  console.log(response);
}
```

In this case, we don't know what we are receiving as example, and later we don't know what information we are receiving as a response. In this case we only want to display the received data, so we don't mind about the content. As we don't mind, we don't have to declare any explicit type so we could say this is *less work*. **JavaScript** give us this amount of freedom. But in my personal experience this is also its ***worst feature***. Since by not knowing the type, our application might result in total chaos.

## HTML and JavaScript

Going back to our last lessons, we have seen two main concepts about web development:

1. **HTML** (page structure, information organization).
2. **CSS** (styling to each HTML element).

However, when we think about **web development** we know that for most of the *useful* apps, these are not the only features that we need. We can picture often **forms** these places where we type and submit information. Or for example, when we think about a social applications, we can notice that there are many interactions that define different behaviours: liking or sharing a post, storaging user information, uploading media and some others. This kind of things can't be done exclusively with **HTML and CSS**, which is why we need a **scripting language (JavaScript)**.

So far, in the examples that we have seen that use **HTML and CSS** we use **static data** (data that does not change), which when we think about a web application is not the only thing that we need. For example, we might want to show the user name or user picture.

**Previous HTML and CSS example:**

```
<div style="background-color: red">
  <text>Some cool text</text>
</div>  
```

![static-example](https://user-images.githubusercontent.com/58167190/180062050-f7697bb2-1acc-4973-9172-f94d943ea22f.png)

What about showing a different text from *Some cool text*? We should use **JavaScript**. 

The first thing that we need to work with **JavaScript** in these exercises, is to create a **JavaScript** (`.js`) file. Let's go to our favorite **editor** for working with **JavaScript**. Let's use [**Code Sandbox**](https://codesandbox.io) for our example. Let's create a new folder called `js` and inside of it, lets create a `script.js` (this example assumpts that you already have your HTML file).

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

main();
```

Firstly, in the **HTML** file you might have noticed a new **tag** **`<script>`**. The first think to know, is that this tag is not *self-closing*, this means that we **could not** make something like this: **`<script />`**. Also is important for you to know, that we could actually write our **JavaScript** code inside of the `<script>` tag. However, **it is not the recommended way to proceed**. Just to clarify, here is an example:

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

main();
```

With these modifications we are doing the following:

1. Create a `fullName` variable initialized to an empty string (`""`).
2. Assigning the responde of the `getFullName()` function to this variable by sending two parameters (`"John", "Doe"`).
3. Showing in the browser console the value of the `fullName` variable.

Let's see how does this look in our **CodeSandbox** project:

![image](https://user-images.githubusercontent.com/58167190/181112162-de4925b1-45ac-48b2-8a51-f073516472c8.png)

You might be wondering where is the output of our function.

If you go down in the UI of **CodeSanbox**, you will find a **console** button. Just click and bingo!

![image](https://user-images.githubusercontent.com/58167190/181112448-af0a3fe0-7b40-45bc-8b1e-f43229bc3d3a.png)

In a regular browser, like **Chrome**, **Firefox** or **Edge** you can show the content of this console by pressing **`F12`** on your keyboard. Of course, this console is way more robust and have many features, but still, can be used for testing purposes.

![image](https://user-images.githubusercontent.com/58167190/181112734-843a4dd4-f361-48dd-8135-342daa258899.png)

Example of **Microsoft's Chromium Edge** console.

Okay, we have already used some functions in here, but... **What are functions?**

**Functions** are a special programming structure meant to perform a defined operation or task. We used our `main()` and `getFullName()` function, from which objetives were to call other functions and printing and returning a full name from a first name and a last name, respectively.

In **JavaScript**, functions are defined in two different ways:

1. By the **arrow function `() => {}`** notation.
2. By using the reserved word **function**.

The syntaxis of the function would look like this:

```
const myNewFunction = (myParameter1, myParamter2, ..., myParameterN) => {
  // Content of the function
  // Perhaps a return
}
```

Or probably like this:

```
function myNewFunction (myParameter1, myParamter2, ..., myParameterN) {
  // Content of the function
  // Perhaps a return
}
```

If well both ways are correct, at least for this course, we will be using the **arrow function `() => {}`** notation.

Did you notice the slashes (`//`) so far in the code? As in many different programming languages, we can use some symbols to indicate in our program that some section of the code should not be taken as statements. Probably we just want to document, take notes or say something useful about our code. For that matter, in **JavaScript**, the `//` and `/**/` symbols are used.

**Examples:**

```
// This is a test function
const myFunction = (text) => {
  return text + " another text";
}
```

```
/*
 * Function test meant for performing some operation. Please
 * notice that this is an option for multiline commentaries
 * inside of the code.
 */
const myFunction = (text) => {
  return text + " another text";
}
```

As shown in the examples, we called our **main** function `main()`, trying to emulate a main function that is used in other programming language and having that name for clearence. However, the function can take any name that we define.

```
const thisIsADumbNameFunctionThatIsNotRelatedToItsFunctionality = (number1, number2) => {
  return number1 + number2;
}
```

Of course makes any sense to call a function with a different name from one that describes functionality, so correcting the example, we would have:

```
const numberAddition = (number1, number2) => {
  return number1 + number2;
}
```

As already said, **JavaScript** give us a lot of freedom when coding, so also, we can call the **received parameters** of the function any way we want. Using the last example:

```
const numberAddition = (ball1, yelloJacketAndJohn) => {
  return ball1 + yelloJacketAndJohn;
}
```

But again, for clearance and to follow the best practice, the best choice is to give the parameters names that are actually related to their use in a given function.

Let's quickly try to change our original HTML + **JavaScript** example a little and test it. We will be using the `numberAddition()` example function. in our **`script.js`** example we will have:

```
const getFullName = (firstName, lastName) => {
  return firstName + " " + lastName;
};

const numberAddition = (number1, number2) => {
  return number1 + number2;
}

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
}

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

## Sources

- [**Mozilla**](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
