# APIs

Up to now we have been building things that live entirely inside our own page: a calculator, some buttons, a few functions that add numbers together. But every *serious* application you use every day, Facebook, Instagram, Wikipedia, YouTube, is constantly talking to a computer somewhere else on the internet to fetch and store information. The tool that lets two programs talk to each other like that is called an **API**.

Do not worry if the word sounds intimidating. **API** stands for **Application Programming Interface**, and an *interface* is simply an agreed-upon way for two things to communicate. Think of a restaurant: you (the customer) do not walk into the kitchen and cook your own food. Instead, you talk to a **waiter**, who takes your order to the kitchen and brings back your plate. The waiter is the *interface* between you and the kitchen. An API is exactly that waiter: your program tells the API what it wants, and the API brings back the data (or confirms it saved something), without you ever needing to know *how* the kitchen works inside.

In this lesson we focus on the **concepts**: what an API is, the client/server relationship, REST, the HTTP verbs, endpoints, requests and responses, status codes, and the JSON format your data travels in. We will also introduce `fetch` at a conceptual level. The actual *asynchronous mechanics* (promises, `async`/`await`) are covered in the next lesson, so we will cross-link there rather than repeat them here.

> **Note:** This is an introductory, conceptual lesson. You do **not** need to become an expert. The goal is that you recognize these ideas when you meet them again in the React lessons, where you will actually write code that calls APIs.

## Module Content

- [**What Is an API and Why We Need One**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-6/README.md#what-is-an-api-and-why-we-need-one)
- [**Client and Server**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-6/README.md#client-and-server)
- [**REST**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-6/README.md#rest)
- [**Endpoints and URLs**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-6/README.md#endpoints-and-urls)
- [**The HTTP Verbs (GET, POST, PUT, PATCH, DELETE)**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-6/README.md#the-http-verbs)
- [**Requests and Responses**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-6/README.md#requests-and-responses)
- [**HTTP Status Codes**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-6/README.md#http-status-codes)
- [**JSON: The Language of APIs**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-6/README.md#json-the-language-of-apis)
- [**Fetching Data with `fetch`**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-6/README.md#fetching-data-with-fetch)
- [**Module Activity**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-6/README.md#module-activity)
- [**Sources**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-6/README.md#sources)

## What Is an API and Why We Need One

So far our programs have only used **static data**, information we typed directly into the code. But real applications almost never work that way. When you open Facebook, the app does not already *contain* your name, your friend count and your profile picture. That information lives on a computer somewhere else (a **server**), and your app has to go and **ask for it**.

An **API** is the doorway through which your program asks for that information. It is a well-defined set of requests you are allowed to make, and predictable answers you will get back. Because the doorway is agreed upon in advance, the person who wrote the server and the person who wrote your app do not have to be the same, they just both respect the same interface.

Here is the key mindset for a frontend developer: **you usually do not care what happens inside the server.** Whoever built the backend (your friendly backend engineer) simply hands you a **URL** and says *"call this address and you will get users back"*. From the frontend, all we care about is: *I make a call to this address, and I get data back.* That is it.

```
   YOUR APP (frontend)                    THE API                 THE SERVER (backend)
   ┌────────────────┐   "give me users"  ┌────────┐   query      ┌──────────────────┐
   │  browser code  │ ─────────────────► │ waiter │ ───────────► │  data / database │
   │                │ ◄───────────────── │        │ ◄─────────── │                  │
   └────────────────┘    users (JSON)    └────────┘   results    └──────────────────┘
```

## Client and Server

To understand APIs you need two words that we already met at the very start of the course:

- **Client** — the part the **user sees and interacts with**. In web development this is the **frontend**: the browser code, the buttons, the text, the colors. Our whole course is about the frontend, so *we* are the client.
- **Server** — the machine that **stores and manipulates data**, usually running somewhere in the cloud (the **backend**). It waits, listening, ready to answer calls.

The relationship is simple: the **client makes a request**, and the **server sends a response**. When you log into Facebook, your browser (client) asks a server for your profile data; the server looks it up and sends it back. When you post a photo, the client sends the photo to the server so it can store it.

```
   CLIENT (frontend)                         SERVER (backend)
   what the user sees   ── request ──►        stores & handles data
                        ◄── response ──
```

An important reason this split exists: it would be unsafe and impractical for your browser to reach directly into a company's database. The server sits in the middle, exposes a controlled set of operations through the API, and decides what the client is and is not allowed to do.

## REST

You will hear the word **REST** constantly. **REST** stands for **Representational State Transfer**, and it is a *style* (a set of conventions) for designing APIs that communicate over **HTTP**, the same protocol your browser already uses to load web pages.

You do not need the academic definition. What matters in practice is the core idea REST gives us:

1. Everything is treated as a **resource** (a user, a photo, a product), and each resource has its own **address** (a URL).
2. To act on a resource, you send an **HTTP request** to its address using a **verb** that describes *what you want to do* (read it, create it, update it, delete it).

That predictability is the whole point. Once you know an API is RESTful, you can guess how to use it: to read users you send a "read" request to the users address; to create a user you send a "create" request to the same kind of address. Let's unpack the pieces.

## Endpoints and URLs

An **endpoint** is a specific **URL** that the API exposes, one address that corresponds to one operation or one resource. When your client accesses that route, the server does something (reads data, saves data, etc.) and responds.

```
https://api.example.com/users        ◄─ endpoint for the "users" resource
https://api.example.com/users/123     ◄─ endpoint for the user whose id is 123
https://api.example.com/products      ◄─ endpoint for the "products" resource
```

A **URL** (Uniform Resource Locator) is just the web address. If you have ever mistyped a web address and gotten an error, you already know the practical lesson here: the URL must be **exactly** right. Writing `httttps://...` instead of `https://...` means the address is no longer valid, and the call will simply fail.

You can think of the backend engineer's job as *publishing* these endpoints, and your job (as the frontend) as *calling* them at the right address with the right verb.

## The HTTP Verbs

Every request carries an **HTTP verb** (also called an HTTP **method**) that tells the server *what kind of operation* you want. These verbs map neatly onto the four things we do with almost any data. This mapping is so common it has a nickname: **CRUD** (Create, Read, Update, Delete).

| Operation | HTTP verb | What it does | Facebook example |
|-----------|-----------|--------------|------------------|
| **Read** | `GET` | Fetch / read existing data | Loading your profile to see your name and friends |
| **Create** | `POST` | Store new data | Signing up, submitting a login form, posting a photo |
| **Update (full)** | `PUT` | Replace an **entire** record | Overwriting your whole profile with new data |
| **Update (partial)** | `PATCH` | Change **part** of a record | Editing just your username |
| **Delete** | `DELETE` | Remove data | Deleting your account |

Let's make each one concrete.

### GET — reading data

`GET` is by far the most common verb in the frontend. **Every time you open a web page, you are making `GET` requests.** When you open your Facebook profile, the client sends a `GET` to the server asking *"what is my name? how many friends do I have? what is my profile picture?"* and the server returns that information. When Wikipedia shows you an article, that is a `GET`. Even loading an image from a URL is a `GET`, the picture lives on a server and your app downloads it.

```
GET  https://api.example.com/users        // read the list of users
GET  https://api.example.com/users/123     // read one specific user
```

### POST — creating data

`POST` **stores** new information on the server. Think of the login form on Facebook. Before you type anything, the app has no idea who you are. As you type your email and password, you fill a JavaScript object with that information. The moment you press *"Log in"*, the client sends a `POST` request carrying that data so the server can store or process it.

```
POST https://api.example.com/users        // create a new user (data travels with the request)
```

### PUT and PATCH — updating data

Both change existing data, and the difference is a classic interview question:

- **`PUT`** replaces an **entire** record. You send the full object, and the server overwrites everything.
- **`PATCH`** changes **only part** of a record. You send just the field(s) you want to modify.

For example, imagine you saved a user by mistake with the name *"Panchito"*, when it should be *"Francisco"*. If you only want to fix that one field, that is a `PATCH` (a partial update). If you decide to overwrite the whole user record with a brand-new object, that is a `PUT` (a full update).

```
PUT   https://api.example.com/users/123    // replace the whole user 123
PATCH https://api.example.com/users/123    // change only some fields of user 123
```

> **Note:** People are often surprised to learn that "update" is not a single HTTP verb, it is split between `PUT` (replace the whole thing) and `PATCH` (change a part). Keep that distinction handy.

### DELETE — removing data

`DELETE` is the simplest: it removes a record. If a user says *"I want to delete my account"*, the client sends a `DELETE` request for that user, and the server removes the entry.

```
DELETE https://api.example.com/users/123   // delete user 123
```

## Requests and Responses

Every interaction with an API is a pair: a **request** you send, and a **response** you get back.

A **request** is made of a few parts:

- The **URL / endpoint** you are calling.
- The **HTTP verb** (`GET`, `POST`, …) describing the operation.
- Optionally, a **body**, the data you are sending along (needed for `POST`, `PUT`, `PATCH`; not for a plain `GET`).
- Optionally, **headers**, extra metadata about the request (for example, telling the server what format you are sending).

A **response** is what the server sends back:

- A **status code** telling you whether it worked (see the next section).
- Usually a **body**, the data you asked for, almost always in **JSON** format.

```
   REQUEST                                RESPONSE
   ┌─────────────────────────┐            ┌──────────────────────────┐
   │ verb:  GET              │            │ status: 200 OK           │
   │ url:   /users/123       │  ───────►  │ body:   { "id": 123,     │
   │ body:  (none for GET)   │            │           "name": "..." }│
   └─────────────────────────┘  ◄───────  └──────────────────────────┘
```

Notice that a `GET` request typically has no body (you are only *asking*), while a `POST` request carries a body (you are *sending* something to store).

## HTTP Status Codes

Along with its answer, the server always sends back a **status code**: a three-digit number that tells your program, at a glance, *how the request went*. You do not need to memorize all of them, but you should recognize the families:

- **2xx — Success.** The request worked. The most common is **`200 OK`** (general success) and **`201 Created`** (something new was successfully created after a `POST`).
- **3xx — Redirection.** The resource lives somewhere else now; the browser is being sent to another address.
- **4xx — Client error.** *You* did something wrong. The famous **`404 Not Found`** means the endpoint or resource does not exist. **`401 Unauthorized`** and **`403 Forbidden`** mean you are not allowed. **`400 Bad Request`** means your request was malformed.
- **5xx — Server error.** *The server* broke while trying to handle your (perfectly valid) request. **`500 Internal Server Error`** is the classic one.

A simple mental shortcut: **4xx is your fault, 5xx is their fault, 2xx means everyone is happy.**

```
   2xx  ✅  it worked            (200 OK, 201 Created)
   3xx  ↪️  look somewhere else  (301, 302)
   4xx  🙈  the client messed up (400, 401, 403, 404)
   5xx  💥  the server messed up (500, 503)
```

## JSON: The Language of APIs

When the server sends data back, it needs a format both sides understand. That format is almost always **JSON**, which stands for **JavaScript Object Notation**.

If that name feels familiar, it should: JSON looks almost exactly like the **JavaScript objects** you learned about (curly braces, properties, values). It is the natural, readable way to represent structured data as text so it can travel across the internet.

A single user might arrive as JSON like this:

```json
{
  "id": 1,
  "firstName": "Josue",
  "email": "josue@mail.com",
  "friendCount": 145,
  "address": {
    "street": "Evergreen",
    "city": "Springfield",
    "country": "USA",
    "coordinates": {
      "latitude": "40.7128",
      "longitude": "-74.0060"
    }
  },
  "interests": ["videogames", "music", "technology"]
}
```

Notice how rich this is: a JSON value can contain **nested objects** (`address` has its own `coordinates` object) and **arrays** (`interests` is a list). APIs frequently return an **array of objects**, for example, a list of ten users, where each element of the array is itself an object:

```json
[
  { "id": 1, "firstName": "Josue",  "email": "josue@mail.com" },
  { "id": 2, "firstName": "Anakin", "email": "anakin@jedi.com" }
]
```

Because this maps so cleanly onto JavaScript objects and arrays, once the data is in your program you access it exactly the way you already know, with dot notation and indexes:

```js
// Given a `users` array parsed from the JSON above:
console.log(users[0].firstName);                 // "Josue"
console.log(users[0].address.coordinates.latitude); // "40.7128"
```

> **Note:** If you need a refresher on objects, dot notation, and nested/complex structures, revisit the JavaScript lessons. APIs are one of the biggest reasons objects matter so much.

## Fetching Data with `fetch`

JavaScript ships with a built-in function called **`fetch`** whose entire job is to **connect to a URL and bring back data over HTTP**. It is the tool the client uses to reach out to a server.

At its simplest, you give `fetch` a URL, and it performs a **`GET`** request by default (remember: `GET` means "read"):

```js
// Conceptually: "go to this address and read whatever is there"
fetch("https://api.example.com/users");
```

If you wanted a different operation, say a `POST` to *store* data instead of read it, you would tell `fetch` which method to use and hand it a body. But for reading, a plain `fetch(url)` is a `GET`, and that is what we care about here.

Once the server responds, the raw response is not yet plain data you can use directly, you convert it into a usable JavaScript value with the response's **`.json()`** method. Conceptually the flow is:

```js
// 1. Call the server (a GET request to the URL)
// 2. Convert the response body from JSON text into JavaScript objects/arrays
// 3. Now you can use the data (loop over it, read properties, show it on screen)
```

Here is the important catch, and the reason this connects to the next lesson: **`fetch` does not give you the data instantly.** When you call it, your program does not yet know *when* the answer will arrive. Maybe your internet is slow, maybe the server is busy, maybe it is raining and your connection dropped. Anything that depends on the network takes an **unknown amount of time**.

Because of that, `fetch` does not hand you the users right away, it hands you a **promise**: a placeholder that means *"I have started asking the internet; I will give you the real answer once it resolves."* Trying to read the data before that promise resolves gives you nothing useful.

Managing that "wait until it is ready" behavior, promises, the `async` keyword, and `await`, is exactly the topic of the **next lesson**. There we cover the asynchronous mechanics in full, including how `await` forces an asynchronous call to behave synchronously and how `try/catch` lets us handle a failed request gracefully.

> ➡️ **Continue to [Lesson 7 — Asynchronous Functions](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-7/README.md)** to learn *how* to actually wait for and handle the data that `fetch` returns (promises, `async`/`await`, and error handling). This current lesson gives you the **what and why** of APIs; lesson 7 gives you the **how** of consuming them.

For this lesson, the takeaway is conceptual and short:

- `fetch` **reads data from a server** given a **URL**.
- A plain `fetch(url)` is a **`GET`** request.
- The response comes back as **JSON**, which you convert into JavaScript objects/arrays.
- The result does not arrive instantly; it arrives as a **promise**, handled with the async tools from lesson 7.

## Module Activity

<!--
  The instructor did not have students write a full fetch program in this session
  (the async mechanics are deliberately deferred to lesson 7, and the live demo
  was introductory only). This activity is therefore a clean, concept-focused
  exercise in the same spirit as the recorded lesson, exploring a real public
  API and reasoning about verbs, endpoints, status codes and JSON, without yet
  requiring promises/await.
-->

You will explore a **real, free, public API** and reason about it using everything from this lesson. No async code is required yet, that comes in lesson 7.

We will use the **JSONPlaceholder** fake API, which is made for practice: <https://jsonplaceholder.typicode.com>.

**Part 1 — Read data with a GET (in your browser).**

A `GET` request is just a URL, so you can perform one by simply *pasting an endpoint into your browser's address bar*. Try each of these and observe the JSON that comes back:

```
https://jsonplaceholder.typicode.com/users
https://jsonplaceholder.typicode.com/users/1
https://jsonplaceholder.typicode.com/posts/1
```

For each one, write down (in a comment or a note):

1. Is the response a **single object** or an **array of objects**?
2. Pick one property that is itself a **nested object** or an **array**, and write the dot/index path you would use to reach a value inside it (for example, `users[0].address.city`).

**Part 2 — Match operations to verbs.**

For each real-world action below, write which **HTTP verb** you would use and to which kind of **endpoint**:

1. Show the profile of the user whose id is `1`.
2. Register a brand-new user from a sign-up form.
3. Change *only* the email of user `1`.
4. Replace the entire record of user `1` with new data.
5. Remove user `1` permanently.

**Part 3 — Read the status code.**

Open your browser's developer tools (`F12`), go to the **Network** tab, and reload one of the endpoints above. Find the request in the list and note its **status code**. Then intentionally request an endpoint that does not exist, for example:

```
https://jsonplaceholder.typicode.com/users/99999
```

Write down the status code you get back and explain, in one sentence, which *family* (2xx / 4xx / 5xx) it belongs to and why.

> **Optional stretch (only if you have peeked ahead):** In lesson 7 you will learn `async`/`await`. Once you have, come back and write a small `fetch` call that reads `/users`, converts the response with `.json()`, and logs the first user's name to the console.

## Sources

- [**MDN — HTTP overview**](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
- [**MDN — HTTP request methods (verbs)**](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
- [**MDN — HTTP response status codes**](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- [**MDN — Using the Fetch API**](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
- [**MDN — JSON**](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON)
- [**JSONPlaceholder — free fake REST API for practice**](https://jsonplaceholder.typicode.com)
