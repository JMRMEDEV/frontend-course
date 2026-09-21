# VS Code

Up to this point in the course we have been writing code, running JavaScript with [**Node**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-5/README.md), building interfaces with [**React**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-8/README.md). But *where* do we actually type all that code? During the live sessions most of the work happened online in CodeSandbox, which is perfect for learning. On your own machine, though, the tool almost every professional web developer reaches for is **Visual Studio Code**, usually shortened to **VS Code**.

Do not worry if you have heard scary words like "IDE", "extensions", "IntelliSense" or "command palette" and felt lost. This lesson unpacks all of them in plain language. By the end you will be able to install VS Code, open a project folder, move around its interface with confidence, add a couple of essential extensions, use the built-in terminal, and let the editor format your code for you automatically. The goal is simple: **get you productive in VS Code as fast as possible.**

> **Note:** VS Code is developed by Microsoft, is **free**, and runs on Windows, macOS, and Linux. Its interface changes gradually over time, so a menu label or icon might look slightly different from a screenshot you find online. The concepts in this lesson stay the same; when in doubt, trust the official docs at [code.visualstudio.com/docs](https://code.visualstudio.com/docs).

## Module Content

- [**Editor vs IDE**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-10/README.md#editor-vs-ide)
- [**Installing VS Code**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-10/README.md#installing-vs-code)
- [**A Tour of the Interface**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-10/README.md#a-tour-of-the-interface)
- [**Opening a Folder**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-10/README.md#opening-a-folder)
- [**Syntax Highlighting**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-10/README.md#syntax-highlighting)
- [**The Integrated Terminal**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-10/README.md#the-integrated-terminal)
- [**Extensions**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-10/README.md#extensions)
- [**IntelliSense**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-10/README.md#intellisense)
- [**Format on Save**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-10/README.md#format-on-save)
- [**Snippets**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-10/README.md#snippets)
- [**Essential Shortcuts**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-10/README.md#essential-shortcuts)
- [**Module Activity**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-10/README.md#module-activity)
- [**Sources**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-10/README.md#sources)

## Editor vs IDE

This is the single most important idea in the whole lesson, and it is a very common interview question, so let's get it straight.

**VS Code is a code *editor*, not an IDE.** These two things are genuinely different:

- A **code editor** is, at heart, a smart text editor for writing code. It gives you niceties like coloring your code, autocompletion, and searching across files, but its *nature* is editing text.
- An **IDE** (Integrated Development Environment) is a bigger, all-in-one package. It **includes** a code editor, but *bundles* many more tools alongside it out of the box: a compiler or interpreter, a debugger, a build system, project management, and so on. Classic examples are Visual Studio (not "Code"), IntelliJ IDEA, and Eclipse.

Here is the relationship, and the exact distinction your instructor stressed:

> An **IDE usually includes a code editor**, but the reverse is **not** true, a code editor is not automatically an IDE.

So why does everyone treat VS Code like an IDE? Because it is a **very advanced** editor that lets you add so much functionality (through *extensions*, which we cover below) that you can basically **turn it into an IDE-like environment**, gaining debugging, linting, autocompletion, and more. But in its *nature* it is still a code editor. Keep that nuance in mind:

> **Interview tip:** *"Is VS Code an IDE?"* The precise answer is **no, it is a code editor** that can be extended until it feels like an IDE. *"Does an IDE contain an editor?"* **Yes.**

To make the point concrete: you could technically write JavaScript in Notepad and run it with Node, it works. But Notepad gives you a wall of same-colored text with no help whatsoever. An editor like VS Code colors your code, completes it, formats it, and catches mistakes. It is the difference between writing in the dark and writing with the lights on.

> **Note:** There is also a middle-ground editor called **Notepad++** that recognizes code better than plain Notepad. It is fine in a pinch, but a full editor like VS Code is the better default for this course.

## Installing VS Code

Installing VS Code has, in the instructor's words, *"no great science"* to it, it is basically "go to the link and download it." Still, there is one checkbox on Windows worth knowing about.

1. Open your browser and go to the official site: [**code.visualstudio.com**](https://code.visualstudio.com).
2. The **Download** button usually **detects your operating system automatically** (Windows, macOS, or Linux) and offers the right installer. Click it.
3. Run the downloaded installer and accept the defaults by clicking through.
4. **Windows users, watch for one step.** During setup, on the *"Select Additional Tasks"* screen, you will see checkboxes. Make sure the option **"Add 'Open with Code' action to Windows Explorer file context menu"** (there are usually two, one for files and one for directories) is checked. This is what lets you **right-click any folder and choose *"Open with Code"*** to jump straight into a project, a huge time-saver.

Once it is installed, that is it, you are ready to open your first folder.

> **Note (macOS/Linux):** On macOS you drag the app into *Applications*; on Linux you install via your package manager or a downloaded package. To get the handy `code .` terminal command on macOS, open the Command Palette (see below) and run *"Shell Command: Install 'code' command in PATH"*.

## A Tour of the Interface

When VS Code opens, the window is divided into a few main areas. Do not be overwhelmed, you will use all of them within your first hour.

1. **Activity Bar** (far left, vertical strip of icons). Switches between major views. The most important ones:
   - **Explorer** (the pages icon) — the file/folder tree of your project.
   - **Search** (the magnifying glass) — find and replace text across your whole project.
   - **Source Control** (the branching icon) — where Git changes show up.
   - **Run and Debug** (the play-with-bug icon) — for running and debugging code.
   - **Extensions** (the blocks icon) — the marketplace where you add functionality.
2. **Side Bar** (next to the Activity Bar). Shows the contents of whichever view is active, most often the **Explorer** with your files.
3. **Editor** (the big central area). Where you actually read and write code. You can open several files at once as **tabs**, and even split the editor side by side to view two files together.
4. **Panel** (bottom area). Holds the **integrated Terminal**, the **Problems** list, the **Output**, and the **Debug Console**.
5. **Status Bar** (very bottom strip). Small but useful: it shows the current Git branch, the file's language (e.g. "JavaScript"), line/column position, and any errors/warnings count.
6. **Command Palette** (not always visible, you summon it). This is VS Code's superpower: a search box for *commands*. Press **`Ctrl`+`Shift`+`P`** (macOS: **`Cmd`+`Shift`+`P`**) and start typing what you want to do, "format document", "toggle terminal", "change language mode". If you only remember one shortcut from this whole lesson, remember this one, because it can find every other feature for you.

## Opening a Folder

A crucial habit: **in VS Code you work on a *folder* (a project), not just a lone file.** Opening the whole folder is what lets features like search, IntelliSense, and the integrated terminal understand your project as a unit.

You have a few ways to open a folder:

- **From inside VS Code:** *File → Open Folder…* and pick your project directory.
- **From Windows Explorer:** right-click the folder and choose **"Open with Code"** (this is the context-menu option you enabled during installation).
- **From the terminal** (once the `code` command is available): navigate into the folder and run:

```bash
code .
```

The `.` means "the current folder". This opens VS Code with that folder already loaded, its files appear in the **Explorer** on the left, ready to edit.

## Syntax Highlighting

One of the first things you will notice is that your code is no longer one flat color, VS Code **colors different pieces of code differently**. This is called **syntax highlighting**, and it exists for one reason: to make code **readable** at a glance.

Take a small JavaScript snippet. In a plain editor it is all the same color; in VS Code, each kind of token gets its own color. Roughly (exact colors depend on your theme):

```js
// comments are shown in one muted color
const number1 = 2;          // "const" (keyword) and "number1" (constant) are colored
const myUser = {
  username: "panchito68",   // strings get their own color
  age: 22,                  // numbers get another color
};

const myFunction = () => {  // function names are colored yet differently
  console.log(myUser.username); // "username" (a property) is colored as a property
};
```

Constants, properties, strings, numbers, comments, and function names each get a distinct color. Ask yourself the instructor's question: *just from the colors, ignoring everything else, which is easier to read, a wall of identical text, or this?* The colored version wins every time. That readability is exactly why we use an editor instead of Notepad.

> **Note:** You can change the color scheme (the **theme**) freely. Open the Command Palette and run *"Preferences: Color Theme"*, then arrow through the options to preview them live. Dark themes are popular, but pick whatever you find most readable, it has no effect on how your code runs.

## The Integrated Terminal

You already know the terminal from the [**Node lesson**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-5/README.md), where we ran commands like `node myFunnyScript.js`. The great thing about VS Code is that it has a **terminal built right in**, so you do not have to switch to a separate window.

Open it with **``Ctrl`+` `` `** (Control + backtick, the key above `Tab`) or via *Terminal → New Terminal* from the menu. A panel appears at the bottom.

Here is a subtle but important point the instructor made: **the integrated terminal is not a "VS Code terminal", it is your operating system's own shell running inside the editor.** On Windows it is typically PowerShell; on macOS and Linux it is your usual shell (bash, zsh, etc.). VS Code is simply *hosting* it. That means anything you can do in your normal terminal, you can do here, with the bonus that it opens already pointed at your project folder.

So you can run exactly what you ran before, without leaving the editor:

```bash
node myFunnyScript.js
```

And for a React project, the commands you already know from earlier lessons:

```bash
npm install
npm start
```

Having your files, your code, and your terminal in one window is a big part of what makes VS Code feel productive.

## Extensions

Here is where a plain editor grows toward an IDE-like tool. **Extensions** are add-ons that give VS Code **extra functionality it does not have out of the box**: things like debugging support for a language, linting, autocompletion for a framework, Git integrations, and much more. This is precisely the mechanism that lets you *"turn VS Code into an IDE-like environment."*

You install them from the **Extensions** view: click the blocks icon in the Activity Bar (or press **`Ctrl`+`Shift`+`X`**), search by name, and click **Install**.

A few must-haves for web development:

- **ESLint** (publisher: Microsoft) — surfaces code-style and correctness problems from **ESLint** directly in the editor, underlining issues and offering fixes. ESLint gets its own treatment in [**lesson 12**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-12/README.md); here, just know the extension is what lets its warnings show up as you type and enables the *fix on save* behavior we describe below.
- **Prettier – Code formatter** (publisher: Prettier) — an opinionated code formatter. Where ESLint focuses on *problems*, Prettier focuses on *consistent formatting* (indentation, quotes, line width). It is the tool most people wire up to "format on save".
- **npm Intellisense** / **Path Intellisense** — autocomplete package names and file paths in your `import` statements.
- **GitLens** — supercharges VS Code's built-in Git, showing who changed each line and when. (Git itself is a separate topic.)

> **Note:** Extensions are optional and swappable, there is no single "correct" set. ESLint and Prettier are the two you will almost certainly want for the projects in this course. Install only what you need; too many extensions can slow the editor down.

> **Note (ESLint vs Prettier):** They complement each other. ESLint catches *code-quality* issues ("this variable is never used"); Prettier enforces *formatting* ("use two-space indentation"). Modern setups run both, and Prettier is usually the one that reformats your file on save.

## IntelliSense

**IntelliSense** is VS Code's umbrella name for its **smart autocompletion**. As you type, the editor pops up a list of suggestions, variable names, function names, and, very usefully, the **properties available on an object**.

Recall the `myUser` object from the Node lesson. Because VS Code understands JavaScript, when you type `myUser.` it *knows* that `myUser` is an object with `username`, `age`, and `email`, and it offers exactly those:

```js
const myUser = {
  username: "panchito68",
  age: 22,
  email: "panchito68@gmail.com",
};

// Type "myUser." and IntelliSense suggests: username, age, email
console.log(myUser.email);
```

This does more than save keystrokes, it prevents typos and reminds you what is actually available, so you spend less time guessing and looking things up. IntelliSense gets even more powerful with **TypeScript** (see [**lesson 4**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-4/README.md)), because types tell the editor even more precisely what each value can do.

> **Tip:** If the suggestion list does not appear on its own, you can summon it any time with **`Ctrl`+`Space`**.

## Format on Save

This is one of the most satisfying features to enable early. **Format on save** means that every time you save a file, VS Code automatically tidies its formatting, fixing indentation, spacing, and line breaks, so you never have to do it by hand.

Picture the instructor's demonstration: he deliberately wrote messy code, hundreds of stray spaces, random blank lines, wild indentation, the kind of thing that makes you go *"what is this?"* when you open a teammate's file. Then he simply pressed save (**`Ctrl`+`S`**) and everything snapped neatly into place. That "auto-fix on save" is exactly what we are enabling.

There are two related pieces:

1. **Format Document** — you can always format the current file on demand: right-click in the editor and choose **Format Document**, or use the Command Palette (*"Format Document"*), or the shortcut **`Shift`+`Alt`+`F`** (macOS: **`Shift`+`Option`+`F`**).
2. **Do it automatically on every save** — this is the real productivity win.

To turn on automatic formatting, open your **Settings** (Command Palette → *"Preferences: Open User Settings (JSON)"*) and add:

```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode"
}
```

The first line turns on formatting-on-save; the second tells VS Code to use **Prettier** as the formatter (this requires the Prettier extension from the previous section).

If you also want ESLint to **auto-fix** its problems every time you save (the exact behavior the instructor had configured), add this too:

```json
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  }
}
```

Now a save both **formats** the file (Prettier) and **fixes fixable lint problems** (ESLint). Messy code cleans itself up the moment you hit `Ctrl`+`S`.

> **Note:** These settings can live in your personal **User** settings (applies everywhere) or in a project's **Workspace** settings (a `.vscode/settings.json` file committed with the project, so the whole team formats identically). For a shared project, workspace settings are the better choice.

## Snippets

A **snippet** is exactly what it sounds like: a small, reusable **piece of code** that you can insert by typing a short trigger word instead of writing it all out. Snippets save you from re-typing boilerplate you write over and over.

VS Code ships with some built-in snippets, and many extensions add more. For example, in a React file, popular snippet packs let you type a short prefix like `rfc` and press `Tab` to expand it into a whole React function-component skeleton, or type `log` to expand into `console.log()`. You type a few letters, hit `Tab`, and the full template appears with the cursor already positioned for you to fill in.

You can also make **your own** snippets for code you personally repeat. Open the Command Palette and run *"Snippets: Configure Snippets"*, choose a language, and add an entry. A minimal example for a `console.log` shortcut looks like this:

```json
{
  "Print to console": {
    "prefix": "cl",
    "body": ["console.log($1);"],
    "description": "Log output to the console"
  }
}
```

With that in place, typing `cl` and pressing `Tab` inserts `console.log();` with the cursor waiting between the parentheses (that is what `$1` marks). Small, but multiplied across a day of coding it adds up.

## Essential Shortcuts

You do not need to memorize these all at once, but a handful will quickly become muscle memory. (On macOS, swap `Ctrl` for `Cmd` in most of these.)

| Action | Windows / Linux | What it does |
| --- | --- | --- |
| **Command Palette** | `Ctrl`+`Shift`+`P` | Search and run *any* command (the master key) |
| **Quick Open file** | `Ctrl`+`P` | Jump to any file by typing part of its name |
| **Save** | `Ctrl`+`S` | Save (and, if enabled, format) the current file |
| **Toggle Terminal** | ``Ctrl`+` `` ` | Show/hide the integrated terminal |
| **Format Document** | `Shift`+`Alt`+`F` | Reformat the whole file now |
| **Find in file** | `Ctrl`+`F` | Search within the current file |
| **Find in project** | `Ctrl`+`Shift`+`F` | Search across all files |
| **Comment line** | `Ctrl`+`/` | Toggle a `//` comment on the current line |
| **Multi-cursor** | `Alt`+`Click` | Place several cursors to edit many spots at once |
| **Rename symbol** | `F2` | Rename a variable/function everywhere at once |
| **Trigger IntelliSense** | `Ctrl`+`Space` | Force the autocomplete suggestions to appear |

> **Note:** Every shortcut is customizable. Open the Command Palette and run *"Preferences: Open Keyboard Shortcuts"* to view or change any of them, and to discover many more.

## Module Activity

Put it all together by setting up a real local project in VS Code, no CodeSandbox this time.

1. **Install VS Code** from [code.visualstudio.com](https://code.visualstudio.com). On Windows, tick the *"Open with Code"* context-menu option during setup.
2. **Create a project folder** somewhere on your computer (e.g. `vscode-practice`) and **open it in VS Code**, either with *File → Open Folder…*, by right-clicking the folder and choosing *"Open with Code"*, or by running `code .` inside it.
3. **Explore the interface:** locate the Explorer, open the Command Palette (`Ctrl`+`Shift`+`P`) and read the list of commands it offers, then open the integrated terminal (``Ctrl`+` ``).
4. **Write and run a script.** Create `myFunnyScript.js` with a small program (reuse the `user` object idea from the Node lesson) and run it in the integrated terminal with `node myFunnyScript.js`. Confirm the output prints right there in VS Code. Notice the **syntax highlighting** coloring your constants, strings, and functions.
5. **Install two extensions:** **ESLint** and **Prettier – Code formatter** from the Extensions view.
6. **Enable format on save.** Open your settings JSON and add `"editor.formatOnSave": true` with Prettier as the default formatter. Then deliberately mess up your file's formatting (add random spaces, blank lines, and bad indentation) and press `Ctrl`+`S`, watch it snap back into shape.
7. **Try IntelliSense and a snippet.** Type `yourObject.` and watch the property suggestions appear; then create the `cl` snippet from the Snippets section and use it to insert a `console.log`.

Deliverable: a screenshot (or short description) of your VS Code window showing your project open, the script's output in the integrated terminal, and format-on-save working. No files need to be submitted, this activity is about getting comfortable in the editor you will use for the final project.

## Sources

- [**Visual Studio Code — Documentation**](https://code.visualstudio.com/docs)
- [**VS Code — Introductory Videos**](https://code.visualstudio.com/docs/getstarted/introvideos)
- [**VS Code — The Basics of the Editor (User Interface)**](https://code.visualstudio.com/docs/editing/getting-started/userinterface)
- [**VS Code — Integrated Terminal**](https://code.visualstudio.com/docs/terminal/basics)
- [**VS Code — IntelliSense**](https://code.visualstudio.com/docs/editing/intellisense)
- [**VS Code — Snippets**](https://code.visualstudio.com/docs/editing/userdefinedsnippets)
- [**VS Code — Extension Marketplace**](https://code.visualstudio.com/docs/configure/extensions/extension-marketplace)
- [**Prettier — Documentation**](https://prettier.io/docs/)
- [**ESLint — Documentation**](https://eslint.org/docs/latest/)
- [**MDN — Web development learning resources**](https://developer.mozilla.org/en-US/docs/Learn)
