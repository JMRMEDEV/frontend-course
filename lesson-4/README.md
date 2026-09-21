# TypeScript

TypeScript (TS) is a **superset of JavaScript**. That word "superset" sounds fancier than it is: it just means TypeScript is *JavaScript, plus some extra features on top*. Every valid JavaScript program is already valid TypeScript, but TypeScript adds one big thing that plain JavaScript does not have, **static types**.

Do not worry if the phrase "static types" feels intimidating. In the previous lesson we learned that JavaScript *has* types (string, number, boolean, and so on) but never forces us to write them down, it figures them out for us at the moment the code runs. We even warned that this freedom can lead to "total chaos". TypeScript is the answer to that chaos: it lets us **write the types down on purpose** and then checks, *before the program ever runs*, that we are respecting our own rules.

The simplest way to think about it: **TypeScript is JavaScript with types**. If you understood the JavaScript lesson, you already understand most of what is happening here, we are just adding labels that describe what kind of value each thing is allowed to be.

## Module Content

- [**What TypeScript Is (and Why)**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-4/README.md#what-typescript-is-and-why)
- [**TypeScript Compiles to JavaScript**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-4/README.md#typescript-compiles-to-javascript)
- [**Typing Variables, Parameters and Return Values**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-4/README.md#typing-variables-parameters-and-return-values)
- [**void, any and undefined**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-4/README.md#void-any-and-undefined)
- [**More Data Types: arrays, objects and functions**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-4/README.md#more-data-types-arrays-objects-and-functions)
- [**Interfaces**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-4/README.md#interfaces)
- [**Optional Properties**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-4/README.md#optional-properties)
- [**Type Aliases**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-4/README.md#type-aliases)
- [**Extending Interfaces**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-4/README.md#extending-interfaces)
- [**Union and Intersection Types**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-4/README.md#union-and-intersection-types)
- [**Generics**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-4/README.md#generics)
- [**Utility Types: Omit and Pick**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-4/README.md#utility-types-omit-and-pick)
- [**Sources**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-4/README.md#sources)

## What TypeScript Is (and Why)

The default behavior of TypeScript is to be **strict about data types**. Remember the "worst feature" of JavaScript we mentioned last lesson, that not knowing the type can turn an app into chaos? Here is a concrete example of that chaos.

In **JavaScript**, we can write a function meant to add two numbers and then, by accident, call it with text:

```js
const usernameGenerator = (firstName, lastName) => {
  return firstName.slice(0, 3) + lastName.slice(0, 3);
};

// Someone calls it with numbers instead of strings...
console.log(usernameGenerator(123, [1, 2, 3]));
// 💥 Runtime error: firstName.slice is not a function
```

JavaScript happily *accepts* this bad call. The program only breaks **later**, at runtime, and then you have to go debugging to discover that someone passed numbers where strings were expected.

TypeScript catches this **before the program even runs**. If you tell TypeScript that `firstName` must be a `string`, it will refuse to let you pass a number, and it will underline the mistake in your editor immediately. That is the whole point of TypeScript: is it much easier to debug than JavaScript? **A thousand percent yes**, because a huge class of bugs simply cannot exist anymore.

## TypeScript Compiles to JavaScript

Here is a key idea: **browsers and Node do not run TypeScript directly, they run JavaScript.** So before your TypeScript code can execute anywhere, it is **compiled** (translated) into plain JavaScript. During that compilation step, all the type annotations are simply *erased*, because JavaScript has no concept of them.

You can see this side by side in the [**TypeScript Playground**](https://www.typescriptlang.org/play). On the left you write TypeScript; on the right you see the generated JavaScript. For example, this TypeScript:

```ts
const performAddition = (first: number, second: number): number => {
  const result = first + second;
  return result;
};
```

compiles down to this JavaScript:

```js
const performAddition = (first, second) => {
  const result = first + second;
  return result;
};
```

Notice the difference: the JavaScript on the right has **no type annotations** (`: number` is gone) because those types do not exist in JavaScript. They existed only to let TypeScript check our work. And here is the important part, **if we break our own type rules, TypeScript will not even compile.** The types are a safety net that lives at authoring/compile time, then disappears in the final JavaScript that actually runs.

## Typing Variables, Parameters and Return Values

The core new syntax in TypeScript is the **colon** (`:`). After a name, a colon lets us declare *what type that thing is allowed to be*.

Let's revisit the addition function. We want the first parameter to be a `number`, the second to be a `number`, and we also want to promise that the whole function **returns** a `number`:

```ts
const performAddition = (first: number, second: number): number => {
  const result = first + second;
  return result;
};
```

Read it piece by piece:

- `first: number` → the first **parameter** must be a number.
- `second: number` → the second parameter must be a number.
- `): number =>` → the part after the parentheses is the **return type**: this function promises to give back a number.

Because we promised to return a number, TypeScript will complain if we return nothing (that would be `void`), or if we return the wrong type. Once we actually `return result` (a number), the compilation errors disappear.

Now watch what happens if we call it incorrectly:

```ts
const myVariable1 = "abc"; // this is a string
const myVariable2 = 456;

console.log(performAddition(myVariable1, myVariable2));
// ❌ Argument of type 'string' is not assignable to parameter of type 'number'.
```

TypeScript immediately underlines `myVariable1` in red: we said the first parameter had to be a `number`, but we handed it a `string`. In JavaScript this call would be perfectly "valid" (it would quietly glue `"abc"` onto a number and produce a nonsense string). In TypeScript it **simply is not allowed**. To fix it, we pass a number and the error is gone:

```ts
console.log(performAddition(12, 123)); // 135 ✅
```

We were **consistent with our data types**, so there was no problem.

## void, any and undefined

When you declare a return type, TypeScript enforces it strictly. In particular, once you say a function returns a specific type, you are **not allowed** to return `undefined`, `void`, or `any` in its place. It is worth knowing what these three words mean:

- **`void`** → "this function returns **nothing**". It is the return type of a function whose only job is a side effect, like printing to the console.
- **`undefined`** → the value a variable has when it exists but was never given a value (we met this in the JavaScript lesson).
- **`any`** → a special escape hatch that means "this could be **any** type, stop checking it". It effectively turns TypeScript's protection *off* for that value. It exists, but using it defeats the purpose of TypeScript, so prefer to avoid it.

Here is a function that returns nothing, so its return type is `void`:

```ts
const myFunctionA = (first: string): void => {
  console.log(`Receive string is: ${first}`);
};

myFunctionA("Luke"); // Receive string is: Luke
```

How do we know it returns nothing? Because it only *prints* to the console, it never gives a value back. That is exactly what `void` describes.

## More Data Types: arrays, objects and functions

Beyond `number` and `string`, TypeScript lets us describe more elaborate shapes.

An **array of numbers** is written as `number[]`. Here is a function that takes a `number[]` and returns a `string[]`:

```ts
const myFunctionB = (array: number[]): string[] => {
  return array.map((item, index) => {
    return `The index for item ${item} is ${index}`;
  });
};

console.log(myFunctionB([0, 117, 56]));
// ["The index for item 0 is 0", "The index for item 117 is 1", "The index for item 56 is 2"]
```

A nice detail: inside `.map`, if you hover over `item`, TypeScript already knows it is a `number`, thanks to the type we declared. This is TypeScript helping you understand your own code as you write it.

We can also declare a parameter as a generic **object**:

```ts
const myFunctionC = (first: object): void => {
  console.log(`Received object is: ${JSON.stringify(first)}`);
};

myFunctionC({ property: "value" }); // Received object is: {"property":"value"}
```

> **Note:** We used `JSON.stringify()` here because printing an object directly in the Playground console shows something unhelpful like `[object Object]`. `JSON.stringify()` converts the object into readable text so we can actually see its contents.

Even a **function** can be a type. That is, a parameter can be described as "a function that receives these arguments and returns this type":

```ts
const myFunctionD = (func: (a: number, b: string) => string): void => {
  console.log(`Receive function is: ${func(3, "abc")}`);
};

const myAuxFunc = (a: number, b: string): string => {
  return `${a} and ${b}`;
};

myFunctionD(myAuxFunc); // pass the reference, not myAuxFunc()
```

Do not get stuck on *why* we would do this. The takeaway is simply that **a type can even be the shape of a function**. Notice we pass `myAuxFunc` (the function *reference*), not `myAuxFunc()` (which would *call* it).

## Interfaces

Interfaces are one of the most useful features of TypeScript. The official name is **interface**, but what it really represents is a **contract**, a contract about *types*.

Here is the problem interfaces solve. Imagine a function that needs many parameters:

```ts
const myFunctionZ = (
  paramsA: number,
  paramsB: string,
  paramsC: object,
  paramsD: object[]
): void => {
  console.log("params are:", paramsA, paramsB, paramsC, paramsD);
};
```

Four parameters is already a bit much. Now imagine **thirty** of them. Writing them all inline would be neither readable nor practical. Instead, we define an **interface** that groups them together. By convention, interface names start with a capital **`I`** (this is a convention and a good practice, not a requirement):

```ts
interface IMyFunctionZParams {
  paramsA: number;
  paramsB: string;
  paramsC: object;
  paramsD: object[];
}

const myFunctionZ = (params: IMyFunctionZParams): void => {
  console.log("params are:", params.paramsA, params.paramsB, params.paramsC, params.paramsD);
};
```

Notice that inside an interface each property ends with a **semicolon** (or a line break), and the interface itself looks like the *shape of an object*. So when we call the function, we pass an object that satisfies the contract:

```ts
myFunctionZ({
  paramsA: 123,
  paramsB: "hello",
  paramsC: { propA: "test" },
  paramsD: [{ propB: "value" }],
});
```

If you forget a property, or give one the wrong type, TypeScript complains immediately: *"your object is missing `paramsD`"*, or *"string is not assignable to number"*. This is why TypeScript is so useful: it tells you **exactly** which properties a function expects and forces you to provide them. If you do not, your program will not even compile.

A common professional practice is to place interface definitions in their **own separate files**. That way your functions stay perfectly readable (just clean function calls), while the type definitions live elsewhere.

Interfaces also support **docstrings**, comments that show up when you hover over a property in your editor:

```ts
interface IMyFunctionZParams {
  /** The number of friends you have */
  paramsA: number;
  /** The full message you want to show */
  paramsB: string;
  paramsC: object;
  paramsD: object[];
}
```

Now, hovering over `paramsA` anywhere in your code shows *"The number of friends you have"*. Your code stays clean, but the documentation is one hover away.

Finally, interfaces are not only for function parameters, they describe **the shape any object must have**. We can annotate a variable with an interface:

```ts
const myObject: IMyFunctionZParams = {
  paramsA: 23,
  paramsB: "hello",
  paramsC: { propA: 123 },
  paramsD: [{ propB: "value" }],
};

myFunctionZ(myObject); // TypeScript knows myObject satisfies the contract
```

## Optional Properties

By default, every property in an interface is **mandatory**, you must always provide it. To make a property **optional**, add a question mark (`?`) after its name:

```ts
interface IMyFunctionZParams {
  paramsA: number;
  paramsB: string;
  paramsC: object;
  paramsD?: object[]; // optional: may be provided, or may be undefined
}
```

Now `paramsD` can be an array of objects **or** simply be left out (in which case its value is `undefined`). If you read it without setting it, you will get `undefined`; if you set it, you get whatever you assigned.

## Type Aliases

Alongside `interface`, TypeScript has another keyword: **`type`**. A `type` lets us create an **alias**, a named shortcut for a type, and it can do a few things interfaces cannot.

One of the most useful is defining a set of **specific allowed values** (a union of literals). Let's move to game examples. Suppose a character's class can only be one of three options:

```ts
type CharacterClassType = "wizard" | "warrior" | "assassin";
```

Now anything typed as `CharacterClassType` can *only* be one of those three strings. If you try to assign `"mage"`, TypeScript rejects it:

```ts
let myClass: CharacterClassType = "warrior"; // ✅ allowed
// let myClass: CharacterClassType = "mage"; // ❌ "mage" is not a valid CharacterClassType
```

Let's put this to work in an MMORPG character interface:

```ts
type CharacterClassType = "wizard" | "warrior" | "assassin";

interface IMMORPGCharacter {
  /** The name the rest of the users will see while you play */
  name: string;
  /** Amount, in units, of how much health you have remaining */
  health: number;
  /** The class of your character; it defines your strengths and weaknesses */
  characterClass: CharacterClassType;
  /** Objects that can improve your character's stats */
  magicObjects?: string[];
}

const kingslayer: IMMORPGCharacter = {
  name: "Arthas",
  health: 100,
  characterClass: "warrior",
  // magicObjects is optional, so we can leave it out
};
```

> **Note:** we could not name the property `class`, because `class` is a reserved word in TypeScript. That is why we used `characterClass`.

Interfaces can even be **nested**: a property of one interface can be typed with another interface. For example, a city that contains a list of non-playable characters (NPCs), where each NPC is itself an `IMMORPGCharacter`:

```ts
type FactionType = "alliance" | "horde";

interface IMMORPGCity {
  /** Name of the city */
  name: string;
  /** Identifier used for the database */
  id: string;
  /** Who is controlling the city right now */
  faction: FactionType;
  /** All the non-playable characters wandering the city */
  npcs: IMMORPGCharacter[];
}

const stratholme: IMMORPGCity = {
  name: "Stratholme",
  id: "123",
  faction: "alliance",
  npcs: [{ name: "Panchito", health: 100, characterClass: "wizard" }],
};

console.log(stratholme.npcs[0].name); // "Panchito"
```

This way our game is perfectly under control at all times: we always know exactly what type of data every piece needs.

## Extending Interfaces

Think about a game: almost every object (a city, a character, a sword, a terrain tile) has a **name** and an **id**. Repeating those two properties in every interface is wasteful. Instead, we can define them once and have other interfaces **extend** that base interface:

```ts
interface IGameObjectCommonProperties {
  /** Name that can be publicly seen */
  name: string;
  /** Identifier used for the database */
  id: string;
}

interface IMMORPGCharacter extends IGameObjectCommonProperties {
  health: number;
  characterClass: CharacterClassType;
  magicObjects?: string[];
}
```

The `extends` keyword makes the new interface **inherit** all the properties of the interface it extends. So now every `IMMORPGCharacter` automatically requires `name` and `id` too.

You can even extend **multiple** interfaces at once. Suppose everything stored in a database also needs to track when it was created and last updated:

```ts
interface IDatabaseObject {
  /** When the object was created in the DB */
  created: number;
  /** When the object was last updated in the DB */
  updated: number;
}

interface IMMORPGCharacter extends IGameObjectCommonProperties, IDatabaseObject {
  health: number;
  characterClass: CharacterClassType;
  magicObjects?: string[];
}
```

Now every character must define `name`, `id`, `created`, `updated`, plus its own specific properties. Separate the interfaces you want to extend with a **comma**.

## Union and Intersection Types

We already used the `|` (**pipe**) operator above to say "one of these string values". The pipe is called the **union** operator, and it works with whole types too, it means *"this value can be one type **or** another type, but you pick one"*.

The opposite is the `&` (**ampersand**) **intersection** operator, which **combines** types: *"this value must satisfy **both** types at once"*.

Let's see both with two small interfaces:

```ts
interface ISimpleCharacter {
  name: string;
  id: string;
}

interface IWarrior {
  attack: number;
}
```

**Union (`|`)** — either one type or the other:

```ts
type EitherCharacter = ISimpleCharacter | IWarrior;

const simpleCharacter: ISimpleCharacter = { name: "James", id: "3" };
const warrior: IWarrior = { attack: 22 };

// Both of these are allowed, because it can be one OR the other:
const a: EitherCharacter = simpleCharacter; // ✅
const b: EitherCharacter = warrior;         // ✅
```

**Intersection (`&`)** — both types combined:

```ts
type AttackingNpc = ISimpleCharacter & IWarrior;

// Must satisfy BOTH interfaces, so it needs name, id AND attack:
const myCharacter: AttackingNpc = {
  ...warrior,          // brings attack
  ...simpleCharacter,  // brings name and id
};
```

If we left out either half, TypeScript would complain that properties are missing, because the intersection demands **all** properties of **both** types.

So, to summarize the difference:

- **`|` (pipe / union)** → this value is **one type OR the other**.
- **`&` (ampersand / intersection)** → this value **combines both types** and must satisfy all of them.

> **`extends` vs intersection:** you may wonder how `A & B` differs from `interface C extends A, B`. In practice they achieve very similar results; the difference is mostly about readability and intent. `extends` reads as *"I am defining a new interface and adding my own new properties on top of the ones I inherit"*, while `&` reads as *"I am simply merging existing types together"* without adding anything new.

We can build a type from the combination and reuse it to avoid repetition (following the *don't repeat yourself* principle):

```ts
type CommonEntityPropertiesType = IDatabaseObject & IGameObjectCommonProperties;

interface IMMORPGWeapon extends CommonEntityPropertiesType {
  /** How much damage will be inflicted on the attacked entity */
  damage: number;
  /** How long the weapon is going to last */
  durability: number;
  /** Whether the weapon has magic or not */
  isMagic: boolean;
}
```

## Generics

Sometimes we do not know, *at definition time*, what type a property will hold, we want to decide that **later**, at the moment we create a specific object. For that, TypeScript has **generics**.

Imagine a collectible that a player can drop in a city. It might be a **number** (how much health it restores) or a **string** (a message another player will read), or many other things. Instead of writing a huge `number | string | object | ...` union, we use a generic type parameter, written between angle brackets `<>` right after the interface name:

```ts
interface IMMORPGCity<CollectibleType> {
  name: string;
  id: string;
  /** Item that a player drops or that is randomly found */
  collectible?: CollectibleType;
}
```

`CollectibleType` is a placeholder for a type we will **fill in dynamically** when we create an object. The name is arbitrary, we could call it `PanchitoType` and it would still work, but always give it a meaningful name.

Now, when we create a city, we specify the concrete type:

```ts
// A city whose collectible is a message (string):
const stratholme: IMMORPGCity<string> = {
  name: "Stratholme",
  id: "123",
  collectible: "hello there",
};

// A city whose collectible is a health boost (number):
const cholula: IMMORPGCity<number> = {
  name: "Cholula",
  id: "456",
  collectible: 20,
};
```

In the first city, `collectible` must be a `string`; in the second, it must be a `number`, TypeScript enforces whatever we plugged into the generic. That is the power of generics: **dynamic type assignment at the moment you create the value.**

## Utility Types: Omit and Pick

TypeScript ships with built-in helpers called **utility types**. Two very common ones are **`Omit`** and **`Pick`**, and they are opposites of each other.

**`Omit`** takes an existing type and produces a new one **without** the properties you list. Suppose a legendary weapon is just like a regular weapon, but it has no `durability` (it is practically infinite) and cannot be `isMagic`, plus it gains a `bonus`:

```ts
interface IMMORPGLegendaryWeapon extends Omit<IMMORPGWeapon, "durability" | "isMagic"> {
  /** How much extra damage the legendary weapon causes compared to a regular one */
  bonus: number;
}

const morningstar: IMMORPGLegendaryWeapon = {
  name: "Morningstar",
  id: "ABCD",
  created: 0,
  updated: 0,
  damage: 40,
  bonus: 20,
  // durability and isMagic are NOT allowed here, we omitted them
};
```

`Omit` takes two arguments: the type to remove properties **from**, and the properties to remove (joined with `|` when there is more than one).

**`Pick`** is the opposite: it keeps **only** the properties you list. Suppose an NPC's chore object only needs a weapon's `name` and `id`:

```ts
interface INpcChoreObject extends Pick<IMMORPGWeapon, "name" | "id"> {
  /** What this object is going to be used for */
  forToBePerformed: string;
}

const broom: INpcChoreObject = {
  name: "Simple broom",
  id: "789",
  forToBePerformed: "sweeping",
  // no damage, durability, created, updated... we only picked name and id
};
```

So, in one sentence each:

- **`Omit<Type, Keys>`** → everything from `Type` **except** the listed keys.
- **`Pick<Type, Keys>`** → **only** the listed keys from `Type`.

TypeScript is genuinely deep, but for our purposes the key mindset is simple: **think of it as JavaScript with types.** With that, you already understand enough to be productive.

## Module Activity

Model a small MMORPG's type system using everything from this lesson. Do it in the [**TypeScript Playground**](https://www.typescriptlang.org/play) so you can watch the generated JavaScript on the right and confirm your code compiles with no red underlines.

1. Create a base interface `IGameObjectCommonProperties` with `name: string` and `id: string`, and a `type CharacterClassType = "wizard" | "warrior" | "assassin"`.
2. Create an `IMMORPGCharacter` interface that **extends** `IGameObjectCommonProperties` and adds `health: number`, `characterClass: CharacterClassType`, and an **optional** `magicObjects?: string[]`. Add a docstring to at least one property and confirm it shows on hover.
3. Create an `IMMORPGCity` interface (also extending the base) whose `npcs` property is an **array of `IMMORPGCharacter`** (a nested interface).
4. Create one character (`kingslayer`) and one city (`stratholme`) that satisfy their contracts. Then `console.log` the name of the city's first NPC.
5. Add an `IMMORPGWeapon` interface, then use **`Omit`** to build an `IMMORPGLegendaryWeapon` (drop `durability`) and **`Pick`** to build an `INpcChoreObject` (keep only `name` and `id`). Create one instance of each.

Bonus: turn `IMMORPGCity` into a **generic** `IMMORPGCity<CollectibleType>` with an optional `collectible?: CollectibleType`, then create one city with a `string` collectible and another with a `number` collectible.

<!--
Repaired/adjusted from the recording:
- In the recording the instructor's live union/intersection demo momentarily mislabeled which
  operator (| vs &) does what, then self-corrected on camera. The written lesson presents only
  the corrected, accurate version (| = union / "one or the other", & = intersection / "both").
- Node.js, HTTP verbs (GET/POST/PUT/PATCH/DELETE), the mock "database" array demo, and all
  async/Promise/await/fetch material shown at the end of the recording are intentionally left
  out here to respect lesson scope; Node.js belongs to a later lesson and asynchronous
  functions are covered in lesson 7.
-->

## Sources

- [**TypeScript Official Documentation**](https://www.typescriptlang.org/docs/)
- [**TypeScript Handbook — Everyday Types**](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)
- [**TypeScript Utility Types (Omit, Pick, ...)**](https://www.typescriptlang.org/docs/handbook/utility-types.html)
- [**TypeScript Playground**](https://www.typescriptlang.org/play)
- [**Mozilla — JavaScript**](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
