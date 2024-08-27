# HTML

[**HTML**](https://developer.mozilla.org/en-US/docs/Web/HTML) is the most basic building block of the web. It defines the meaning and structure of web content.

## Module Content

- [HTML Tags](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-1/README.md#html-tags)
- [Module Activity](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-1/README.md#module-activity)
- [Sources](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-1/README.md#sources)

## HTML tags

**HTML** uses "markup" to annotate text, images, and other content for display in a Web browser.

The **HTML tags** usually have the following syntax (way to structure the code):

```
<tag attribute1="value1" attribute2="value2">
  children
</tag>
```

Where the **`tag`** can by **HTML tag** like `div`, `nav`, `h1`, the **`attribute`** are **properties** that can provide extra behavior to each tag and the **children** are all elements that are between the **openning tag** `<>` and the **closing tag** `</>`. Please note that the items used like `tag`, `attribute1`, `attribute2` and `children` are only for **exemplification purposes** and are not **actual HTML elements**.

**Note**: The usual way the **tags** are structured is with an **openning tag** and a **closing tag**. 

Like here:

```
<p>This is a text</p>
```

However there are **special cases** like the `img` tag, that is **self-closing**, `<img />` where the **oppening and closing tag** are **combined**.

Usually the **attributes** go in the **openning tag**, like `<a href="https://wikipedia.org">Wikipedia</a>`, where **`href`** is an **attribute**.

However, for the tags that are **self-closing**, the attributes go on the **self-closing** tag, before the symbol `/`, like in here: `<img src="htpps://wikipedia.org" />`, where `src` is an **attribute**.

**HTML markup includes** special "elements" such as:

1. [`<title>`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-1/README.md#title).
2. [`<body>`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-1/README.md#body).
3. [`<header>`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-1/README.md#header).
4. [`<footer>`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-1/README.md#footer).
5. [`<section>`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-1/README.md#section).
6. [`<p>`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-1/README.md#p).
7. [`<div>`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-1/README#div.md).
8. [`<img>`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-1/README#img.md).
9. [`<nav>`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-1/README#nav.md).
10. [`<ul>`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-1/README#ul.md).
11. [`<ol>`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-1/README#ol.md).
12. [`<li>`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-1/README#li.md).
13. [`<a>`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-1/README.md#a).

And many others...

### title

`<title></title>`

The **title** tag let us set the title of the web page (the name of that will be displayed on the tab) we are working on:

**Example:** `<title>HTML: HyperText Markup Language | MDN</title>`.

![image](https://user-images.githubusercontent.com/58167190/179821111-5622d54b-c7ea-484e-a1ea-f25689a8be52.png)

### body

`<body></body>`

This tag represents the full content of a web page. There can be only one body inside a web page. This tag should contain any other tags that are not part of the **metadata**.

**Example:**

```
<body>
  <p>
    This is an example test
  </p>
</body>
```

### header

`<header></header>`

The **header** represents introductory content (we could think on magazines and newspaper, where each article has a main header to describe what does the article talk about). Please notice that this tag does not break the content into different **sections**.

**Example:**

```
<body>
  <h1>
    This is a header example
  </h1>
  <p>And this is a random text</p>
</body>
```

![image](https://user-images.githubusercontent.com/58167190/180033731-b25625bd-57d1-471f-ac9f-c0ba4d81f810.png)

### footer

`<footer></footer>`

In a webpage, this element typically contains information about the author, copyright or relevant links. It is usually found at the bottom of a web page.

**Example:**

```
  <div>
    <h1>
      This is a header example
    </h1>
    <p>And this is a random text \n</p>
    <footer>
      In this place you will find <a href="https://www.google.com">useful links</a>
    </footer>
  </div>
```

![image](https://user-images.githubusercontent.com/58167190/180033986-c2869494-bec6-48b7-9382-e018eda1aeae.png)

### section

`<section></section>`

This element represents a **section** of a document. It should have a heading element. It is usually used to organize information by subject.

**Example:**

```
<body>
  <h1>This is a section example</h1>
  <section>
    <h2>
      This is a header example
    </h2>
    <p>And this is a random text</p>
  </section>
  <section>
    <h2>
      This is a header example 2
    </h2>
    <p>And this is a random text 2</p>
  </section>
</body>
```

![image](https://user-images.githubusercontent.com/58167190/180034113-8dc994ce-74dd-4cac-aa9e-0b66d3c042c9.png)

### p

`<p></p>`

This HTML element defines a **paragraph**. It is the most used tag when it comes to **texts**. Each paragraph includes a **line break** at the end by default.

**Example:**

```
<div>
  <h2>This is a header</h2>
  <p> And this is an example of a pragraph. usually this kind of elements will do line breakes by itself.</p>
</div>
```

![image](https://user-images.githubusercontent.com/58167190/180034208-23c47a83-6d93-4efe-9e35-ebd1bc610d97.png)

### div

`<div></div>`

This is one of the most relevant items of HTML. It groups some other elements. The **div** is a container (this means, it is used to **graphically** group other items inside of it).

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

### img

`<img />`

This item is pretty self-explanatory. It does render an **image** with a given image soruce (online or offline).

**Note**: this is one of the **HTML** items that is **self-closing**. This means, we don't have an opening `<>` and a `</>` closing tag, but it **opens** and **closes** in the same tag, like this: `< />`.

**Example:**

```
<div>
  <p> In here you will find an image </p>
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/2f/Google_2015_logo.svg/200px-Google_2015_logo.svg.png" alt="img-example"/>
</div>
```

![image](https://user-images.githubusercontent.com/58167190/180034326-114d4e88-c17d-4276-a4f2-138c88952273.png)

### nav

`<nav></nav>`

The purpose of this element is to provide **navigation** links (elements that can be clicked and usually will take a user to another section or page).

**Example:**

```
<div>
  <nav>
    <a href="https://www.google.com.mx/">Google</a>
    <a href="https://es.wikipedia.org/wiki/Wikipedia:Portada">Wikipedia</a>
    <a href="https://www.youtube.com/">Youtube</a>
  </nav>
  <p>This is different from the navbar</p>
<div>
```

![image](https://user-images.githubusercontent.com/58167190/180034569-9b935520-27b4-4a61-89bc-3ab61470c3bb.png)

### ul

`<ul></ul>`
  
This element represents an **unordered** list. 

**Note**: This element requires to be complemented with the `<li>` (list item) tag.
  
**Example:**
  
```
  <ul>
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
  </ul>
```
  
![image](https://user-images.githubusercontent.com/58167190/180034667-90fbfea9-d5c9-4da3-b199-d7687200b5a9.png)
  
### ol

`<ol></ol>`
  
This element represents an **ordered** list.

**Note**: This element requires to be complemented with the `<li>` (list item) tag.
  
**Example:**
  
```
  <ol>
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
  </ol>
```
  
![image](https://user-images.githubusercontent.com/58167190/180034760-3ee2203d-0092-443b-88d9-1f9b1ebcb60b.png)
  
### li

`<li></li>`
  
This is a plain item to be used inside of a list. This, at the same time, can contain other elements inside of it.
  
**Example:**
  
```
  <ol>
    <li>Item 1</li>
    <li>Item 2</li>
  </ol>
```
  
![image](https://user-images.githubusercontent.com/58167190/180034773-dcc5b475-71da-49f4-97c1-da38a4d119df.png)

### a

`<a></a>`
  
This element makes its **children** a **hyperlink**.
  
**Example:**
  
```
  <a href="https://es.wikipedia.org/wiki/Wikipedia:Portada">Wikipedia</a>
```

## Module activity

Create a menu for a pizza restaurant (4 pizzas). It needs to fit the following requirements:

- Have a `<body>` tag.
- Have a `<h>` tag (for the types of pizza that we have).
- Have images `<img>` (regarding each image file).
- Have descriptions with `<p>` for describing each pizza. 
- An unordered list `ul` describing pizza dough types.

**Tip:** Group each pizza type into a `div` tag.

**Resolution**

```
<!DOCTYPE html>
<html lang="en">
   <head>
      <meta charset="UTF-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <meta http-equiv="X-UA-Compatible" content="ie=edge" />
      <title>Pizza Menu</title>
   </head>
   <body>
      <div
         style="
         background-color: #eb4034;
         display: flex;
         flex: 1;
         color: white;
         padding-left: 20px;
         padding-right: 20px;
         flex-direction: column;
         "
         >
         <section>
            <div>
               <h1>
                  Giancarlo's Pizza bistro
               </h1>
               <p>
                  In Giancarlo's pizza bistro, you will find a wide variety of
                  old-fashioned italian pizzas. We have a wide menu and you can select
                  among all the different crusts that we have available for you.
                  Please, take a look of our fantastic menu.
               </p>
            </div>
         </section>
         <section>
            <h2>Pizza menu</h2>
            <div>
               <h3>Margherita Pizza</h3>
               <img
                  src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c8/Pizza_Margherita_stu_spivack.jpg/220px-Pizza_Margherita_stu_spivack.jpg"
                  alt="margherita"
                  />
               <p>
                  <b><i>Pizza Margherita</i></b> (more commonly known in English as Margherita
                  pizza) is a typical Neapolitan pizza, made with San Marzano
                  tomatoes, mozzarella cheese, fresh basil, salt, and extra-virgin
                  olive oil.
               </p>
               <p>
               You can choose for this pizza among our delicious crusts:
               </p>
               <ul>
                  <li>Stuffed Crust.</li>
                  <li>Cracker Crust.</li>
                  <li>Flat Bread Crust.</li>
                  <li>Thin Crust.</li>
                  <li>Cheese Crust Pizza.</li>
                  <li>Thick Crust Pizza.</li>
                  <li>Wrapping It Up.</li>
               </ul>
            </div>
            <div>
               <h3>Pepperoni Pizza</h3>
               <img
                  src="https://cdn.tasteatlas.com/images/dishes/b05a0af72ad845f3a6abe16143d7853a.jpg"
                  alt="pepperoni"
                  style="width: 220px"
                  />
               <p>
                  <b><i>Pepperoni Pizza</i></b> is an American pizza variety which includes one of the country's most beloved toppings. Pepperoni is actually a corrupted form of peperoni (one “p”), which denotes a large pepper in Italian, but nowadays it denotes a spicy salami, usually made with a mixture of beef, pork, and spices.

                  The popularity of pepperoni pizza had only started to rise in the 1950s. Nowadays, beef pepperoni pizza is the most popular pizza variety, but there are also versions such as fish pepperoni pizza and port pepperoni pizza. The preparation varies from one state to another, but the popularity of this pizza has made it a staple across the United States, and it’s usually prepared simply with mozzarella, tomato sauce, and pepperoni.
               </p>
               <p>
               You can choose for this pizza among our delicious crusts:
               </p>
               <ul>
                  <li>Stuffed Crust.</li>
                  <li>Cracker Crust.</li>
                  <li>Flat Bread Crust.</li>
               </ul>
            </div>
            <div>
               <h3>Mushroom Pizza</h3>
               <img
                  src="https://www.homecookingadventure.com/wp-content/uploads/2022/01/mushroom-pizza.jpg"
                  alt="mushroom"
                  style="width: 200px"
                  />
               <p>
                  <b><i>Mushroom pizza</i></b> has a thin and crispy crust, right amount of mushrooms and a combination of spices which turns into a delicious Italian pizza.
               </p>
               <p>
               You can choose for this pizza among our delicious crusts:
               </p>
               <ul>
                  <li>Stuffed Crust.</li>
                  <li>Cracker Crust.</li>
                  <li>Thick Crust Pizza.</li>
                  <li>Wrapping It Up.</li>
               </ul>
            </div>
            <div>
               <h3>Mexican Pizza</h3>
               <img
                  src="https://life-in-the-lofthouse.com/wp-content/uploads/2013/07/Mexican-Pizza4.jpg"
                  alt="mexican"
                  style="height: 300px"
                  />
               <p>
                  <b><i>Mexican Pizza</i></b> start out with a crisp flour tortilla topped with refried beans, a seasoned ground beef mixture and another crispy tortilla. Zesty enchilada sauce is then spread over the top followed by a sprinkling of cheddar and pepper-jack cheese, diced tomato, green onion and olives. To make the cheese all melty and bubbly, the pizza is placed in the oven for 5 minutes, creating a warm, gooey Mexican Pizza ready to be devoured!
               </p>
               <p>
               You can choose for this pizza among our delicious crusts:
               </p>
               <ul>
                  <li>Thick Crust Pizza.</li>
                  <li>Wrapping It Up.</li>
               </ul>
            </div>
         </section>
      </div>
   </body>
</html>
```

**Output:**

![image](https://user-images.githubusercontent.com/58167190/180043376-f72801ec-a81c-45b4-b8fe-d0185ad25739.png)

![image](https://user-images.githubusercontent.com/58167190/180043457-31997397-31ee-4571-916c-710462059312.png)

![image](https://user-images.githubusercontent.com/58167190/180043508-e1af9090-63ec-4495-9738-d90b0c16ae45.png)

![image](https://user-images.githubusercontent.com/58167190/180043551-19823153-9ee7-4e8f-a2ee-da5f11156a24.png)

**Resolution Notes:**

Please notice that `style` property is used multiple times. At this part of the course, is not mandatory to worry about this property. The only thing you need to know, is that helps us providing some styles to our tags and that when having large images, this property must be used to properly resizing them as shown in the example. Also `<b>` and `<i>` tags are used, representing **bold** and *italic* texts, respectively. The output here is shown as cropped screenshots, the real output is a scrollable page.

## Sources

- [**Mozilla**](https://developer.mozilla.org/en-US/docs/Web/HTML).


