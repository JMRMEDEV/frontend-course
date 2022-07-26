# JavaScript

JavaScript (JS) is a lightweight, interpreted, or just-in-time compiled programming language with first-class functions. While it is most well-known as the scripting language for Web pages, many non-browser environments also use it, such as Node.js, Apache CouchDB and Adobe Acrobat. JavaScript is a prototype-based, multi-paradigm, single-threaded, dynamic language, supporting object-oriented, imperative, and declarative (e.g. functional programming) styles.

**JavaScript** and **Java** are entirely different programming languages.

## Module Content

- [**JavaScript Pros and Cons**](https://github.com/JMRMEDEV/frontend-course/tree/master/lesson-3#javascript-pros-and-cons)
- [**Sources**](https://github.com/JMRMEDEV/frontend-course/tree/master/lesson-3#sources)
- [**HTML and JavaScript**](https://github.com/JMRMEDEV/frontend-course/tree/master/lesson-3#html-and-javascript)

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

The first thing that we need to work with **JavaScript** in these exercises, is to create a **JavaScript** (`.js`) file. Let's go to our favorite **editor** for working with **JavaScript**. Let's use [**Code Sandbox**](https://codesandbox.io) for our example. Let's create a new folder called `js` and inside of it, lets create a `script.js`.

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
  getFullName();
};

main();
```



## Sources

- [**Mozilla**](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
