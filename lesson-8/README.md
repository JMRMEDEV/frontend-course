# React Library

[**React**](https://react.dev/) is a **library** for building user interfaces out of small, reusable pieces called **components**. It was created by **Facebook (Meta)** and it powers a huge part of the modern web and, through **React Native**, a huge part of mobile apps too.

In the previous lessons we learned **HTML** (structure), **CSS** (styling) and **JavaScript** (behavior). React sits on top of all three: you keep using your HTML and CSS knowledge, but instead of manually reaching into the page with `document.getElementById` (like we did in the JavaScript lesson), React lets you **describe** what the UI should look like for a given set of data, and it takes care of updating the real page for you.

> **About this lesson and the next one.** React is a big topic, so it is split across two lessons. **This lesson (React Library)** covers the *what* and *why*: what React is, how it compares to other tools, and where it is used. The next lesson, [**React Key Concepts**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-9/README.md), covers the *how*: the actual features you write every day (JSX, components, props, state, hooks, forms, and more). Both target **React 19**, and where the ecosystem has moved on you will find **Modern note** callouts.

## Module Content

- [A. React: library or framework?](#a-react-library-or-framework)
- [B. React benefits & drawbacks](#b-react-benefits--drawbacks)
- [C. React vs Angular vs Vue](#c-react-vs-angular-vs-vue)
- [D. Where is React used?](#d-where-is-react-used)
- [Next lesson: React Key Concepts](#next-lesson-react-key-concepts)

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


## Next lesson: React Key Concepts

Now that you know *what* React is and *why* it exists, the next lesson gets hands-on with the features you will actually write: JSX, components, props, state, hooks, forms, TypeScript + ESLint, advanced patterns, and the wider ecosystem (React Native, Next.js, and more).

Continue with [**Lesson 9 — React Key Concepts**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-9/README.md).
