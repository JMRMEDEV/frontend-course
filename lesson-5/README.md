# Node.js

So far in this course our JavaScript has always lived **inside a web browser**. We wrote a `.js` file, an HTML page loaded it, and the browser ran it. But JavaScript is not trapped in the browser. **Node.js** is the piece of software that lets us run JavaScript *outside* the browser, straight on our own computer (or on a computer in the cloud).

Do not worry if the word "runtime" or "engine" sounds intimidating, we will unpack it gently. The one idea to hold on to for the whole lesson is this: **Node.js lets you run JavaScript on your desktop (and on servers), not just in a web page.** Everything else here builds on that single sentence.

> **Interview tip:** A very common question is *"Is Node.js a framework?"* The correct answer is **no**. Node.js is a **runtime** (built on a JavaScript engine), not a framework. Keep this straight, it comes up often.

## Module Content

- [**What Node.js Is**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-5/README.md#what-nodejs-is)
- [**Installing Node.js**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-5/README.md#installing-nodejs)
- [**Running JavaScript on Your Machine**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-5/README.md#running-javascript-on-your-machine)
- [**npm: The Node Package Manager**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-5/README.md#npm-the-node-package-manager)
- [**package.json and node_modules**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-5/README.md#packagejson-and-node_modules)
- [**Using a Third-Party Library**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-5/README.md#using-a-third-party-library)
- [**A Note on Tooling**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-5/README.md#a-note-on-tooling)
- [**Module Activity**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-5/README.md#module-activity)
- [**Sources**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-5/README.md#sources)

## What Node.js Is

Let's build the definition one word at a time.

A web browser cannot run JavaScript by magic, it needs a **JavaScript engine**: a program that reads your JavaScript and actually executes it. Google Chrome ships with an engine called **V8**. It is fast, and it is open source.

Someone had a clever idea: *what if we take that same V8 engine out of the browser and let it run JavaScript directly on the operating system?* That is exactly what **Node.js** is, V8 packaged so it can run on your desktop, plus a set of extra abilities that a plain browser does not give you (reading files, opening network connections, reserving a port, and so on).

So a useful working definition:

> **Node.js** is a **runtime** that uses **JavaScript** as its scripting language and runs on **Chrome's V8 engine**. It lets us execute JavaScript on our computer, including many things we would normally only see in a browser.

### Why would I want to run JavaScript outside the browser?

Two big reasons.

1. **Servers and the cloud.** When you use a modern app, the data usually comes from a *server*, a computer that is always on, waiting to answer requests. Most modern services do not run that server on some dusty machine in a closet; they run it on a **virtual machine in the cloud** (a computer that lives in a data center somewhere). With Node.js installed on that cloud machine, we can write the server itself in JavaScript. In other words, Node lets JavaScript power the **backend**, not just the frontend.

2. **Local development.** Even on your own laptop, Node lets you **emulate a server**. It reaches into the operating system, reserves a **port** on your machine, and *serves* your app there so you can open it in your browser at an address like `http://localhost:3000`. This is why, when you run a React project, you visit `localhost` in your browser: Node is quietly running a little server on your own computer.

> Remember the online editor we used in earlier lessons, **CodeSandbox**? It felt like magic, you typed code and a preview appeared. Behind the scenes CodeSandbox also runs a virtual machine with Node on it. So you have already been using Node without realizing it.

The scope of this lesson stops here: we care about *what Node is* and *how to use its tooling*. Actually building servers and APIs is its own topic and belongs to later lessons.

## Installing Node.js

You will need Node installed for the rest of the course, so let's get it.

1. Go to the official site: [**nodejs.org**](https://nodejs.org).
2. The site usually detects your operating system automatically and offers the right installer (for example, an `.msi` Microsoft Installer on Windows).
3. **Always pick the version marked `LTS`.** LTS stands for **Long Term Support**, it is the stable version recommended for most people, as opposed to the newest experimental one.
4. On **macOS** you can use the installer from the site, or install it through a package manager like **Homebrew**. On **Linux**, use your distribution's package manager or the official installer.

Once it finishes, confirm the install worked by opening a **terminal** (command line) and asking Node for its version:

```bash
node --version
```

If Node is installed correctly, this prints a version number such as `v20.11.0`. Installing Node also installs **npm** (more on that below), which you can check the same way:

```bash
npm --version
```

## Running JavaScript on Your Machine

Let's prove the core promise, JavaScript running with no browser at all.

Create an empty folder (say, `node-mini-test`), and inside it create a file named `myFunnyScript.js`. The `.js` extension matters, if you name it `.txt`, Node will not treat it as JavaScript.

> You can write this file in *any* text editor, even the plain Notepad that ships with Windows. That is precisely the point: nothing browser-specific is involved. (In practice, please use a real code editor like **VS Code**, we will get to why in the tooling section, but Node itself does not care.)

Put some ordinary JavaScript inside it:

```js
const number1 = 2;
const number2 = 3;
const sum = number1 + number2;

console.log("sum:", sum);
```

Now open a terminal **in that folder** and run the file by handing it to Node:

```bash
node myFunnyScript.js
```

You will see the output printed right in the terminal:

```
sum: 5
```

That `console.log` output did not come from a browser console, it came from Node executing your script on your operating system. This is the whole idea in miniature.

We can go a little further to show it handles anything JavaScript can, objects, template literals, functions:

```js
const myUser = {
  username: "panchito68",
  age: 22,
  email: "panchito68@gmail.com",
};

const myFunction = () => {
  console.log(`The user is: ${myUser.username}`);
  console.log(`Its age is: ${myUser.age}`);
};

myFunction();
```

Running `node myFunnyScript.js` again prints:

```
The user is: panchito68
Its age is: 22
```

Same JavaScript you already know, no HTML page, no `<script>` tag, just Node.

## npm: The Node Package Manager

Here is where Node becomes genuinely powerful. When you installed Node, you also got **npm**, which stands literally for **Node Package Manager**. Its job is to **install packages** (also called **libraries** or **dependencies**), reusable chunks of JavaScript that other people have written and shared.

Why does that matter? Because of one of the most important principles in programming: **do not reinvent the wheel.** If a problem has already been solved well by someone else, reach for their solution instead of writing hundreds of lines yourself.

You install a package from the terminal with:

```bash
npm install <package-name>
```

For example:

```bash
npm install date-fns
```

There is a famous (and slightly meme-worthy) side effect of npm: a single, simple command can pull in a *huge* number of packages. This happens because each library may itself depend on other libraries, which depend on still others. Creating a fresh React app, for instance, can install **hundreds** of packages and hundreds of megabytes of files, just to get the basics running. That is normal. Each package is a small wheel that someone already built so you do not have to.

> **`npm` vs `npx`:** You will also see a command called `npx`. Roughly, `npm install` **adds a package to your project**, while `npx` **runs a package/template once** (for example, scaffolding a new project) without permanently installing it. Mixing these two up is a classic source of confusion, if a "create a new project" command misbehaves, check whether it should have been `npx` rather than `npm`.

## package.json and node_modules

Two things appear in a Node project that you should recognize.

### `package.json`

`package.json` is a plain text file (in **JSON** format) that describes your project: its name, and crucially, the **list of dependencies** it uses. Every time you run `npm install some-library`, that library gets recorded here. Think of it as the **shopping list** for your project, anyone who receives your code can read `package.json` and reinstall exactly the same libraries.

A trimmed-down example looks like this:

```json
{
  "name": "my-project",
  "version": "1.0.0",
  "dependencies": {
    "date-fns": "^3.6.0"
  },
  "scripts": {
    "start": "node index.js"
  }
}
```

Notice the `scripts` section. It lets you give friendly names to commands. With the example above, typing:

```bash
npm start
```

runs whatever `start` points to. In a React project, `npm start` is what launches the local development server we talked about earlier.

### `node_modules`

When you install packages, their actual code has to live somewhere. That somewhere is a folder called **`node_modules`**. It is where npm downloads every package (and every package's packages). This folder gets **large**, easily hundreds of megabytes, because it contains the real source code of everything you depend on. If you open it, you will find, for example, a `react` folder containing React's own hundreds of thousands of lines of code.

Because `node_modules` is huge and can always be rebuilt from `package.json`, you normally do **not** share it. Instead you share your code plus `package.json`, and whoever receives it runs `npm install` to recreate `node_modules` locally. (Excluding `node_modules` from version control is one of the first things you set up with **Git**, which is a separate topic.)

> **The mental model:** `package.json` is the *recipe* (the list of ingredients), and `node_modules` is the *pantry* full of the actual ingredients. Ship the recipe, not the pantry.

## Using a Third-Party Library

Let's see the payoff with a real, everyday problem: **formatting a date**.

Suppose we create a date in JavaScript and try to show it:

```js
const date = new Date();
console.log(date.toISOString());
// e.g. "2024-11-05T18:18:00.000Z"
```

That `toISOString()` output (`year-month-dayThours:minutes:seconds` plus a time zone) is a standard machine-readable format, but it is **not** how a human reads a date. When a cinema website tells you your showtime, it does not print that wall of text.

To format it by hand, we would have to pull the pieces apart ourselves:

```js
const date = new Date();

const year = date.getFullYear();
const month = date.getMonth(); // ⚠️ see the note below
const day = date.getDate();
const hours = date.getHours();
const minutes = date.getMinutes();

const stringDate = `${day}/${month + 1}/${year} ${hours}:${minutes}`;
console.log(stringDate);
```

> **Note on months:** For historical reasons, JavaScript's built-in `Date` treats months like an array, **January is `0` and December is `11`**. This is genuinely counter-intuitive (days and years are *not* zero-based), and it is a well-known trap. That is why the example writes `month + 1`. It is exactly the kind of fiddly detail a good library saves you from.

Even for this *simple* case we are already writing a pile of error-prone code. Real date work (handling different formats, adding days, subtracting minutes) can balloon into hundreds of lines. Rather than reinvent that wheel, we install a library that has already solved it. A popular one is **`date-fns`**:

```bash
npm install date-fns
```

Now we **import** the specific function we want from the library by its name, and let it do the work:

```js
import { format } from "date-fns";

const date = new Date();

// day/month/year, 24-hour hours:minutes
console.log(format(date, "dd/MM/yyyy HH:mm"));
// e.g. "05/11/2024 18:25"
```

What took us many fragile lines by hand becomes **one clear line**. No manual `month + 1`, no juggling. That is the entire point of libraries: **they make our lives easier by reusing work that is already done well.**

The `import { format } from "date-fns"` line is the same idea you will use constantly in React (`import ... from "react"`). It works because the library's code is sitting in `node_modules`, and npm made it available under its package name.

> **Note:** older Node/JavaScript code often uses `require("date-fns")` instead of `import`. Both mean "bring in this library"; this course uses the modern `import` syntax, which you will also use throughout the React lessons.

## A Note on Tooling

Along the way you will meet several tools. They each have (or will get) their own place in the syllabus, so here we only name them so they are not mysterious:

- **VS Code (Visual Studio Code)** — a very powerful **code editor** (not an IDE by nature, though its extensions can make it feel like one). It gives you syntax coloring, autocompletion, and automatic formatting. Writing the earlier script in Notepad *works*, but VS Code makes the same code far easier to read and edit. (Covered on its own later in the course.)
- **Notepad++** — a lightweight editor that recognizes code better than plain Notepad. Fine in a pinch; a full editor like VS Code is the better default.
- **ESLint** — a tool that enforces a consistent **code style** and can auto-fix issues (for example, on save). It keeps a messy file tidy. (Its own syllabus item.)
- **Postman** — a tool for testing APIs. (Its own syllabus item.)
- **Chakra UI** — a component library *for React* that gives you ready-made, good-looking components so you do not hand-build every button and layout. It is a great example of the "don't reinvent the wheel" idea applied to user interfaces, and you install it exactly like any other package, with npm. (It belongs to the React lessons; we only mention it here as a motivating example of what npm packages can do.)

The common thread: everything above (editors aside) is installed and managed through **npm**, which is why understanding Node and npm comes *before* all of them.

## Module Activity

Put the core idea into practice: **run JavaScript on your own machine and consume a library, with no browser involved.**

1. **Install Node** from [nodejs.org](https://nodejs.org) (LTS version) and confirm it with `node --version`.
2. Create a new folder and, inside it, a file called `myFunnyScript.js`. Write a small program that defines a `user` object (`username`, `age`, `email`) and a function that prints a friendly sentence about that user using a **template literal**. Run it with `node myFunnyScript.js` and confirm the output appears in your terminal.
3. Turn the folder into a real project and add a dependency:
   - Run `npm init -y` to generate a `package.json`.
   - Run `npm install date-fns`.
   - Open `package.json` and confirm `date-fns` now appears under `dependencies`. Notice the new `node_modules` folder.
4. In a script, create a `new Date()` and print it **twice**: once with the raw `toISOString()`, and once formatted with `date-fns`'s `format` function into a human-friendly `dd/MM/yyyy HH:mm`. Compare how much simpler the library makes it.

Deliverable: your `myFunnyScript.js` (and the date-formatting script), plus the `package.json` showing `date-fns` as a dependency. You do **not** need to submit `node_modules`.

<!--
Repair note: In the live session, the instructor's main hands-on demo was a React + Chakra UI setup that broke repeatedly (a scaffolding mistake, using `npm` where `npx` was needed, plus a JavaScript-vs-TypeScript template mismatch) and consumed a long, muddied stretch of the class. That React/Chakra troubleshooting belongs to the React lessons and would teach the wrong lesson here, so it has been intentionally omitted. The activity above is rebuilt from the parts of the class that were clean and on-scope for Node: installing Node, running a .js file with `node`, and consuming the date-fns library via npm. The npm-vs-npx pitfall the instructor hit is captured as a note in the npm section rather than as a broken exercise.
-->

## Sources

- [**Node.js — Official Site**](https://nodejs.org/en)
- [**Node.js Documentation**](https://nodejs.org/en/docs)
- [**npm Documentation**](https://docs.npmjs.com/)
- [**date-fns Documentation**](https://date-fns.org/docs/Getting-Started)
- [**MDN — JavaScript**](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
