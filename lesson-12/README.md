# Code styling with ESLint

Imagine you open a project written by a teammate (or by yourself, six months ago) and every file uses a slightly different style: some lines end with a semicolon and some do not, some blocks are indented with 2 spaces and others with 4, a variable is declared but never used, and there is a typo in a function name that only explodes when you run the app. Reading that code feels like reading a book where every page uses a different font. [**ESLint**](https://eslint.org/) is the tool that fixes exactly this: it is *"a library that gives style to the code"*, and it can also catch real mistakes **before** you ever run your program.

Do not worry if the word **"linter"** sounds intimidating. A linter is simply a program that reads your code and points out problems, the same way a spell-checker reads an essay and underlines misspelled words. In this lesson we focus on **ESLint fundamentals** for a plain Node.js/JavaScript project: what a linter is, how ESLint differs from Prettier, how to install and configure it, how rules and severities work, how to run it from the command line, and how to make your editor fix problems automatically every time you save.

> Note: This lesson deliberately stays on **ESLint fundamentals**. The **React-specific** plugins and rules (`eslint-plugin-react`, `eslint-plugin-jsx-a11y`, `eslint-plugin-react-hooks`) are already covered in [**lesson 9 — React Key Concepts**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-9/README.md#f-react--typescript--eslint). We will not repeat them here; instead we build the foundation those React rules sit on top of.

## Module Content

- [What is a linter (and why use one)](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-12/README.md#what-is-a-linter-and-why-use-one)
- [ESLint vs Prettier](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-12/README.md#eslint-vs-prettier)
- [Installing ESLint in a Node project](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-12/README.md#installing-eslint-in-a-node-project)
- [The configuration file](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-12/README.md#the-configuration-file)
- [Rules and severity](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-12/README.md#rules-and-severity)
- [Running ESLint from the CLI](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-12/README.md#running-eslint-from-the-cli)
- [Editor integration and format-on-save](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-12/README.md#editor-integration-and-format-on-save)
- [Shareable configs (Airbnb, Standard)](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-12/README.md#shareable-configs-airbnb-standard)
- [Module Activity](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-12/README.md#module-activity)
- [Sources](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-12/README.md#sources)

## What is a linter (and why use one)

A **linter** is a tool that reads your source code **without running it** (this is called **static analysis**) and reports two kinds of things:

1. **Errors and likely bugs** — code that is probably wrong. For example, using a variable you never defined, declaring a variable you never use, comparing values with `==` when you meant `===`, or an `if` that can never be true.
2. **Style inconsistencies** — code that *works* but does not follow an agreed-upon style. For example, mixing single and double quotes, inconsistent indentation, or missing semicolons.

**ESLint** is the standard linter for JavaScript and TypeScript. As the instructor put it during the course, it is *"a library that gives style to the code"*. That is a great one-line summary, but ESLint does even more: beyond style, it protects you from a whole category of small mistakes that would otherwise only reveal themselves at runtime.

Why bother installing one more tool?

- **Catch bugs early.** ESLint can flag a typo like `conts` (instead of `const`) or a variable used before it is defined, right in your editor, before you run the program.
- **Consistency across a team.** When everyone's code follows the same rules, the whole codebase reads as if a single person wrote it. Reviews get faster and arguments about style disappear.
- **Fewer "it works on my machine" surprises.** Rules such as "no unused variables" or "always handle this case" nudge you toward safer code.
- **It teaches you.** Every warning links to documentation explaining *why* a pattern is discouraged. Beginners learn good habits just by fixing lint messages.

Think of it as the automatic version of a senior developer looking over your shoulder and gently saying "you forgot a semicolon here" and "hey, that variable is never used".

## ESLint vs Prettier

Newcomers almost always confuse these two tools, so let's separate them clearly. They solve **different problems** and are commonly used **together**.

- **ESLint is a _linter_.** It cares about **code quality and correctness**: unused variables, undefined names, risky comparisons, and code-style rules. It can *find* problems and, for many of them, automatically *fix* them.
- **Prettier is a _formatter_.** It cares only about **how the code looks**: where the line breaks go, indentation, quote style, trailing commas, maximum line length. Prettier does not understand whether your code is *correct*; it just re-prints it in a consistent shape.

A simple way to remember the difference:

| Concern | Tool | Example it handles |
| --- | --- | --- |
| Is this code **correct / safe**? | **ESLint** (linting) | "You declared `x` but never used it." |
| Does this code **look consistent**? | **Prettier** (formatting) | "Re-indent this block and add a trailing comma." |

There is a small overlap: ESLint *can* enforce some purely visual rules too. Historically that overlap caused conflicts (ESLint and Prettier fighting over the same spacing). The modern, recommended approach is to let each tool do what it is best at: **Prettier handles formatting, ESLint handles code quality**, and you stop ESLint from arguing about formatting.

> Note: The old package `eslint-config-prettier` was commonly used to "turn off" ESLint's formatting rules so Prettier could own them. That approach still works and is still widely used. Whether you add Prettier is optional; ESLint alone is enough to complete this lesson.

## Installing ESLint in a Node project

Remember from the [Node.js lesson](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-5/README.md) that **npm** (Node Package Manager) is how we install libraries into a project. ESLint is just another library we install with npm.

First, make sure you have a Node project. If you are starting from an empty folder, create a `package.json` file with:

```bash
npm init -y
```

The `-y` flag accepts all the defaults so you get a `package.json` right away.

Now, the easiest and most modern way to add ESLint is its **guided setup**. From the root of your project run:

```bash
npm init @eslint/config@latest
```

This launches an interactive wizard that asks a few questions (What do you want to use ESLint for? Which module system? Are you using a framework? JavaScript or TypeScript? Where does your code run — browser or Node?). Based on your answers, it installs ESLint plus any needed packages **and** generates a ready-to-use configuration file for you.

If you prefer to install ESLint by hand instead of using the wizard:

```bash
npm install --save-dev eslint
```

The `--save-dev` flag (shortcut: `-D`) records ESLint under `devDependencies` in your `package.json`. We use `devDependencies` because ESLint is a **development tool** — it is only needed while you are writing code, not when the finished app runs for a user.

You can confirm which version got installed with:

```bash
npx eslint --version
```

> Note: ESLint is **version-sensitive**. This lesson assumes **ESLint v9 or newer**, where the flat config file (`eslint.config.js`) is the default. If you inherit an older project you may see a different setup (see the next section). Always check the version with the command above before copying config from the internet.

## The configuration file

ESLint needs to know **which rules to apply**. That lives in a **configuration file** at the root of your project.

### Flat config (the modern default): `eslint.config.js`

Since ESLint v9, the default configuration format is called **flat config**, and it lives in a file named `eslint.config.js`. It is a normal JavaScript file that **exports an array** of configuration objects. Reading top to bottom, later objects can override earlier ones.

A minimal `eslint.config.js` looks like this:

```js
// eslint.config.js
import js from "@eslint/js";

export default [
  // Start from ESLint's recommended rules
  js.configs.recommended,

  {
    // Which files this configuration applies to
    files: ["**/*.js"],

    // Language options: what JS features / globals to expect
    languageOptions: {
      ecmaVersion: "latest",
      sourceType: "module",
    },

    // Your own rule choices (explained in the next section)
    rules: {
      "no-unused-vars": "warn",
      "no-undef": "error",
      "eqeqeq": "error",
      "semi": ["error", "always"],
      "quotes": ["error", "double"],
    },
  },
];
```

What each part means, in plain language:

- **`files`** — a glob pattern (like the ones we saw for file matching) saying *which* files this block applies to. `"**/*.js"` means "every `.js` file, in any folder".
- **`languageOptions`** — tells ESLint what kind of JavaScript to expect: which language version (`ecmaVersion: "latest"`), and whether you use `import`/`export` modules (`sourceType: "module"`) or classic scripts (`"commonjs"`).
- **`rules`** — the heart of the file. Each key is a **rule name**; each value is how strict to be about it. We cover these values next.
- **`js.configs.recommended`** — a bundle of sensible default rules maintained by the ESLint team, so you do not start from zero.

### Legacy config (older projects): `.eslintrc`

Before flat config, ESLint used files named `.eslintrc.json`, `.eslintrc.js`, `.eslintrc.cjs`, or an `eslintConfig` key inside `package.json`. You will still run into these in existing codebases. A legacy `.eslintrc.json` looks like this:

```json
{
  "root": true,
  "env": { "browser": true, "node": true, "es2021": true },
  "extends": ["eslint:recommended"],
  "parserOptions": { "ecmaVersion": "latest", "sourceType": "module" },
  "rules": {
    "no-unused-vars": "warn",
    "eqeqeq": "error",
    "semi": ["error", "always"]
  }
}
```

> Note: The legacy `.eslintrc` format is now **deprecated**. For any **new** project, use flat config (`eslint.config.js`). Only reach for `.eslintrc` when maintaining an older codebase that already uses it.

## Rules and severity

A **rule** is a single, named check — for example `no-unused-vars` ("do not leave variables that are never used") or `semi` ("require semicolons"). You choose, per rule, **how seriously** ESLint should treat a violation. This is called the rule's **severity**, and there are three levels:

| Severity | Word | Number | What happens |
| --- | --- | --- | --- |
| Off | `"off"` | `0` | The rule is disabled. ESLint ignores it entirely. |
| Warn | `"warn"` | `1` | Reported as a **warning** (yellow). Does **not** fail the command. |
| Error | `"error"` | `2` | Reported as an **error** (red). Makes ESLint exit with a failing code. |

You can write the severity as either the word or the number — both are equivalent:

```js
rules: {
  "no-console": "warn",     // same as 1
  "no-debugger": "error",   // same as 2
  "no-alert": "off",        // same as 0
}
```

Why does the difference between **warn** and **error** matter? Because build systems and automated checks (Continuous Integration) usually **fail** when there is an error but **pass** when there are only warnings. So you might set style preferences to `"warn"` (nice to fix, but not blocking) and genuine bug-risks to `"error"` (must be fixed before the code ships).

### Rules that take options

Some rules need more than just a severity — they take **options**. In that case you use an **array**: the first item is the severity, and the rest are the options.

```js
rules: {
  // "Require semicolons everywhere"
  "semi": ["error", "always"],

  // "Require double quotes for strings"
  "quotes": ["error", "double"],

  // "Indent using 2 spaces"
  "indent": ["error", 2],
}
```

Read `["error", "always"]` as: *"treat violations as an **error**, and my chosen option is **always**"*.

### Turning a rule off for one line

Sometimes you have a good reason to break a rule in exactly one place. You can silence a rule inline with a comment, instead of turning it off for the whole project:

```js
// eslint-disable-next-line no-console
console.log("This one console.log is intentional");
```

Use this sparingly — every disable comment is a small promise that *you* know better than the rule this time.

## Running ESLint from the CLI

Once ESLint is installed and configured, you run it from the terminal. Use `npx` so you run the version installed **in this project** (not some global one):

```bash
# Lint every file ESLint is configured to look at
npx eslint .

# Or lint a specific folder / file
npx eslint src
npx eslint src/index.js
```

If everything is clean, the command prints nothing and exits successfully. If there are problems, you get a report like this:

```
/home/you/project/src/index.js
   3:7   error    'total' is assigned a value but never used   no-unused-vars
   5:1   error    Expected '===' and instead saw '=='          eqeqeq
   8:20  warning  Unexpected console statement                 no-console

✖ 3 problems (2 errors, 1 warning)
  2 errors and 0 warnings potentially fixable with the `--fix` option.
```

Each line tells you the **location** (`line:column`), the **severity**, a **description**, and the **rule name** that fired. Notice the last line: many problems can be fixed **automatically**.

### Auto-fixing with `--fix`

Add the `--fix` flag and ESLint will rewrite your files to fix everything it safely can — missing semicolons, wrong quotes, spacing, and more:

```bash
npx eslint . --fix
```

> Note: `--fix` only fixes problems that are **safe to fix automatically** (mostly style). Real logic bugs, like using an undefined variable, still need a human, ESLint will report them but leave them for you.

### A handy npm script

Instead of typing the command every time, add a **script** to your `package.json`:

```json
{
  "scripts": {
    "lint": "eslint .",
    "lint:fix": "eslint . --fix"
  }
}
```

Now you can simply run:

```bash
npm run lint       # report problems
npm run lint:fix   # report and auto-fix
```

## Editor integration and format-on-save

Running ESLint in the terminal is useful, but the real magic is seeing problems **live, inside your editor**, and having them fixed the moment you press save. During the course we used [**Visual Studio Code**](https://code.visualstudio.com/), so we will describe the setup there.

**1. Install the ESLint extension.**

1. Open VS Code.
2. Click the **Extensions** icon in the left sidebar (the four little squares), or press `Ctrl+Shift+X`.
3. Type **ESLint** in the search box.
4. Choose the extension published by **Microsoft** (named "ESLint") and click **Install**.

Once installed, the extension reads your project's `eslint.config.js` automatically and **underlines problems** directly in your code with squiggly lines. Hover over a squiggle to read the message and the rule name — no need to run anything in the terminal to see it.

**2. Turn on fix-on-save.**

This is exactly the setup the instructor described in class: *VS Code is configured to automatically resolve ESLint problems every time you save the file*. You get this by adding a couple of settings.

In VS Code, open your settings as JSON:

1. Press `Ctrl+Shift+P` to open the **Command Palette**.
2. Type **Preferences: Open User Settings (JSON)** and select it.

Then add (or merge in) these settings:

```json
{
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  }
}
```

- **`editor.formatOnSave`** tells VS Code to format the file whenever you save it.
- **`editor.codeActionsOnSave` → `source.fixAll.eslint`** tells the ESLint extension to run its auto-fixes on save.

With this in place, every time you hit `Ctrl+S`, ESLint quietly cleans up your file, fixing quotes, semicolons, spacing, and any other auto-fixable rule, so you can focus on logic instead of housekeeping.

> Note: You can also apply these settings **per project** instead of globally by putting them in a `.vscode/settings.json` file at the root of the repository. That way each project can have its own behavior, and teammates who open the project inherit the same setup.

## Shareable configs (Airbnb, Standard)

Writing every rule yourself is a lot of work, and you would spend forever deciding "semicolons or not?", "single or double quotes?". To avoid **reinventing the wheel**, the community publishes **shareable configs**: pre-packaged sets of rules you can adopt in one line. You install the config as an npm package and reference it from your configuration.

Two of the most famous:

- **Airbnb** — a large, opinionated, fairly strict style guide widely used in industry. It enforces a lot of best practices, which is great for learning, though it can feel picky at first. See the [**Airbnb JavaScript Style Guide**](https://github.com/airbnb/javascript).
- **Standard** — a "zero-configuration" style with strong opinions (famously: **no semicolons**). You do not tweak it; you just adopt it as-is. See [**StandardJS**](https://standardjs.com/).

The idea is simple: instead of hand-picking dozens of rules, you extend a config that already encodes a whole team's collective experience, then override just the few rules you disagree with.

> Note: These shareable configs each have their own installation steps and their own pace of support for the newer flat-config format. Always follow the **current** instructions on the config's official page for the ESLint version you are using, rather than copying an old snippet.

## Module Activity

Set up ESLint from scratch in a small Node project and watch it catch a real mistake.

1. Create a new folder and initialize a project:

   ```bash
   npm init -y
   ```

2. Add ESLint using the guided setup (choose **JavaScript**, **ES modules**, running in **Node**, no framework):

   ```bash
   npm init @eslint/config@latest
   ```

3. Open your generated `eslint.config.js` and make sure the `rules` block includes at least these:

   ```js
   rules: {
     "no-unused-vars": "warn",
     "eqeqeq": "error",
     "semi": ["error", "always"],
     "quotes": ["error", "double"],
   }
   ```

4. Create a file `index.js` that **breaks several rules on purpose** (this is a Star Wars–flavored version of the course examples):

   ```js
   const jedi = 'Luke'
   const unused = 'this variable is never used'

   function greet(name) {
     if (name == 'Luke') {
       console.log('Hello there, ' + name)
     }
   }

   greet(jedi)
   ```

   This file has: single quotes (should be double), missing semicolons, an unused variable, and `==` instead of `===`.

5. Run the linter and read the report carefully:

   ```bash
   npx eslint index.js
   ```

   You should see errors for the quotes, missing semicolons, and `==`, plus a warning for the unused variable.

6. Now auto-fix what can be fixed:

   ```bash
   npx eslint index.js --fix
   ```

   Open the file again — the quotes, semicolons, and spacing are now clean. Notice that `no-unused-vars` and `eqeqeq` were **not** auto-fixed: ESLint won't guess your intent for those. Fix them by hand (remove `unused`, and change `==` to `===`), then run `npx eslint index.js` once more and confirm it reports no problems.

7. **Bonus:** Install the VS Code **ESLint** extension, add the fix-on-save settings from the previous section, re-introduce a broken line (e.g., change a `"` back to a `'`), and watch it repair itself the instant you save.

**Reflection:** Compare how quickly you spotted the `==` bug with ESLint versus how long it might have taken to notice it only after the program misbehaved at runtime. That early feedback is the whole point of linting.

## Sources

- [**ESLint — Official Documentation**](https://eslint.org/docs/latest/)
- [**ESLint — Getting Started**](https://eslint.org/docs/latest/use/getting-started)
- [**ESLint — Configuration Files (flat config)**](https://eslint.org/docs/latest/use/configure/configuration-files)
- [**ESLint — Configure Rules and severities**](https://eslint.org/docs/latest/use/configure/rules)
- [**ESLint — Command Line Interface (`--fix`)**](https://eslint.org/docs/latest/use/command-line-interface)
- [**Prettier — Documentation**](https://prettier.io/docs/)
- [**Prettier vs. Linters**](https://prettier.io/docs/comparison)
- [**Visual Studio Code — ESLint extension (Marketplace)**](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- [**Visual Studio Code — User and Workspace Settings**](https://code.visualstudio.com/docs/getstarted/settings)
- [**Airbnb JavaScript Style Guide**](https://github.com/airbnb/javascript)
- [**StandardJS**](https://standardjs.com/)
- [**MDN — JavaScript**](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
