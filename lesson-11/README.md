# Postman

In [lesson 6](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-6/README.md) we learned what an **API** is: a doorway that lets your program ask another computer for data. We talked about **endpoints**, the **HTTP verbs** (`GET`, `POST`, `PUT`, `PATCH`, `DELETE`), **requests and responses**, **status codes**, and the **JSON** format your data travels in. But there was a catch: to actually *call* an API back then, you needed to write code (`fetch`) and wait until the asynchronous lessons to make it work.

[**Postman**](https://www.postman.com/) removes that catch. It is a friendly app that lets you send requests to any API and read the responses **without writing a single line of code**. You type an address, pick a verb, press **Send**, and Postman shows you exactly what the server sent back. It is the fastest way to *explore* an API, confirm an endpoint works, and understand its shape before you wire it into your app.

Do not worry if you have never used a tool like this. If you can fill in a form and click a button, you can use Postman. Think of it as a "browser for APIs": a browser is great at loading web pages (`GET` requests), but it cannot easily send a `POST` with a JSON body or set custom headers. Postman can do all of that, and it keeps your requests organized so you can run them again tomorrow.

> **Note:** Postman is updated frequently, so a menu label or button might sit in a slightly different place than described here. The *concepts* (send a request, read the response, save it into a collection) do not change. When in doubt, check the official docs at [learning.postman.com](https://learning.postman.com/).

## Module Content

- [**What Postman Is and Why Use It**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-11/README.md#what-postman-is-and-why-use-it)
- [**Installing Postman**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-11/README.md#installing-postman)
- [**The Practice API: JSONPlaceholder**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-11/README.md#the-practice-api-jsonplaceholder)
- [**Your First GET Request**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-11/README.md#your-first-get-request)
- [**Reading the Response (Body, Status, Headers)**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-11/README.md#reading-the-response-body-status-headers)
- [**Query Parameters**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-11/README.md#query-parameters)
- [**Sending Headers**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-11/README.md#sending-headers)
- [**POST: Creating Data with a JSON Body**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-11/README.md#post-creating-data-with-a-json-body)
- [**PUT and PATCH: Updating Data**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-11/README.md#put-and-patch-updating-data)
- [**DELETE: Removing Data**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-11/README.md#delete-removing-data)
- [**Collections: Saving Your Requests**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-11/README.md#collections-saving-your-requests)
- [**Environments and Variables**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-11/README.md#environments-and-variables)
- [**Module Activity**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-11/README.md#module-activity)
- [**Sources**](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-11/README.md#sources)

## What Postman Is and Why Use It

**Postman** is an **API client**: an application whose whole job is to build a request, send it to a server, and display the response in a readable way. It is one of the most widely used tools in web development, and both frontend and backend engineers rely on it every day.

Here is why it matters for you as a frontend developer:

- **You can test an API before you code against it.** When a backend engineer hands you an endpoint (remember the "waiter" from lesson 6), you can call it in Postman first, see the exact JSON it returns, and *then* write your `fetch` code with confidence. No more guessing the shape of the data.
- **You isolate problems.** If your app is not showing the users list, is the bug in your code or in the API? Call the endpoint in Postman. If it works there but not in your app, the problem is your code. If it fails in Postman too, the problem is the API. This one habit will save you hours.
- **You can send requests a browser cannot.** Typing a URL in your browser only ever sends a `GET`. Postman lets you send `POST`, `PUT`, `PATCH`, and `DELETE`, attach a **JSON body**, and set custom **headers**, all through a simple form.
- **You keep your work organized.** Postman saves requests into **Collections** so you can re-run them, share them with teammates, and document how an API is used.

In short: Postman is where you *explore and understand* an API. Your React code is where you *use* it.

## Installing Postman

You have two ways to run Postman. Pick whichever is easier for you.

**Option 1 — The desktop app (recommended).**

1. Go to [**www.postman.com/downloads**](https://www.postman.com/downloads/).
2. Download the installer for your operating system (Windows, macOS, or Linux). The site usually detects your system automatically.
3. Run the installer and open Postman when it finishes.
4. On first launch you can **create a free account** or click the option to **skip signing in** and use it in a lightweight mode. An account lets Postman sync your collections across devices, but it is not required to follow this lesson.

**Option 2 — The web version (no installation).**

1. Go to [**go.postman.co**](https://go.postman.co/) (or click *Launch Postman* on the website).
2. Sign in with a free account. The web version needs an account because it stores your work in the cloud.
3. Everything in this lesson works the same in the web version.

> **Note:** To call APIs that run on your own computer (like `http://localhost:3000` from later lessons), the **web** version needs a small helper called the **Postman Desktop Agent**. For public APIs like the one we use below, either version works out of the box. When you reach the React lessons and run a local server, the desktop app is the simpler choice.

## The Practice API: JSONPlaceholder

To practice safely we need a real API that is free, public, and does not require a password. We will use [**JSONPlaceholder**](https://jsonplaceholder.typicode.com/), the same fake REST API we met in lesson 6. It exposes familiar resources like `posts`, `users`, `comments`, and `todos`.

Its base address is:

```
https://jsonplaceholder.typicode.com
```

And it offers endpoints such as:

```
GET     /posts          // read all posts
GET     /posts/1        // read the post with id 1
POST    /posts          // create a new post
PUT     /posts/1        // replace the entire post 1
PATCH   /posts/1        // change part of post 1
DELETE  /posts/1        // delete post 1
```

> **Note:** JSONPlaceholder is a *fake* API. It **pretends** to create, update, and delete data and it sends back a realistic, correct response, but it does not actually save your changes on the server. That is perfect for learning: you can send any request you like without breaking anything.

## Your First GET Request

Let's read the list of posts. In lesson 6 you did this by opening the URL in a browser or the Network tab; now we do it the professional way.

1. Open Postman.
2. Click the **+** (plus) button near the top to open a **new request tab**. (You can also use **New → HTTP Request**.)
3. On the left of the address bar there is a **method dropdown**. Make sure it is set to **`GET`** (it usually is by default).
4. In the **URL field** (the long bar next to the dropdown), type:

   ```
   https://jsonplaceholder.typicode.com/posts
   ```

5. Click the blue **Send** button.

Within a moment, the bottom half of the window fills with the **response**: a big JSON array of post objects. Congratulations, you just called an API without writing any code.

Now try a single resource. Change the URL to:

```
https://jsonplaceholder.typicode.com/posts/1
```

Press **Send** again. This time you get back one object instead of a list:

```json
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur ..."
}
```

## Reading the Response (Body, Status, Headers)

The response panel has three parts you should learn to read. They map exactly onto the concepts from lesson 6.

**1. The Body.** This is the actual data the server sent back, shown in the large area at the bottom. For a JSON API this is your JSON. Postman gives you view options above the body:

- **Pretty** — nicely formatted and color-coded (the default; easiest to read).
- **Raw** — the exact text as it came over the wire.
- **Preview** — renders the body as a web page if it happens to be HTML.

**2. The Status code.** Look at the top-right of the response panel for something like:

```
200 OK        Time: 240 ms        Size: 1.2 KB
```

That **`200 OK`** is the **HTTP status code** from lesson 6. Remember the families:

- **2xx** — success (`200 OK`, `201 Created`).
- **4xx** — *you* made a mistake (`404 Not Found`, `400 Bad Request`).
- **5xx** — the *server* had a problem.

Try requesting a resource that does not exist to see a `4xx`:

```
GET https://jsonplaceholder.typicode.com/posts/99999
```

You will get **`404 Not Found`** and an empty body. Postman also shows the **Time** (how long the request took) and the **Size** of the response, which are handy for spotting slow endpoints.

**3. The Headers.** Click the **Headers** tab inside the response panel to see the **response headers**, extra information *about* the response that is not part of the body. A common one is:

```
Content-Type: application/json; charset=utf-8
```

That header is how your app knows the body is JSON. Headers are metadata: they describe the message rather than being the message itself.

## Query Parameters

Sometimes you do not want *all* the data, you want a filtered slice of it. You do that with **query parameters**: extra `key=value` pairs added to the end of a URL after a `?`, separated by `&`.

For example, JSONPlaceholder lets you fetch only the posts written by user `1`:

```
https://jsonplaceholder.typicode.com/posts?userId=1
```

You could type that whole string into the URL bar, but Postman has a nicer way:

1. Type the base URL `https://jsonplaceholder.typicode.com/posts`.
2. Click the **Params** tab just below the address bar.
3. Add a row with **Key** = `userId` and **Value** = `1`.

As you type, Postman **automatically builds the `?userId=1`** onto the URL for you. Press **Send** and notice the response now contains only that user's posts. You can add more rows (for example `userId` and `_limit`) and Postman joins them with `&`.

```
https://jsonplaceholder.typicode.com/posts?userId=1&_limit=3
```

Query parameters are perfect for **filtering, sorting, and pagination**, all without changing the endpoint itself.

## Sending Headers

Just as responses have headers, so do **requests**. A **request header** is metadata you attach to *your* request to tell the server something about it, for example, what format you are sending, or a token that proves who you are.

To add one:

1. With a request open, click the **Headers** tab below the address bar (this is the *request* Headers tab, not the response one).
2. Add a row, for example **Key** = `Content-Type` and **Value** = `application/json`.

The two headers you will meet most often are:

- **`Content-Type`** — tells the server what format the **body you are sending** is in. For JSON that is `application/json`.
- **`Authorization`** — carries a credential, such as `Bearer <token>`, so a protected API knows you are allowed to call it. (Public APIs like JSONPlaceholder do not need this, but almost every real one will.)

> **Note:** When you add a JSON body in the next section using Postman's **raw → JSON** option, Postman is smart enough to set `Content-Type: application/json` for you automatically. It is still worth knowing the header exists, because you will set it by hand when you write `fetch` code later.

## POST: Creating Data with a JSON Body

A `GET` just reads, so it carries no body. To **create** data with `POST`, we need to *send* data along with the request, and that data is the **request body**. For a JSON API, the body is a JSON object.

Let's create a new post:

1. Open a new request tab.
2. Set the method dropdown to **`POST`**.
3. Enter the URL:

   ```
   https://jsonplaceholder.typicode.com/posts
   ```

4. Click the **Body** tab (below the address bar).
5. Select the **raw** option.
6. In the format dropdown on the right (it usually says *Text*), choose **JSON**. Postman turns the body editor into a JSON editor and sets the `Content-Type` header for you.
7. Type the object you want to create:

   ```json
   {
     "title": "The Force Awakens",
     "body": "A galaxy far, far away.",
     "userId": 1
   }
   ```

8. Press **Send**.

The server answers with **`201 Created`** and echoes your object back, now with an `id` the server assigned:

```json
{
  "title": "The Force Awakens",
  "body": "A galaxy far, far away.",
  "userId": 1,
  "id": 101
}
```

Notice the status is **`201 Created`**, not `200`. That `2xx` code specifically means "I successfully created a new resource." Remember, JSONPlaceholder does not truly save it, but it responds exactly as a real API would, so the *shape* of what you learn here is 100% real.

## PUT and PATCH: Updating Data

Updating works just like `POST`: you choose the verb, target the specific resource, and send a JSON body. The difference between the two verbs is the one from lesson 6:

- **`PUT`** replaces the **entire** record. Send the whole object.
- **`PATCH`** changes **only part** of the record. Send just the field(s) you want to change.

**PUT example** — replace post `1` completely:

1. Method **`PUT`**, URL `https://jsonplaceholder.typicode.com/posts/1`.
2. **Body → raw → JSON**:

   ```json
   {
     "id": 1,
     "title": "Return of the Jedi",
     "body": "The Empire strikes out.",
     "userId": 1
   }
   ```

3. **Send**. You get back **`200 OK`** with the full updated object.

**PATCH example** — change only the title of post `1`:

1. Method **`PATCH`**, URL `https://jsonplaceholder.typicode.com/posts/1`.
2. **Body → raw → JSON**:

   ```json
   {
     "title": "The Empire Strikes Back"
   }
   ```

3. **Send**. You get back **`200 OK`** with the record, where only the title changed and the other fields kept their original values.

The mental model: point the verb at the exact resource (`/posts/1`), and let the body describe the change.

## DELETE: Removing Data

`DELETE` removes a resource. It targets a specific item and usually needs no body at all.

1. Method **`DELETE`**, URL `https://jsonplaceholder.typicode.com/posts/1`.
2. Leave the **Body** empty.
3. **Send**.

You get back **`200 OK`** and an empty object `{}`, the API's way of saying "done, it is gone." (On JSONPlaceholder the post is not really deleted, but a real API would remove it.)

## Collections: Saving Your Requests

So far every request has lived in a throwaway tab. Close it and your work is gone. **Collections** fix that: a **Collection** is a saved, named group of requests that belong together, like a folder for one API or one feature.

To create one and save a request:

1. In the left sidebar, click **Collections**, then the **+** to create a new collection. Name it, for example, `JSONPlaceholder Practice`.
2. Open (or rebuild) your `GET /posts` request.
3. Click **Save** (top-right of the request, or press the save shortcut). Choose your new collection as the destination and give the request a clear name like `Get all posts`.

Now that request lives inside the collection permanently. Repeat for your `POST`, `PUT`, `PATCH`, and `DELETE` requests. The benefits are immediate:

- **Re-run any request** with one click, no retyping.
- **Group related calls** so an API's whole surface is documented in one place.
- **Share** the collection with teammates, or export it as a file, so everyone tests the API the same way.

Think of a collection as the *saved game* of your API exploration: you can always come back and pick up exactly where you left off.

## Environments and Variables

Notice how we typed `https://jsonplaceholder.typicode.com` over and over. Real projects have several servers, a **local** one on your machine, a **staging** one for testing, and a **production** one for real users, and the URL differs for each. Retyping (and re-editing) that everywhere is tedious and error-prone.

**Variables** solve this. A variable is a named placeholder you write in double curly braces, like `{{baseUrl}}`, and Postman substitutes its real value when it sends the request. An **Environment** is a named set of those variable values, so you can flip between "local" and "production" with a single dropdown.

A beginner-friendly setup:

1. In the left sidebar open **Environments** and create a new one called `JSONPlaceholder`.
2. Add a variable:
   - **Variable**: `baseUrl`
   - **Value**: `https://jsonplaceholder.typicode.com`
3. Save it, then select it in the **environment dropdown** at the top-right of Postman.
4. Now rewrite your requests to use the variable instead of the literal URL:

   ```
   {{baseUrl}}/posts
   {{baseUrl}}/posts/1
   ```

When you press **Send**, Postman swaps `{{baseUrl}}` for the real value. To point every request at a different server later, you change the variable in one place, not in a dozen requests.

Variables are also the safe home for **secrets** like API tokens: you store the token once as a variable (for example `{{token}}`) and reference it in your `Authorization` header, instead of pasting it into every request.

> **Note:** Postman has several variable *scopes* (global, environment, collection, and more). As a beginner, you only need **environment variables** like the `baseUrl` above. The other scopes exist for larger projects and you can learn them later.

## Module Activity

Build a small collection that exercises every verb against JSONPlaceholder. Do the work in Postman and write your answers in a text file.

**Part 1 — Set up.**

1. Install Postman (desktop or web).
2. Create an environment named `JSONPlaceholder` with a `baseUrl` variable set to `https://jsonplaceholder.typicode.com`, and select it.
3. Create a collection named `JSONPlaceholder Practice`.

**Part 2 — Read (GET).**

1. Save a request `Get all posts` → `GET {{baseUrl}}/posts`. Send it and note the **status code**.
2. Save a request `Get one post` → `GET {{baseUrl}}/posts/1`.
3. Using the **Params** tab, save `Get posts by user` → `GET {{baseUrl}}/posts?userId=2`. How many posts come back?
4. Request `{{baseUrl}}/posts/99999` and write down the status code and which family (2xx/4xx/5xx) it belongs to.

**Part 3 — Create, update, delete.**

1. Save `Create post` → `POST {{baseUrl}}/posts` with a JSON body of your own (use a Star Wars or game theme if you like, e.g. a post titled `"Level Up"`). What **status code** comes back, and what `id` does the server assign?
2. Save `Replace post` → `PUT {{baseUrl}}/posts/1` sending a full JSON object.
3. Save `Edit post title` → `PATCH {{baseUrl}}/posts/1` sending **only** a `title`. Confirm the other fields stayed the same in the response.
4. Save `Delete post` → `DELETE {{baseUrl}}/posts/1`. What status code and body come back?

**Part 4 — Reflect.**

In two or three sentences, explain *why* calling an endpoint in Postman first (before writing `fetch` code) helps you find bugs faster. Tie your answer back to the client/server idea from [lesson 6](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-6/README.md#client-and-server).

## Sources

- [**Postman — official website & downloads**](https://www.postman.com/downloads/)
- [**Postman Learning Center — Getting started**](https://learning.postman.com/docs/getting-started/overview/)
- [**Postman Learning Center — Sending your first request**](https://learning.postman.com/docs/getting-started/first-steps/sending-the-first-request/)
- [**Postman Learning Center — Collections**](https://learning.postman.com/docs/collections/collections-overview/)
- [**Postman Learning Center — Managing environments**](https://learning.postman.com/docs/sending-requests/variables/managing-environments/)
- [**Postman Learning Center — Using variables**](https://learning.postman.com/docs/sending-requests/variables/variables/)
- [**MDN — HTTP request methods (verbs)**](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
- [**MDN — HTTP response status codes**](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- [**MDN — HTTP headers**](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
- [**MDN — JSON**](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON)
- [**JSONPlaceholder — free fake REST API for practice**](https://jsonplaceholder.typicode.com/)
