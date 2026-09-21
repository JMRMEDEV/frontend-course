# Asynchronous Functions

Up to now, almost every program we have written runs **top to bottom, one line at a time**: line 1 finishes, then line 2 runs, then line 3, and so on. That predictable, orderly flow is called **synchronous** code, and it is exactly what we are used to. But the real world of web development is not always that tidy. Some operations, like asking a server on the other side of the planet for data, do **not** finish instantly, and we simply cannot know in advance how long they will take.

Do not worry if the word *asynchronous* sounds intimidating. Break it down: *a-* means "not", and *synchronous* means "happening at the same, coordinated time". So **asynchronous** just means *"not perfectly in step / not guaranteed to finish right away"*. This lesson is about how JavaScript deals with those slow, unpredictable tasks **without freezing your whole app** while it waits.

We will connect this to something you already met in [**lesson 6 (APIs)**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-6/README.md): the idea that a server hands us data when we make an HTTP call. Here we focus on the **mechanics of waiting** for that data correctly. We will not re-explain what an API is, if you need a refresher, revisit lesson 6.

## Module Content

- [**Synchronous vs Asynchronous**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-7/README.md#synchronous-vs-asynchronous)
- [**Why Does Async Exist?**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-7/README.md#why-does-async-exist)
- [**Callbacks (a quick word)**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-7/README.md#callbacks-a-quick-word)
- [**Promises**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-7/README.md#promises)
- [**async / await**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-7/README.md#async--await)
- [**Handling Errors: try / catch / finally**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-7/README.md#handling-errors-try--catch--finally)
- [**Calling an API with fetch**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-7/README.md#calling-an-api-with-fetch)
- [**Module Activity**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-7/README.md#module-activity)
- [**Sources**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-7/README.md#sources)

## Synchronous vs Asynchronous

Let's start from what we already know. Consider this small, ordinary program:

```js
const myVar = 12;
const mySecondVar = 13;

const myAddFunction = (paramA, paramB) => {
  return paramA + paramB;
};

const result = myAddFunction(myVar, mySecondVar);
console.log(result); // 25
```

Think about the order in which things happen:

1. First, `myVar` is created.
2. Then, `mySecondVar` is created.
3. Then, `myAddFunction` is defined.
4. Then, we call it and store the `result`.
5. Then, we print `25`.

Each step happens **in the exact instant after the previous one finishes**. Nothing here can "take a while", adding two numbers is immediate. This is **synchronous** code: step 1, then step 2, then step 3, in a strict, guaranteed line.

The problem is that many operations in programming are **not** immediate like that. They depend on things outside our control, such as:

- your **internet connection** (do you even have signal? how fast is it?),
- the **size of a file** you are downloading or saving,
- the current **load on your CPU** or disk,
- whether a **server** is fast, slow, or overwhelmed with other users.

Any of these factors can make an operation take a fraction of a second... or several seconds... or fail entirely. Those are **asynchronous** operations. We need a way to say *"go do this slow thing, and I do not know exactly when you will be done, but handle it gracefully"*.

## Why Does Async Exist?

Here is the key fact you must hold onto: **JavaScript is single-threaded**. We hinted at this all the way back in the [**JavaScript lesson**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-3/README.md): JavaScript does **one thing at a time**, like a single cook working through orders one after another.

Now imagine that single cook receives an order that requires waiting 30 seconds for water to boil. If the cook just **stands there frozen** staring at the pot, every other customer waits too, nobody gets served, the whole kitchen stalls. That would be terrible.

That is precisely what would happen if a slow task (like fetching data from a server) blocked JavaScript's single thread: your **entire page would freeze**, buttons would stop responding, animations would halt, until the data finally arrived. Unacceptable.

So asynchronous behavior exists to solve exactly this: it lets JavaScript **start** a slow task (a network request, reading a file, saving data) and then **keep the kitchen running** for everyone else, coming back to deal with the result once it is ready. The slow work does not block the single thread.

Picture the difference:

```
SYNCHRONOUS (blocking):
  [ ask server ]───(frozen, nothing else can happen)───[ got data ] → next line

ASYNCHRONOUS (non-blocking):
  [ ask server ]···························[ got data, handle it ]
        │
        └─► meanwhile, the rest of the app keeps working
```

Network requests are the classic example, and the one we care about most in front-end work: when your app asks a server for data, that request travels across the internet and back. It might be fast, it might be slow. Either way, we do not want to freeze the app while we wait.

## Callbacks (a quick word)

Historically, the *first* tool JavaScript offered for "do this **when** the slow thing finishes" was the **callback**: a function you hand to another function, to be called *later*, once the work is done.

You have actually already used callbacks without naming them. Remember the button from the JavaScript lesson?

```js
button.onclick = handleOnClick; // handleOnClick runs LATER, when the click happens
```

`handleOnClick` is a callback, we are not running it now, we are saying *"run this later, when the event occurs"*. Array methods like `forEach` and `map` also take callbacks.

For asynchronous work, callbacks technically do the job, but when you need to wait for one thing, *then* another, *then* another, they nest into a hard-to-read mess (sometimes nicknamed "callback hell"). Because of that, modern JavaScript gives us cleaner tools built on top of the same idea: **Promises** and **async/await**. Those are what we will focus on, and what you will use in practice.

> **Note:** You do not need to master raw callbacks for asynchronous code in this course. Just know they were the original approach, and that Promises and `async/await` were created to make the same job much more readable.

## Promises

A **Promise** is JavaScript's way of representing *"a value that is not here yet, but should arrive later"*, kind of like a receipt you get when you order food: you do not have the meal in your hands yet, but you hold a token that will eventually turn into either your meal, or an apology that they ran out.

A Promise is always in exactly one of **three states**:

- **pending** → the work is still in progress. The value has not arrived yet. (You are still waiting for your order.)
- **fulfilled** (also called *resolved*) → the work succeeded and the value is ready. (Your meal arrived.)
- **rejected** → the work failed. (They ran out; you get an error explaining why.)

```
                 ┌──────────► fulfilled (we got the value)
   pending ──────┤
                 └──────────► rejected  (something went wrong)
```

Why does this matter? Because functions that do slow work do **not** hand you the finished value directly, they hand you a **Promise** immediately, while the real work continues in the background.

This is exactly what surprises people the first time. Watch what happens if we try to use a network result *without* waiting for it:

```js
const url = "https://random-data-api.com/api/v2/users?size=10";

const retrieveUsers = () => {
  const response = fetch(url); // fetch() is asynchronous by nature
  console.log(response);       // What do we see here?
};

retrieveUsers();
```

You might expect to see the user data. Instead, the console shows something like:

```
Promise { <pending> }
```

That is JavaScript telling us: *"I started the request, but at this exact instant the data has not come back yet, so all I can give you is this pending Promise."* The request simply had no time to finish before that `console.log` ran. We need a way to say **"wait for this Promise to settle before continuing"**, and that is what `async`/`await` is for.

## async / await

`async` and `await` are two keywords that work together to make asynchronous code **read like ordinary synchronous code**, while still not blocking the app.

- **`async`** goes in front of a function. It marks that function as one that will perform asynchronous work (and, under the hood, makes it return a Promise).
- **`await`** goes in front of a Promise *inside* an `async` function. It means: *"pause right here and wait until this Promise settles, then give me its actual value (not the Promise wrapper)."*

Think of `await` as **forcing an asynchronous operation to behave synchronously for us**: *"however long you take, five seconds, a minute, I will wait for you to finish before running the next line."*

There is one strict rule: **`await` can only be used inside a function marked `async`**. If you try to `await` in a normal function, JavaScript will complain that you cannot use `await` outside an async function.

Let's fix the earlier example so we actually get the value:

```js
const url = "https://random-data-api.com/api/v2/users?size=10";

const retrieveUsers = async () => {         // marked async
  const response = await fetch(url);        // wait for the request to come back
  const data = await response.json();       // wait again while we read/parse the body
  console.log(data);                        // now this really is our data
};

retrieveUsers();
```

Notice we used `await` **twice**. That is not a typo, both steps are asynchronous:

1. `await fetch(url)` waits for the server to respond.
2. `await response.json()` waits while JavaScript reads that response and converts it into a usable JavaScript value.

We will unpack `fetch` and `.json()` in detail in the next section. For now, the takeaway is: **`async` marks the function, `await` waits for each Promise, and after `await` you finally hold the real value instead of a pending Promise.**

## Handling Errors: try / catch / finally

Asynchronous operations are exactly the kind of thing that can **fail**. Maybe your Wi-Fi drops mid-request. Maybe it started raining and your internet provider is having a bad day. Maybe the server got hacked or is simply down. Maybe you (or a user) typed the URL wrong. Any of these can make the request fail, and if we do not handle that, our program crashes.

For this, JavaScript gives us the **`try / catch`** structure (also available in other languages like Java and C#). It reads almost like plain English:

- **`try`** → *"attempt to do this."*
- **`catch`** → *"if anything went wrong while trying, do this instead."* It receives the **error** that was caught, so we can inspect or report it.
- **`finally`** *(optional)* → *"either way, success or failure, always run this at the end."* Useful for cleanup, like turning off a loading spinner.

```js
const retrieveUsers = async () => {
  try {
    const response = await fetch(url);
    const data = await response.json();
    console.log(data);
  } catch (error) {
    // This block only runs if something inside `try` failed.
    console.error("There was an error connecting to the server:", error);
  } finally {
    // This runs no matter what.
    console.log("Finished attempting to fetch users.");
  }
};
```

If, say, a user accidentally typed `htttps://...` instead of `https://...`, the URL becomes invalid, `fetch` fails, and control jumps straight into the `catch` block, so instead of a mysterious crash, we can show a friendly message. That is the whole point: **`try/catch` lets us react to failure gracefully.**

> **Note:** Always name the caught value something meaningful like `error` (not `e` or a random name). When you are debugging at 2 a.m., a clear name is a gift to your future self.

## Calling an API with fetch

Now let's put everything together in the scenario you will meet constantly in real front-end work (and in job interviews for React roles): *"Here is a URL. Read the users from it."*

In [**lesson 6 (APIs)**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-6/README.md) we saw that a server exposes data and that reading data is done with the **GET** HTTP method. From the front-end, we do **not** care how the data got there or which database is behind it, someone gives us a URL, and when we make an HTTP call to it, we get data back. That is all we need.

The built-in JavaScript function for this is **`fetch`**. In its simplest form, you give `fetch` a URL and it performs a **GET** request (reading data) by default:

```js
const response = await fetch("https://random-data-api.com/api/v2/users?size=10");
```

But there is a subtlety. `fetch` does **not** hand you the final data directly. It hands you a **`response`** object, which describes the *whole* reply from the server, including things like:

- **`response.ok`** → `true` if the call succeeded.
- **`response.status`** → the numeric HTTP status code. You have probably seen these in the wild: the dreaded `404` (not found), or a `429`/`503` when a ticket site is overwhelmed the second concert tickets go on sale.
- **`response.headers`** → extra metadata about the reply.

We usually do not want all that. We want the **actual data**. To dig it out, the `response` object has a method called **`.json()`**:

```js
const data = await response.json();
```

`JSON` stands for **JavaScript Object Notation**, it is data written in the shape of JavaScript objects and arrays, which (as we learned) is the natural way JavaScript stores structured, related information. `.json()` says *"forget the status and headers, just parse the body into a real JavaScript value I can use."* And because reading/parsing that body also takes time, `.json()` **also returns a Promise**, which is why we `await` it too.

Here is the complete, correct pattern, the one you can genuinely copy and reuse:

```js
const USERS_URL = "https://random-data-api.com/api/v2/users?size=10";

const fetchUsers = async () => {
  try {
    const response = await fetch(USERS_URL); // 1) call the server (GET by default)
    const data = await response.json();      // 2) parse the JSON body into JS
    console.log(data);                       // 3) use the data (an array of users)
  } catch (error) {
    console.error("The data could not be fetched:", error);
  }
};

fetchUsers();
```

What comes back from this particular API is an **array of objects**, where each object is a user, and some properties are themselves objects (a nested `address` with `city`, `state`, coordinates, and so on). This is the "complex, nested structure" we talked about with objects. Because it is just objects and arrays, we access it the same way as always:

```js
const data = await response.json();

console.log(data[0]);                         // the first user (an object)
console.log(data[0].first_name);              // that user's first name
console.log(data[0].address.city);            // digging into a nested object
console.log(data.length);                     // how many users we received (10)
```

> **Note:** Property names such as `first_name` use underscores because that is exactly how *this* server sends them, we must match the server's spelling. Different APIs use different naming styles, so always inspect the real data (you can even paste a public API URL straight into your browser) before writing your code.

And that is the essence of asynchronous front-end work: **`fetch` lets us read data from a server; `await` forces us to wait for both the response and its JSON body; and `try/catch` protects us when the network misbehaves.** In the next module (React) you will take exactly this pattern and use it to display real users on screen.

## Module Activity

<!--
  The instructor deliberately did NOT assign a standalone async exercise in the
  recording; hands-on async practice was postponed to the React module, and the
  live coding also had a couple of small "which await goes where" hiccups. So the
  activity below is a clean, self-contained equivalent in the same spirit as what
  students actually watched being built: fetch users from the same public API,
  await correctly, guard against errors, and read the resulting data.
-->

Build a small **plain JavaScript** program (no React yet) that fetches a list of users from a public API and prints information about them. This is the exact skill an interviewer will ask you to demonstrate before you touch any UI.

Use this public endpoint (it needs no API key):

```
https://random-data-api.com/api/v2/users?size=10
```

Requirements:

1. Create an **`async`** function called `fetchUsers`.
2. Inside a **`try` block**, use **`fetch`** with `await` to call the URL, then use **`await response.json()`** to parse the data.
3. In a **`catch` block**, print a clear error message (use `console.error`) so a failed request does not crash your program silently.
4. Once you have the data, `console.log`:
   - the **total number** of users received (hint: `.length`),
   - the **first name** of the **first** user,
   - the **city** of the first user (hint: it lives inside a nested `address` object).
5. Call `fetchUsers()` so it actually runs.

**Stretch goals (optional):**

- Add a **`finally`** block that logs `"Done."` whether or not the request succeeded.
- Loop through **all** the users with `forEach` (or `map`) and print each user's full name (`first_name` + `last_name`).
- Deliberately break the URL (e.g. type `htttps://`) and confirm your `catch` block runs, then fix it. This proves your error handling works.

You can run this in [**Code Sandbox**](https://codesandbox.io), in a Node.js file, or straight in your browser's developer console (`F12`).

## Sources

- [**MDN — Asynchronous JavaScript**](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous)
- [**MDN — Using Promises**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
- [**MDN — async function**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
- [**MDN — await**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await)
- [**MDN — try...catch**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch)
- [**MDN — Using the Fetch API**](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
