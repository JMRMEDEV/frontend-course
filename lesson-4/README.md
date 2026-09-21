# React

[**React**](https://react.dev/) is a **library** for building user interfaces out of small, reusable pieces called **components**. It was created by **Facebook (Meta)** and it powers a huge part of the modern web and, through **React Native**, a huge part of mobile apps too.

In the previous lessons we learned **HTML** (structure), **CSS** (styling) and **JavaScript** (behavior). React sits on top of all three: you keep using your HTML and CSS knowledge, but instead of manually reaching into the page with `document.getElementById` (like we did in the JavaScript lesson), React lets you **describe** what the UI should look like for a given set of data, and it takes care of updating the real page for you.

> **A note on this lesson.** This lesson is longer than the previous ones because React is a big topic. It is organized into clearly separated areas (A–I), the same way the live sessions are. You do not have to absorb everything at once, treat it as a reference you can come back to. Wherever the ecosystem has moved on since this material was first written, you will find a **Modern note** callout pointing at the up-to-date way of doing things (this lesson targets **React 19**).

## Module Content

- [A. React: library or framework?](#a-react-library-or-framework)
- [B. React benefits & drawbacks](#b-react-benefits--drawbacks)
- [C. React vs Angular vs Vue](#c-react-vs-angular-vs-vue)
- [D. Where is React used?](#d-where-is-react-used)
- [E. React features](#e-react-features)
  - [Virtual DOM](#virtual-dom)
  - [JSX](#jsx)
  - [Components](#components)
  - [Class vs functional components](#class-vs-functional-components)
  - [Component lifecycle](#component-lifecycle)
  - [Props](#props-properties)
  - [State](#state)
  - [Context API](#context-api)
  - [Hooks](#hooks)
  - [Forms](#forms)
- [F. React + TypeScript + ESLint](#f-react--typescript--eslint)
- [G. Advanced React](#g-advanced-react)
- [H. Frameworks & libraries](#h-frameworks--libraries)
- [I. References](#i-references)

## A. React: library or framework?

One of the first questions people ask is: *is React a **library** or a **framework**?* The two words are often used as if they meant the same thing, but there is a real difference, and it comes down to a concept called **inversion of control**.

- When you use a **library**, *you* are in control. Your code decides **where** and **when** the library is called. You call it; it does a job; it hands control back to you.
- When you use a **framework**, the **framework** is in control. You fill in your code in the slots the framework gives you, and the framework decides **when** those slots run. (People often summarize this as the "Hollywood principle": *don't call us, we'll call you*.)

By that definition, **React is a library**. You decide where to render it and when to call its features; it does not dictate the overall shape of your application the way a full framework (like Angular) does. This is also why React pairs with so many other tools, routing, data fetching, and build tooling are all choices *you* make, not things React forces on you.

> **Modern note.** You will still hear people casually call React a "framework", and that is fine in everyday conversation. The library-vs-framework distinction matters most when you compare React to Angular (a full framework) further down. Tools built *on top of* React, like **Next.js**, are frameworks in their own right.

## B. React benefits & drawbacks

No tool is all upside. Here is an honest look at what you gain and what you pay for when you choose React.

**Benefits**

- **Component-based architecture** — build your UI from small, reusable, composable pieces.
- **Virtual DOM** — React updates the real page efficiently (more on this below).
- **JSX** — write HTML-like markup right next to the logic that drives it.
- **Unidirectional data flow** — data flows down in one direction, which makes apps easier to reason about.
- **Single Page Applications (SPA)** — smooth, app-like experiences without full page reloads.
- **Open source & community support** — a massive community, so answers and packages are everywhere.
- **Vast ecosystem** — there is a library for almost anything you need.

**Drawbacks**

- **Learning curve** — JSX, hooks, and "thinking in React" take time to click.
- **Complexity** — a real app pulls in routing, state management, tooling, and more.
- **Vast ecosystem** — yes, this appears on *both* lists on purpose: the huge number of choices is a blessing when you know what you want and a burden when you do not ("which router? which state library?").
- **It is JavaScript** — you inherit JavaScript's quirks (remember the "untyped freedom is also its worst feature" point from the JavaScript lesson).
- **Constant changes** — React and its ecosystem move quickly; material can go out of date (which is exactly why this lesson has *Modern note* callouts).

## C. React vs Angular vs Vue

React is not the only option. The three most talked-about choices are **React**, **Angular**, and **Vue**. A useful mental model: **React is a library** you assemble with other pieces, **Angular is a full framework** that comes with almost everything built in, and **Vue** sits in between (a "progressive framework" you can adopt gradually).

Rather than declare a winner, here is what each is known for.

**React** — component-based architecture, Virtual DOM, JSX, unidirectional data flow, a reconciliation algorithm, declarative syntax, hooks, server-side rendering, static site generation, props and state, conditional rendering, and reusability.

**Angular** — two-way data binding, directives, dependency injection, an MVVM architecture, templates, built-in routing, services and factories, filters, form validation, testing support, animation support, internationalization/localization, and third-party integration.

**Vue** — declarative rendering, component-based architecture, Virtual DOM, directives, two-way data binding, watchers, lifecycle hooks, reactivity, event handling, transition/animation support, custom directives, routing, and server-side rendering.

Notice the overlap: all three use a component model and (React and Vue especially) a Virtual DOM. The biggest philosophical split is **how much the tool decides for you**, Angular decides a lot, React decides very little, Vue lets you choose how much.

## D. Where is React used?

If you are wondering whether learning React is worth it: it is used by a huge number of the apps you already use every day. A few well-known examples:

- Facebook, Instagram
- Airbnb
- Discord, Twitch
- Netflix
- Duolingo
- Dropbox, Spotify
- Microsoft (Outlook, Teams)

And through **React Native** (covered in area H), the same skills reach mobile apps too. Learning React opens doors on both web and mobile.

## E. React features

This is the heart of the lesson. We will go through the features that make React what it is, one at a time, with runnable code you can paste into a sandbox.

> **Tip.** As with the earlier lessons, the easiest place to try this out is [**CodeSandbox**](https://codesandbox.io). Create a new **React** sandbox and you get a working project instantly, no local setup required.

### Virtual DOM

The **Virtual DOM (VDOM)** is a programming concept where a *"virtual"* representation of the UI is kept in memory and kept in sync with the *"real"* DOM.

Why does this matter? Remember from the JavaScript lesson that touching the real DOM (`document.getElementById(...).innerHTML = ...`) is how we change the page. Doing that by hand, over and over, is both tedious and slow if done carelessly. React's idea is:

1. You describe what the UI *should* look like for the current data.
2. React builds a lightweight virtual copy of that UI in memory.
3. When the data changes, React builds a new virtual copy, **compares** it to the previous one (a process called **reconciliation**), and figures out the **smallest set of real changes** needed.
4. React applies only those minimal changes to the real DOM.

The result: you write simple "this is what it should look like" code, and React does the fiddly, performance-sensitive DOM updates for you.

### JSX

**JSX** is a syntax extension for JavaScript that lets us write **HTML-like markup inside a JavaScript file**. Instead of keeping your markup in one file and the logic that drives it somewhere else, JSX lets rendering logic and markup live together in the same place: the **component**.

Here is what JSX looks like:

```jsx
const element = <h1>Hello, world!</h1>;
```

That is not a string and it is not HTML, it is JSX, and React turns it into real elements for you. A few rules that trip up beginners:

- Use `className` instead of `class` (because `class` is a reserved word in JavaScript).
- Every tag must be closed, including self-closing ones: `<img />`, `<br />`.
- To drop a JavaScript value into the markup, wrap it in **curly braces**: `<h1>Hello, {name}!</h1>`.
- A component must return a **single** top-level element. If you need to return several siblings without adding an extra `<div>`, wrap them in an empty **fragment**: `<>...</>`.

### Components

**Components are the fundamental building blocks of React applications.** They encapsulate UI elements, behavior, and logic, and they can be **reused** and **composed** to build up complex interfaces from simple parts.

A component is, at heart, just a JavaScript function that returns some JSX:

```jsx
function Welcome() {
  return <h1>Hello, world!</h1>;
}
```

You then use it like a tag: `<Welcome />`. Notice the **capital letter**, React treats lowercase tags as plain HTML (`<div>`) and capitalized tags as your components (`<Welcome />`).

### Class vs functional components

React components come in two flavors, and there is some history here worth knowing.

Originally, React was designed with the **Object-Oriented Programming (OOP)** paradigm in mind, and the first components were **class components**. These required the `class` reserved word and extended `Component` from React.

With **React 16.8** (released in 2019), **hooks** were introduced. Hooks let you build an entire React application with **functional components** (embracing a more functional programming style). Since then, functional components have become the **preferred approach**, and the React team itself recommends them.

Here is the quick contrast:

| Class components | Functional components |
| --- | --- |
| use `this` | use **hooks** |
| no `const` / no `function` for the component body | `useState`, `useEffect`, ... |
| lifecycle methods: `componentDidMount`, `componentDidUpdate`, `componentWillUnmount` | one `useEffect` covers those cases |
| need `constructor`, `super`, and `bind` | defined as `const Comp = () => {}` |
| OOP style | functional style |

> **Modern note.** You will still *see* class components in older codebases, so it is good to recognize them. But for new code, **write functional components with hooks**. The rest of this lesson uses functional components except where we explicitly show the old class approach for comparison.

### Component lifecycle

Every component goes through a **lifecycle**: it is created and inserted into the page (**mounting**), it re-renders when its data changes (**updating**), and eventually it is removed (**unmounting**).

**In class components**, these phases were handled by named methods, called in this order:

- **Mounting:** `constructor()` → `render()` → `componentDidMount()`
- **Updating:** `render()` → `componentDidUpdate()` (triggered by new props, `setState()`, etc.)
- **Unmounting:** `componentWillUnmount()`

**In functional components**, the single `useEffect` hook covers all of these cases. For example, this effect runs once when the component mounts (like `componentDidMount`), and its returned function runs when the component unmounts (like `componentWillUnmount`):

```jsx
// useEffect as componentDidMount + componentWillUnmount
useEffect(() => {
  console.log("Component did mount");

  // Setup a timer to update the count every second
  const timerId = setInterval(() => {
    setCount((prevCount) => prevCount + 1);
  }, 1000);

  // Return a cleanup function to clear the timer when the component unmounts
  return () => {
    clearInterval(timerId);
    console.log("Component will unmount");
  };
}, []);
```

And this effect runs whenever `count` changes (like `componentDidUpdate` for that value):

```jsx
// useEffect as componentDidUpdate (for `count`)
useEffect(() => {
  console.log("Component did update");
}, [count]);
```

We will look at `useEffect` and its **dependency array** more closely in the [Hooks](#hooks) section, that little `[]` vs `[count]` at the end is the key to controlling *when* an effect runs.

### Props (properties)

React components use **props** to communicate with each other. Every **parent** can pass information down to its **children** by giving them props. Props are like HTML attributes, but you can pass **any JavaScript value** through them, not just strings: numbers, arrays, objects, and even functions.

Let's build an `Avatar` component that receives a `user` object and a `handleClick` function as props:

```jsx
// Avatar.jsx
export const Avatar = (props) => {
  const { user, handleClick } = props;

  const WIDTH = "200px";

  return (
    <img
      alt={user.name}
      src={user.profilePicture}
      width={WIDTH}
      onClick={() => handleClick(user.id)}
    />
  );
};
```

And here is a parent that creates the data and passes it down:

```jsx
// AvatarParent.jsx
import { Avatar } from "./Avatar";

export const AvatarParent = () => {
  const user = {
    name: "Luke Skywalker",
    profilePicture:
      "https://static.wikia.nocookie.net/starwars/images/3/3d/LukeSkywalker.png",
    id: "20230831-501",
  };

  const handleClick = (id) => {
    console.log("The selected id was: ", id);
  };

  return (
    <div style={{ backgroundColor: "pink" }}>
      <Avatar user={user} handleClick={handleClick} />
    </div>
  );
};
```

A couple of things to notice:

- The parent passes `user={user}` and `handleClick={handleClick}`. Those curly braces mean "pass this JavaScript value", the object and the function travel down as props.
- `style={{ backgroundColor: "pink" }}` looks like double braces for a reason: the **outer** braces say "here comes a JavaScript value", and the **inner** braces are a JavaScript **object** describing the styles. (Also note `backgroundColor` in camelCase, not `background-color`, because it is a JS object key.)

#### Reading props: two styles

Inside the child you can read props in two equivalent ways. Both of these `Avatar` variants do exactly the same thing:

```jsx
// Alternative A: destructure in the parameter list
export const AvatarAlternativeA = ({ user, handleClick }) => {
  const WIDTH = "200px";

  return (
    <img
      alt={user.name}
      src={user.profilePicture}
      width={WIDTH}
      onClick={() => handleClick(user.id)}
    />
  );
};
```

```jsx
// Alternative B: keep `props` and reach into it with props.something
export const AvatarAlternativeB = (props) => {
  const WIDTH = "200px";

  return (
    <img
      alt={props.user.name}
      src={props.user.profilePicture}
      width={WIDTH}
      onClick={() => props.handleClick(props.user.id)}
    />
  );
};
```

Most developers prefer **Alternative A** (destructuring) because it is shorter and makes the component's expected props obvious at a glance.

#### The built-in `children` prop

There is one special prop you get for free: **`children`**. Whatever you place *between* a component's opening and closing tags is handed to it as `children`, so a component can wrap and render content it doesn't know about in advance:

```jsx
// AvatarWithChildren.jsx
export const AvatarWithChildren = (props) => {
  const { user, handleClick, children } = props;

  const WIDTH = "200px";

  return (
    <>
      <img
        alt={user.name}
        src={user.profilePicture}
        width={WIDTH}
        onClick={() => handleClick(user.id)}
      />
      {children}
    </>
  );
};
```

Used from a parent like this:

```jsx
<AvatarWithChildren user={user} handleClick={handleClick}>
  <span>I'm the built in children</span>
</AvatarWithChildren>
```

The `<span>I'm the built in children</span>` shows up wherever the component renders `{children}`. So the first example renders just Luke's avatar, and this one renders the avatar **plus** the "I'm the built in children" text underneath.

### State

Props flow *down* from a parent and, from the child's point of view, don't change on their own. But components often need to **change based on interactions**: typing should update an input, clicking "next" should change the image in a carousel, and so on. Components need to **"remember"** things between interactions. That component-specific memory is called **state**.

Let's start with a gallery that shows one sculpture at a time and a "Next" button. Here is a first attempt using a plain variable:

```jsx
// regular-variable-example.jsx
import { sculptureList } from "./data.js";

export default function Gallery() {
  let index = 0;

  function handleClick() {
    index = index + 1;
  }

  let sculpture = sculptureList[index];
  return (
    <>
      <button onClick={handleClick}>Next</button>
      <h2>
        <i>{sculpture.name} </i>
        by {sculpture.artist}
      </h2>
      <h3>
        ({index + 1} of {sculptureList.length})
      </h3>
      <img src={sculpture.url} alt={sculpture.alt} />
      <p>{sculpture.description}</p>
    </>
  );
}
```

**This example won't work.** Clicking "Next" seems like it should advance `index`, but the screen never changes. The `handleClick` handler *is* updating the local variable `index`, but two things prevent that change from being visible:

1. **Local variables don't persist between renders.** When React renders this component a second time, it renders it from scratch, it doesn't consider any changes to the local variables.
2. **Changes to local variables won't trigger renders.** React doesn't realize it needs to render the component again with the new data.

So to update a component with new data, two things need to happen:

1. **Retain** the data between renders.
2. **Trigger** React to render the component with the new data (re-rendering).

State does both. Let's see the two ways to add it.

#### State: the classic (class component) approach

Before hooks, state lived in **class components** via `this.state` and `this.setState`:

```jsx
// classic-state-example.jsx
import React, { Component } from "react";
import { sculptureList } from "./data.js";

class Gallery extends Component {
  constructor(props) {
    super(props);
    this.state = {
      index: 0,
    };
  }

  handleClick = () => {
    this.setState((prevState) => ({
      index: prevState.index + 1,
    }));
  };

  render() {
    const { index } = this.state;
    const sculpture = sculptureList[index];

    return (
      <>
        <button onClick={this.handleClick}>Next</button>
        <h2>
          <i>{sculpture.name} </i>
          by {sculpture.artist}
        </h2>
        <h3>
          ({index + 1} of {sculptureList.length})
        </h3>
        <img src={sculpture.url} alt={sculpture.alt} />
        <p>{sculpture.description}</p>
      </>
    );
  }
}

export default Gallery;
```

Notice `this.setState((prevState) => ({ index: prevState.index + 1 }))`. Calling `setState` is what **triggers a re-render**, and `this.state` **persists** between renders. This solves both problems, but it is verbose: a constructor, `super(props)`, `this` everywhere.

#### State: `useState`

The modern, functional way is the **`useState`** hook. The same gallery becomes much shorter:

```jsx
// use-state-example.jsx
import { useState } from "react";
import { sculptureList } from "./data.js";

export default function Gallery() {
  const [index, setIndex] = useState(0);

  function handleClick() {
    setIndex(index + 1);
  }

  let sculpture = sculptureList[index];
  return (
    <>
      <button onClick={handleClick}>Next</button>
      <h2>
        <i>{sculpture.name} </i>
        by {sculpture.artist}
      </h2>
      <h3>
        ({index + 1} of {sculptureList.length})
      </h3>
      <img src={sculpture.url} alt={sculpture.alt} />
      <p>{sculpture.description}</p>
    </>
  );
}
```

The line `const [index, setIndex] = useState(0)` is the key. `useState(0)` sets the **initial value** to `0` and returns two things: the **current value** (`index`) and a **function to update it** (`setIndex`). Calling `setIndex(index + 1)` both remembers the new value and tells React to re-render. Now "Next" actually advances the gallery. We'll come back to `useState` in the [Hooks](#hooks) section.

### Context API

Passing props down works great between a parent and its direct children. But sometimes you need to get a value to a component **deep** in the tree, and threading it through every component in between (this is nicknamed **"prop drilling"**) becomes verbose and inconvenient, especially if many components need the same information.

The **Context API** lets a parent make some information available to **any** component in the tree below it, no matter how deep, without passing it explicitly through props. There are three steps:

1. **Create** a context.
2. **Provide** that context from a component (so the value is available below it).
3. **Use** that context from any component that needs the data.

```jsx
// context-example.jsx
import React, { createContext, useContext } from "react";

// Step 1: Create a context
const ThemeContext = createContext();

// Step 2: Create a component that provides the context
function ThemeProvider({ children }) {
  const theme = "light"; // You can set the theme dynamically here
  return (
    <ThemeContext.Provider value={theme}>{children}</ThemeContext.Provider>
  );
}

// Step 3: Create a component that consumes the context
function ThemeComponent() {
  const theme = useContext(ThemeContext);
  return <p>Current Theme: {theme}</p>;
}

function App() {
  return (
    <ThemeProvider>
      <div>
        <h1>React Context Example</h1>
        <ThemeComponent />
      </div>
    </ThemeProvider>
  );
}

export default App;
```

`ThemeComponent` reads the theme with `useContext(ThemeContext)` even though nobody passed it a `theme` prop, it picks it up from the nearest `ThemeContext.Provider` above it. That's the whole point of context: skip the drilling.

> **Modern note.** In **React 19** you can render the context object directly as the provider, `<ThemeContext value={theme}>` instead of `<ThemeContext.Provider value={theme}>`. The `.Provider` form shown above still works, so either is fine; the shorter form is the new recommendation.

### Hooks

**Hooks** were introduced in **React 16.8**. They are special functions that give **functional components** access to React features that used to require class components, things like state handling and lifecycle behavior.

Before the individual hooks, three **rules** you must follow:

1. Hooks can only be called inside **React function components** (they will not work in class components).
2. Hooks can only be called at the **top level** of a component.
3. Hooks **cannot be conditional** (don't call a hook inside an `if`, a loop, or a nested function).

You *can* call the same hook multiple times in one component (for example, several `useEffect` calls).

Now let's meet the hooks you will use most.

#### `useEffect`

The `useEffect` hook lets you perform **side effects** in your components. Typical side effects are **fetching data, directly updating the DOM, and timers**.

`useEffect` accepts two arguments (the second is optional):

```jsx
useEffect(<function>, <dependency>)
```

The **dependency array** is what controls *how often* the effect runs. There are three cases, and understanding them prevents a lot of beginner bugs:

```jsx
// 1. No dependency array passed:
useEffect(() => {
  // Runs on every render
});

// 2. An empty array:
useEffect(() => {
  // Runs only on the first render
}, []);

// 3. Props or state values in the array:
useEffect(() => {
  // Runs on the first render
  // And any time any dependency value changes
}, [prop, state]);
```

#### `useState`

The `useState` hook lets us **track state in a function component**. (State, again, is data or properties that need to be tracked in an application.)

We initialize state by calling `useState` at the **top** of the component. It accepts an **initial state** and returns two values: the **current state** and a **function that updates it**.

```jsx
import { useState } from "react";
import ReactDOM from "react-dom/client";

function FavoriteColor() {
  const [color, setColor] = useState("red");

  return (
    <>
      <h1>My favorite color is {color}!</h1>
      <button type="button" onClick={() => setColor("blue")}>
        Blue
      </button>
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<FavoriteColor />);
```

Here `useState("red")` starts `color` at `"red"`. Clicking the button calls `setColor("blue")`, which updates the value **and** re-renders, so the heading changes to "My favorite color is blue!".

#### `useCallback`

The `useCallback` hook returns a **memoized callback function**. Think of memoization as **caching** a value so it does not need to be recalculated. This lets you isolate resource-intensive work so it does not run on every render; `useCallback` only re-creates the function when one of its dependencies changes, which can improve performance.

The classic use is passing a stable function down to a child so the child doesn't re-render unnecessarily:

```jsx
// ChildComponent.jsx
import React from "react";

function ChildComponent({ onIncrement }) {
  console.log("Child component rendered");
  return <button onClick={onIncrement}>Increment</button>;
}

export default ChildComponent;
```

```jsx
// parent.jsx
import React, { useState, useCallback } from "react";
import ChildComponent from "./ChildComponent";

function ParentComponent() {
  const [count, setCount] = useState(0);

  // Define a callback function using useCallback
  const increment = useCallback(() => {
    setCount((prevCount) => prevCount + 1);
  }, []);

  return (
    <div>
      <p>Count: {count}</p>
      <ChildComponent onIncrement={increment} />
    </div>
  );
}

export default ParentComponent;
```

What's happening here:

1. `ParentComponent` defines a callback named `increment` using `useCallback`. This function increments the `count` state.
2. `increment` is passed as a prop to `ChildComponent`.
3. `ChildComponent` receives it as `onIncrement`.
4. Clicking the button in the child invokes `onIncrement`, and `count` updates in the parent.

Using `useCallback` here ensures the `increment` function keeps the **same identity** between renders of the parent. Without it, a **new** function instance would be created on every render, potentially causing unnecessary re-renders in the child.

#### `useRef`

The `useRef` hook lets you **persist values between renders**. It has two common uses:

- Store a **mutable value that does not cause a re-render** when it is updated (unlike state).
- **Access a DOM element directly** (a rare but sometimes necessary escape hatch, e.g. to focus an input).

```jsx
import { useRef } from "react";

function TextInputWithFocus() {
  const inputRef = useRef(null);

  const focusInput = () => {
    inputRef.current.focus(); // reach the real DOM node
  };

  return (
    <>
      <input ref={inputRef} />
      <button onClick={focusInput}>Focus the input</button>
    </>
  );
}
```

The value lives on `inputRef.current`. Changing `.current` does **not** trigger a re-render, which is exactly why refs are used for things that shouldn't cause the UI to redraw.

#### `useMemo`

The `useMemo` hook returns a **memoized value**. Same idea as `useCallback` (caching so you don't recalculate), but for a **computed value** rather than a function. It only re-runs when one of its dependencies changes, which can improve performance for expensive calculations.

In the example below, the expensive function only runs when `count` changes, **not** when a todo is added:

```jsx
import { useState, useMemo } from "react";
import ReactDOM from "react-dom/client";

const App = () => {
  const [count, setCount] = useState(0);
  const [todos, setTodos] = useState([]);
  const calculation = useMemo(() => expensiveCalculation(count), [count]);

  const increment = () => {
    setCount((c) => c + 1);
  };
  const addTodo = () => {
    setTodos((t) => [...t, "New Todo"]);
  };

  return (
    <div>
      <div>
        <h2>My Todos</h2>
        {todos.map((todo, index) => {
          return <p key={index}>{todo}</p>;
        })}
        <button onClick={addTodo}>Add Todo</button>
      </div>
      <hr />
      <div>
        Count: {count}
        <button onClick={increment}>+</button>
        <h2>Expensive Calculation</h2>
        {calculation}
      </div>
    </div>
  );
};

const expensiveCalculation = (num) => {
  console.log("Calculating...");
  for (let i = 0; i < 1000000000; i++) {
    num += 1;
  }
  return num;
};

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<App />);
```

Without `useMemo`, that one-billion-iteration loop would run on **every** render, including when you just add a todo. With `useMemo(() => expensiveCalculation(count), [count])`, it only re-runs when `count` actually changes.

> **Modern note: the React Compiler.** React 19 introduced the **React Compiler**, which can automatically memoize your components and values at build time. As it becomes standard, a lot of manual `useMemo` and `useCallback` becomes unnecessary, the compiler figures out what to cache for you. It is still worth understanding these hooks (you will see them in existing code, and the mental model of memoization is important), but don't feel you must sprinkle them everywhere in new code.

#### `useReducer`

The `useReducer` hook is similar to `useState`, but for **more complex state logic**. If you find yourself tracking multiple pieces of state that change together according to some rules, `useReducer` can be cleaner.

It works with a **reducer function** (which contains your custom state logic) and an **initial state** (a simple value, but usually an object). It returns the **current state** and a **`dispatch`** function you call to request changes:

```jsx
// use-reducer-example.jsx
import React, { useReducer } from "react";

// Reducer function
const reducer = (state, action) => {
  switch (action.type) {
    case "INCREMENT":
      return { count: state.count + 1 };
    case "DECREMENT":
      return { count: state.count - 1 };
    default:
      return state;
  }
};

function ReducerExample() {
  // Initial state and dispatch function from useReducer
  const initialState = { count: 0 };
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: "INCREMENT" })}>Increment</button>
      <button onClick={() => dispatch({ type: "DECREMENT" })}>Decrement</button>
    </div>
  );
}

export default ReducerExample;
```

Instead of calling a setter directly, you **dispatch an action** (like `{ type: "INCREMENT" }`), and the reducer decides how the state should change in response. This pattern scales nicely as state logic grows.

### Forms

With React, you can add **forms** just like any other HTML elements:

```jsx
function MyForm() {
  return (
    <form>
      <label>
        Enter your name:
        <input type="text" />
      </label>
    </form>
  );
}
```

But a form usually needs to *do* something with what the user types. There are two approaches: **uncontrolled** and **controlled** forms.

#### Uncontrolled forms

In an **uncontrolled** form, the form data and form state are managed by the **DOM itself**, rather than by React's component state. These can be useful when you want to take advantage of native form handling and avoid the overhead of managing form state in React. You read the value out of the DOM when you need it, typically with a **ref**:

```jsx
// uncontrolled-form-example.jsx
import React, { useRef } from "react";

function MyForm() {
  const nameInputRef = useRef(null);

  // Handle form submission
  const handleSubmit = (event) => {
    event.preventDefault();
    const name = nameInputRef.current.value;
    console.log("Submitted name:", name);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Enter your name:
        <input type="text" ref={nameInputRef} />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
}

export default MyForm;
```

Notice `event.preventDefault()`, that stops the browser's default "reload the page on submit" behavior. The value is read from the DOM through `nameInputRef.current.value` only at submit time.

#### Controlled forms

In a **controlled** form, **React** manages the form state. Each input's value is driven by state, and every keystroke updates that state through `onChange`. This is more code than an uncontrolled form, but it unlocks more advanced features, validation, dynamic behavior, and easy integration with the rest of your application's state, and it is more maintainable for complex forms.

```jsx
// controlled-form-example.jsx
import React, { useState } from "react";

function ControlledForm() {
  const [name, setName] = useState("");

  const handleSubmit = (event) => {
    event.preventDefault();
    console.log("Submitted name:", name);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Enter your name:
        <input
          type="text"
          value={name}
          onChange={(event) => setName(event.target.value)}
        />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
}

export default ControlledForm;
```

The important line is `value={name}` combined with `onChange={(event) => setName(event.target.value)}`. The input **displays** the state, and typing **updates** the state, so React is always the single source of truth for what's in the box. This is the approach you will reach for most of the time.

## F. React + TypeScript + ESLint

Two tools dramatically improve the quality of a React codebase: **TypeScript** (types) and **ESLint** (linting). We touched on types back in the JavaScript lesson, remember how JavaScript's "freedom" of not declaring types was called its worst feature? TypeScript is the answer to that.

### React + TypeScript

When you use **TypeScript** with React, you can **enforce types**, which translates into more maintainable, clear, and predictable code that prevents many bugs. React provides a TypeScript template out of the box, along with type definitions.

Let's revisit our `Avatar` example, this time typed. First, we describe the shape of a user in its own definition file:

```ts
// user.d.ts
export interface IUser {
  /**
   * Full name of the user.
   */
  name: string;
  /**
   * Picture associated to user.
   */
  profilePicture?: string;
  /**
   * Unique identifier for the user.
   */
  id: string;
}
```

The `?` on `profilePicture?` means it is **optional**, `name` and `id` are required, but a user might not have a picture. Now the parent, in TypeScript:

```tsx
// AvatarParent.tsx
import React from "react";
import { Avatar } from "./Avatar";
import { IUser } from "./user.d";

export const AvatarParent: React.FC = (): JSX.Element => {
  const user: IUser = {
    name: "Luke Skywalker",
    profilePicture:
      "https://static.wikia.nocookie.net/starwars/images/3/3d/LukeSkywalker.png",
    id: "20230831-501",
  };

  const handleClick = (id: string): void => {
    console.log("The selected id was: ", id);
  };

  return (
    <div style={{ backgroundColor: "pink" }}>
      <Avatar user={user} handleClick={handleClick} />
    </div>
  );
};
```

Compare this with the plain-JavaScript version from the [Props](#props-properties) section. The logic is identical, but now:

- `user: IUser` guarantees the object has the right shape, if you forget `id` or misspell `name`, TypeScript tells you *before* you run the code.
- `handleClick = (id: string): void` says this function takes a string and returns nothing.
- The file extensions change: `.jsx` becomes `.tsx` for files with JSX, and `.ts` for plain TypeScript.

> **Modern note.** The `React.FC` type shown here works, but the current community leaning is to **type the props object directly** and skip `React.FC` (it has some historical rough edges). A modern equivalent would be `export const AvatarParent = (): JSX.Element => { ... }` with props typed as their own interface. Either style is acceptable, `React.FC` is not wrong, just no longer the default recommendation.

### React + ESLint

**ESLint** analyzes your code for problems and style violations. With React-specific plugins it can enforce best practices for React specifically.

The `eslint-plugin-react` plugin offers rules such as:

- `react/prop-types` — enforce the usage of `propTypes` for props validation.
- `react/jsx-key` — enforce providing a unique `key` for elements rendered from arrays.

> **Modern note: `propTypes` is gone.** In older React you validated props at runtime with a `propTypes` object, and `react/prop-types` enforced it. **As of React 19, `propTypes` is deprecated and removed from React itself.** If you are using **TypeScript** (as above), you don't need `propTypes` at all, your types already validate props, and they do it at compile time, which is better. For a modern React + TypeScript project, you can skip the `react/prop-types` rule entirely.

The `eslint-plugin-jsx-a11y` plugin adds **accessibility** rules, such as:

- `jsx-a11y/alt-text` — enforce meaningful `alt` text on images.
- `jsx-a11y/label-has-associated-control` — ensure form labels are associated with an input.

For projects using hooks, `eslint-plugin-react-hooks` enforces the rules of hooks we listed earlier:

- `react-hooks/rules-of-hooks` — ensure hooks are used correctly (top level, not conditional).
- `react-hooks/exhaustive-deps` — ensure all dependencies are listed in a `useEffect` dependency array.

ESLint can also enforce **naming conventions** and **formatting**:

- naming: `camelCase` for variables, `PascalCase` for components (and `UPPER_SNAKE_CASE` for true constants).
- formatting: rules like `indent` help keep code consistent.

> **Correction.** The original talk listed "`snake_case` for constants" as a convention. That is **not** a JavaScript/React convention, JS constants are conventionally `camelCase`, or `UPPER_SNAKE_CASE` for genuine fixed constants (like `const MAX_RETRIES = 3`). `snake_case` (lowercase with underscores) belongs to languages like Python, not JavaScript. Stick to `camelCase` / `UPPER_SNAKE_CASE`.

### Why bother? (React + TypeScript + ESLint together)

Putting all three together buys you: cleaner code, better editor/IDE support (autocomplete, inline errors), more predictable and refactor-friendly code, a consistent codebase, React-specific safety, accessibility checks, a smoother development workflow, automatic formatting, and, overall, more **developer confidence**. It is a bit more setup up front, but it pays off quickly on any project bigger than a toy.

## G. Advanced React

Once you are comfortable with components, props, state, and hooks, these patterns help you write faster, more reusable React.

### Optimization: lazy loading

**Lazy loading** improves performance by loading resources only when they are actually needed, rather than all at once up front. In React you do this with `lazy` and `Suspense`:

```jsx
import React, { lazy, Suspense } from "react";

// The component is only downloaded when it is about to render
const LazyComponent = lazy(() => import("./LazyComponent"));

function App() {
  return (
    <Suspense fallback={<p>Loading...</p>}>
      <LazyComponent />
    </Suspense>
  );
}
```

How it works:

1. The `lazy` function dynamically loads a component using **code splitting**. It takes a function that returns a dynamic `import()` statement.
2. The `Suspense` component handles the **loading state** while the component is being fetched. Its `fallback` prop specifies what to display in the meantime.
3. When `LazyComponent` is used inside `Suspense`, React automatically triggers the download when it is about to render.
4. Once loaded, it renders like any other component.

The payoff: your initial bundle is smaller, so the app starts faster, and rarely used screens are only downloaded if the user actually visits them.

### `forwardRef`

`forwardRef` lets a parent pass a **ref** down into a child so the parent can reach the child's underlying DOM element (for example, to focus an input). Historically this required wrapping the child in `forwardRef`:

```jsx
// forward-ref-example.jsx
import React, { forwardRef, useRef, useEffect } from "react";

// Child component that will receive the forwarded ref
const ChildComponent = forwardRef((props, ref) => {
  // Create a local ref for the input element
  const inputRef = useRef();

  // Attach the forwarded ref to the input element
  useEffect(() => {
    if (ref) {
      ref.current = inputRef.current;
    }
  }, [ref]);

  return <input ref={inputRef} />;
});

// Parent component that uses the ChildComponent
const ParentComponent = () => {
  // Create a ref to store the input element
  const childRef = useRef();

  // Focus the input element when the parent component mounts
  useEffect(() => {
    if (childRef.current) {
      childRef.current.focus();
    }
  }, []);

  return <ChildComponent ref={childRef} />;
};

export default ParentComponent;
```

> **Modern note: `forwardRef` is (mostly) no longer needed.** In **React 19**, `ref` can be passed as a **regular prop** to function components, so you rarely need `forwardRef` anymore. The child can simply accept `ref` in its props:
>
> ```jsx
> function ChildComponent({ ref }) {
>   return <input ref={ref} />;
> }
> ```
>
> `forwardRef` still works for now (so you'll see it in existing code), but it is on a deprecation path. For new code, prefer `ref`-as-a-prop.

### Custom hooks

React ships with built-in hooks like `useState`, `useContext`, and `useEffect`. Sometimes you'll wish there were a hook for a **more specific** purpose, to fetch data, to track whether the user is online, or to connect to a chat room. You won't find those in React, but you can **write your own** hooks for your application's needs. A custom hook is just a function whose name starts with `use` and that calls other hooks.

Here is a real one, `useKeyboardShow`, that tracks whether the on-screen keyboard is visible in a React Native app:

```tsx
import { useEffect, useState } from "react";
import { Keyboard } from "react-native";

export const useKeyboardShow = (): { hidden: boolean; visible: boolean } => {
  const [visible, setVisible] = useState(false);
  const [hidden, setHidden] = useState(true);

  const onKeyboardDidShow = (): void => {
    setVisible(true);
    setHidden(false);
  };

  const onKeyboardDidHide = (): void => {
    setVisible(false);
    setHidden(true);
  };

  useEffect(() => {
    const keyboardDidShowListener = Keyboard.addListener(
      "keyboardDidShow",
      onKeyboardDidShow,
    );
    const keyboardDidHideListener = Keyboard.addListener(
      "keyboardDidHide",
      onKeyboardDidHide,
    );

    return () => {
      keyboardDidHideListener.remove();
      keyboardDidShowListener.remove();
    };
  }, []);

  return { hidden, visible };
};
```

Notice the shape of it: it uses `useState` and `useEffect` inside, sets up listeners on mount, cleans them up on unmount (the `return () => { ... }` from the effect), and **returns a value** (`{ hidden, visible }`) that any component can consume. Now any component can simply write:

```tsx
const { visible: keyboardShowed, hidden: keyboardHid } = useKeyboardShow();
```

...and get keyboard visibility without repeating any of the listener logic. That is the real power of custom hooks: **you package up reusable stateful behavior once and reuse it everywhere**, exactly like the built-in hooks.

### Higher-Order Components (HOC)

A **Higher-Order Component (HOC)** is an advanced technique for **reusing component logic**. HOCs are not part of the React API as such, they are a pattern that emerges from React's compositional nature. Concretely, **a higher-order component is a function that takes a component and returns a new component**.

```jsx
// A functional component that receives the "isHovered" prop from the HOC.
function MyComponent({ isHovered }) {
  const text = isHovered ? "Hovered" : "Not Hovered";

  return <div>{text}</div>;
}

// Wrap MyComponent with the withHover HOC to add hover behavior.
const HoverableComponent = withHover(MyComponent);

// Now you can use HoverableComponent just like any other React component.
function App() {
  return (
    <div>
      <h1>Higher-Order Component Example</h1>
      <HoverableComponent />
    </div>
  );
}

export default App;
```

The `withHover(MyComponent)` call wraps your component and injects extra behavior (here, an `isHovered` prop) without `MyComponent` having to know how hover is tracked.

> **Modern note.** HOCs still work and you will meet them in existing code, but for most "share this logic" needs, **custom hooks** (above) are now the preferred, simpler tool. Reach for a HOC only when a hook genuinely can't express what you need.

## H. Frameworks & libraries

React is a library, so a rich ecosystem has grown *around* it. Here are the most important members of that ecosystem, the ones you are most likely to run into.

### React Native

**React Native** is an open-source **framework** for building **Android and iOS** applications (and more) using React and each platform's **native** capabilities. You write JavaScript (and React components) to access the platform's APIs and to describe the appearance and behavior of your UI. Its components are bundles of reusable, nestable code, just like React on the web.

The pitch is very similar to React on the web:

- **Declarative.** Declarative views make your code more predictable and easier to debug.
- **Component-based.** Build encapsulated components that manage their own state, then compose them into complex UIs.
- **Developer velocity.** See local changes in seconds; JavaScript changes can be live-reloaded without rebuilding the native app.
- **Portability.** Reuse code across iOS, Android, and other platforms.

The key difference from web React is that you don't use HTML tags, you use **native components** that map to each platform's real widgets. Here's the mapping:

| React Native | Android | iOS | Web analog | Description |
| --- | --- | --- | --- | --- |
| `<View>` | `ViewGroup` | `UIView` | non-scrolling `<div>` | A container supporting flexbox layout, style, touch handling, accessibility |
| `<Text>` | `TextView` | `UITextView` | `<p>` | Displays, styles, and nests strings of text; handles touch |
| `<Image>` | `ImageView` | `UIImageView` | `<img>` | Displays images |
| `<ScrollView>` | `ScrollView` | `UIScrollView` | `<div>` | A generic scrolling container for multiple components |
| `<TextInput>` | `EditText` | `UITextField` | `<input type="text">` | Lets the user enter text |

**Supported platforms** include Android, iOS, Windows, Web, and even TV. That reach, plus the shared React mental model, is why so many companies use it for their mobile apps. (The custom hook `useKeyboardShow` from area G is a real React Native hook, notice it imported `Keyboard` from `react-native`.)

### Next.js

**Next.js** is a **framework built on top of React**. Where React leaves choices to you, Next.js makes many of them for you and adds capabilities React doesn't have on its own:

- **Server-Side Rendering (SSR):** render pages on the server for better SEO and faster initial load.
- **Static Site Generation (SSG):** pre-render pages at build time for very fast loads and reduced server load.
- **Routing:** simplified routing with automatic code splitting, no extra configuration to create and manage routes.
- **API routes:** create serverless backend functionality inside your app.
- **File-system routing:** organize pages and routes by the file/folder structure.
- **Hybrid apps:** mix server-rendered and client-rendered parts in the same app.
- **Automatic code splitting:** ship smaller chunks that load only when needed.

> **Modern note: the App Router.** The original material describes data fetching with `getServerSideProps`, `getStaticProps`, and `getInitialProps`. Those belong to the older **Pages Router**. Modern Next.js (13+ and especially 14/15) defaults to the **App Router**, built on **React Server Components**, where you fetch data directly inside `async` server components using the standard `fetch` API, and files like `page.tsx`/`layout.tsx` in an `app/` directory define your routes. The Pages Router still exists and works, but new projects should learn the **App Router** first.

### Preact

**Preact** is a **fast, tiny (~3.5 kB) alternative** to React with a largely compatible API. Highlights:

- **Performance:** renders quickly and efficiently.
- **Size:** very small, which helps load time.
- **Efficiency:** careful memory usage (avoiding garbage-collection thrash).
- **Understandability:** the codebase is small enough to grasp in a few hours.
- **Compatibility:** `preact/compat` aims to be as compatible with the React API as possible, so many React apps can switch with little change.
- **Closer to the DOM:** Preact provides a thin Virtual DOM layer over the browser's real DOM, using stable platform features and real event handlers.
- **Portable & embeddable:** its small footprint makes it easy to drop into part of an existing app or even a widget.

If bundle size is critical (say, an embeddable widget or a very performance-sensitive site), Preact is worth a look.

### Million.js

**Million.js** was presented here as an **optimizing layer** for React that promised faster load and render times through an optimizing compiler, reactive data primitives, batching, keyed-rendering optimizations, a React compatibility layer, and a smaller bundle size.

> **Modern note.** Treat Million.js as **historical context** rather than something to adopt today. The project has largely **wound down**, and its author moved on to work on React's own tooling. The performance story it was chasing, automatic optimization so you don't hand-tune `useMemo`/`useCallback`, is now addressed directly by the **React Compiler** (mentioned in the Hooks section) that ships with modern React. If you were reaching for Million.js for speed, the modern answer is the **React Compiler** plus normal good practices.

## I. References

The material in this lesson draws on the following sources, all worth bookmarking:

- **Library vs framework** — [freeCodeCamp: the difference between a framework and a library](https://www.freecodecamp.org/news/the-difference-between-a-framework-and-a-library-bd133054023f/)
- **React** — [react.dev](https://react.dev/) (the official docs, and the best place to learn React today)
- **Virtual DOM** — [GeeksforGeeks: ReactJS Virtual DOM](https://www.geeksforgeeks.org/reactjs-virtual-dom/)
- **React lifecycle** — [React lifecycle methods diagram](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)
- **React hooks** — [W3Schools: React Hooks](https://www.w3schools.com/react/react_hooks.asp)
- **React forms** — [W3Schools: React Forms](https://www.w3schools.com/react/react_forms.asp)
- **React Native** — [reactnative.dev: intro to React Native components](https://reactnative.dev/docs/intro-react-native-components)
- **Next.js** — [nextjs.org](https://nextjs.org/)
- **Preact** — [preactjs.com](https://preactjs.com/)
- **Million.js** — [million.dev](https://million.dev/)

> **On staying current.** React moves fast (remember "constant changes" from the drawbacks). When in doubt, **[react.dev](https://react.dev/) is the source of truth**, it is kept up to date and its examples reflect the current recommended approach.
