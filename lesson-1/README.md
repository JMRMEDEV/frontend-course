# HTML

[**HTML**](https://developer.mozilla.org/en-US/docs/Web/HTML) is the most basic building block of the Web. It defines the meaning and structure of web content.

HTML uses "markup" to annotate text, images, and other content for display in a Web browser. HTML markup includes special "elements" such as:

1. `<title>`.
2. `<body>`.
3. `<header>`.
4. `<footer>`.
5. `<section>`.
6. `<p>`.
7. `<div>`.
8. `<img>`.
9. `<nav>`.
10. `<ul>`.
11. `<ol>`.
12. `<li>`.

And many others...

# Title

The title tag let us set the title of the web page we are working on:

**Example:** `<title>HTML: HyperText Markup Language | MDN</title>`.

![image](https://user-images.githubusercontent.com/58167190/179821111-5622d54b-c7ea-484e-a1ea-f25689a8be52.png)

# Body

This tag represents the content of a web page. There can be only one body inside a web page.

**Example:**

```
<body>
  <text>
    This is an example test
  </text>
</body>
```

**Output:**

<body>
  <text>
    This is an example test
  </text>
</body>

# Header

The header represents introductory content. Please notice that this tag does not break the content into different sections.

**Example:**

```
<body>
  <h1>
    This is a header example
  </h1>
  <text>And this is a random text</text>
</body>
```

**Output:**
<body>
  <h1>
    This is a header example
  </h1>
  <text>And this is a random text</text>
</body>


![image](https://user-images.githubusercontent.com/58167190/179822267-88565d32-e761-49ff-8178-c4f4021c205e.png)

# Footer

In a webpage, this element typically contains information about the author, copyright or relevant links.

**Example:**

```
  <div>
    <h1>
      This is a header example
    </h1>
    <text>And this is a random text \n</text>
    <footer>
      In this place you will find <a href="https://www.google.com">useful links</a>
    </footer>
  </div>
```

**Output:**
<div>
  <h1>
    This is a header example
  </h1>
  <text>And this is a random text</text>
</div>

![image](https://user-images.githubusercontent.com/58167190/179822464-645ff4d6-b858-4a8c-b324-e1d8ffaec497.png)

# Section

This element represents a section of a document. It should have a heading element.

**Example:**

```
<body>
  <h1>This is a section example</h1>
  <section>
    <h2>
      This is a header example
    </h2>
    <text>And this is a random text</text>
  </section>
  <section>
    <h2>
      This is a header example 2
    </h2>
    <text>And this is a random text 2</text>
  </section>
</body>
```

**Output:**

<body>
  <h1>This is a section example</h1>
  <section>
    <h2>
      This is a header example
    </h2>
    <text>And this is a random text</text>
  </section>
  <section>
    <h2>
      This is a header example 2
    </h2>
    <text>And this is a random text 2</text>
  </section>
</body>

# P

This HTML element defines a paragraph.

**Example:**

```
<div>
  <h2>This is a header</h2>
  <p> And this is an example of a pragraph. usually this kind of elements will do line breakes by itself.</p>
</div>
```

**Output:**

<div>
  <h2>This is a header</h2>
  <p> And this is an example of a pragraph. usually this kind of elements will do line breakes by itself.</p>
</div>

# Div

This is one of the most relevant items of HTML. It groups some other elements.

```
<div>
  <h2>This is a header</h2>
  <p> And this is an example of a pragraph. usually this kind of elements will do line breakes by itself.</p>
</div>
<div>
  <p> This is a different div, wich says is in a different group.</p>
</div>
```

**Output:**

<div>
  <h2>This is a header</h2>
  <p> And this is an example of a pragraph. usually this kind of elements will do line breakes by itself.</p>
</div>


# Img

This item is pretty self-explanatory. It does render an image with a given image soruce (online or offline).

**Example:**

```
<div>
  <text> In here you will find an image>
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/2f/Google_2015_logo.svg/200px-Google_2015_logo.svg.png" alt="img-example"/>
</div>
```

# Nav

The purpose of this element is to rpovide navigation links.

**Example:**

```
<div>
  <nav>
    <a href="https://www.google.com.mx/">Google</a>
    <a href="https://es.wikipedia.org/wiki/Wikipedia:Portada">Wikipedia</a>
    <a href="https://www.youtube.com/">Youtube</a>
  </nav>
  <text>This is different from the navbar</text>
<div>
```

**Output:**

<div>
  <nav>
    <a href="https://www.google.com.mx/">Google</a>
    <a href="https://es.wikipedia.org/wiki/Wikipedia:Portada">Wikipedia</a>
    <a href="https://www.youtube.com/">Youtube</a>
  </nav>
  <h3>  
    <text>This is different from the navbar</text>
  </h3>
<div>
  
![image](https://user-images.githubusercontent.com/58167190/179866725-d6372f9c-697a-420a-9db8-4720ff949679.png)

# UL
  
This element represents an unordered list.
  
**Example:**
  
```
  <ul>
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
  </ul>
```
  
**Output:**
  
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
  
# OL
  
This element represents an ordered list.
  
**Example:**
  
```
  <ol>
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
  </ol>
```
  
**Output:**
  
<ol>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ol>
  
# LI
  
This is a plain item to be used inside of a list.
  
**Example:**
  
```
  <ol>
    <li>Item 1</li>
    <li>Item 2</li>
  </ol>
```
  
**Output:**
  
<ol>
  <li>Item 1</li>
  <li>Item 2</li>
</ol>
