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

## Title

The title tag let us set the title of the web page we are working on:

**Example:** `<title>HTML: HyperText Markup Language | MDN</title>`.

![image](https://user-images.githubusercontent.com/58167190/179821111-5622d54b-c7ea-484e-a1ea-f25689a8be52.png)

## Body

This tag represents the content of a web page. There can be only one body inside a web page.

**Example:**

```
<body>
  <text>
    This is an example test
  </text>
</body>
```

## Header

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

![image](https://user-images.githubusercontent.com/58167190/180033731-b25625bd-57d1-471f-ac9f-c0ba4d81f810.png)

## Footer

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

![image](https://user-images.githubusercontent.com/58167190/180033986-c2869494-bec6-48b7-9382-e018eda1aeae.png)

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

![image](https://user-images.githubusercontent.com/58167190/180034113-8dc994ce-74dd-4cac-aa9e-0b66d3c042c9.png)

## P

This HTML element defines a paragraph.

**Example:**

```
<div>
  <h2>This is a header</h2>
  <p> And this is an example of a pragraph. usually this kind of elements will do line breakes by itself.</p>
</div>
```

![image](https://user-images.githubusercontent.com/58167190/180034208-23c47a83-6d93-4efe-9e35-ebd1bc610d97.png)

## Div

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

![image](https://user-images.githubusercontent.com/58167190/180034300-3fe13639-0d17-4dd7-a6d6-9b848aa61ebc.png)

## Img

This item is pretty self-explanatory. It does render an image with a given image soruce (online or offline).

**Example:**

```
<div>
  <text> In here you will find an image>
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/2f/Google_2015_logo.svg/200px-Google_2015_logo.svg.png" alt="img-example"/>
</div>
```

![image](https://user-images.githubusercontent.com/58167190/180034326-114d4e88-c17d-4276-a4f2-138c88952273.png)

## Nav

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

![image](https://user-images.githubusercontent.com/58167190/180034569-9b935520-27b4-4a61-89bc-3ab61470c3bb.png)

## UL
  
This element represents an unordered list.
  
**Example:**
  
```
  <ul>
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
  </ul>
```
  
![image](https://user-images.githubusercontent.com/58167190/180034667-90fbfea9-d5c9-4da3-b199-d7687200b5a9.png)
  
## OL
  
This element represents an ordered list.
  
**Example:**
  
```
  <ol>
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
  </ol>
```
  
![image](https://user-images.githubusercontent.com/58167190/180034760-3ee2203d-0092-443b-88d9-1f9b1ebcb60b.png)
  
## LI
  
This is a plain item to be used inside of a list.
  
**Example:**
  
```
  <ol>
    <li>Item 1</li>
    <li>Item 2</li>
  </ol>
```
  
![image](https://user-images.githubusercontent.com/58167190/180034773-dcc5b475-71da-49f4-97c1-da38a4d119df.png)

Sources: [**Mozilla**](https://developer.mozilla.org/en-US/docs/Web/HTML).
