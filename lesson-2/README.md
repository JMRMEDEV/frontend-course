# CSS

[**Cascading Style Sheets (CSS)**](https://developer.mozilla.org/en-US/docs/Web/CSS) is a stylesheet language used to describe the presentation of a document written in HTML or other markup languages (non relevant to this course). CSS describes how elements should be rendered on screen. In simple words: HTML provides document structure and CSS provides styles for such structure.

## Module content

- CSS insertion
- Common CSS properties
- Image manipulation
- Layout
- Module Activity
- Sources

## CSS Insertion

In order to use the different styling and layout properties that CSS provide us, we have to reference our CSS code in our HTML code. For this matter, we have different ways to do it:

- External CSS
- Internal CSS
- Inline CSS

## External CSS

With an external style sheet, you can change the look of an entire website by changing just one file.

Each HTML page must include a reference to the external style sheet file inside the <link> element, inside the head section. The Style Sheets will always be references as a `.css` file format.

**Example:**

```
<!DOCTYPE html>
<html>
  <head>
  <link rel="stylesheet" href="mystyle.css">
  </head>
  <body>
    <h1>This is a heading</h1>
    <p>This is a paragraph.</p>
  </body>
</html>
```

The `.css` files must not include any HTML tags.

A `.css` (in this example `mystyle.css` file might seem like this:

```
body {
  background-color: lightblue;
}

h1 {
  color: navy;
  margin-left: 20px;
}
```

**Important note:**

The units on a CSS file must be placed together with the value. So please do this: `width: 20px` and **do not** this: `width: 20 px`.

## Internal CSS

An internal style sheet may be used if one single HTML page has a unique style. The internal style is defined inside the <style> element, inside the head section.

**Example:**

```
<!DOCTYPE html>
  <html>
  <head>
  <style>
  body {
    background-color: linen;
  }

  h1 {
    color: maroon;
    margin-left: 40px;
  }
  </style>
  </head>
  <body>
    <h1>This is a heading</h1>
    <p>This is a paragraph.</p>
  </body>
</html>
```

## Inline CSS

A case that we already know, based on our previous examples. An inline style may be used to apply a unique style for a single element. To use inline styles, add the style attribute to the relevant element. The style attribute can contain any CSS property.

**Example:**

```
<!DOCTYPE html>
<html>
<body>
  <h1 style="color:blue;text-align:center;">This is a heading</h1>
  <p style="color:red;">This is a paragraph.</p>
</body>
</html>
```

**Note:** An inline style loses many of the advantages of a style sheet (by mixing content with presentation). Use this method sparingly.
  
**Another note:** Please notice that when using **multiple CSS properties**, this are separated using `;` symbol.
  
## Common CSS Properties
  
When dealing with daily frontend tasks, is very likely to face the following type of properties with CSS:

1. [`background-color`]()
2. [`color`]()
3. [`width`]()
4. [`height`]()
5. [`border-radius`]()
6. [`border-style`]()
7. [`border-width`]()
8. [`border-color`]()
9. [`text-decoration-line`]()
10. [`font-size`]()
11. [`text-align`]()
12. [`font-style`]()
13. [`font-weight`]()
  
### background-color
  
As the name suggests, allow us to change the color of an element's background.
  
The CSS colors can be specified in different manners:
  
1. RGB: (`rgb(255, 99, 71)`)
2. Strings: `white`
3. HEX: `#ff6347`
4. HSL: `hsl(9, 100%, 64%)`
  
**Tip:** Google color picker.
  
**Example:**
  
```
<div style="background-color: red">
  <text>Some cool text</text>
</div>  
```
  
![image](https://user-images.githubusercontent.com/58167190/180062050-f7697bb2-1acc-4973-9172-f94d943ea22f.png)
  
### color
  
Allow us to change the "front" color of an element. Mostly used for texts, icons and more.
  
**Example: **
  
```
<div style="background-color: #248f03">
  <text style="color: white">Hello there!</text>
</div>  
```
  
![image](https://user-images.githubusercontent.com/58167190/180062497-098144dd-c216-4d44-b692-8c98e2fe0dda.png)
  
### width
  
Self explanatory. Please notice that the **units** can be `px`, `rem`, `%` and more. Look at the references for more info about this.
  
**Example:**
  
```
<div style="background-color: green; width: 400px;">
  <text style="color: rgb(255, 255, 255);">Hello there!</text>
</div>
<div style="background-color: red; width: 200px;">
  <text style="color: rgb(255, 255, 255);">Hello there!</text>
</div> 
```
  
![image](https://user-images.githubusercontent.com/58167190/180063034-089879fd-367e-442f-9f2a-bf124ed28410.png)
  
### height
  
Self explanatory.
  
**Example:**
  
```
<div style="background-color: green; height: 400px;">
  <text style="color: rgb(255, 255, 255);">Hello there!</text>
</div>
<div style="background-color: red; height: 200px;">
  <text style="color: rgb(255, 255, 255);">Hello there!</text>
</div> 
```
  
![image](https://user-images.githubusercontent.com/58167190/180063305-fe09dc89-4d33-4255-a628-d83461a6c4ea.png)
  
### border-radius
  
This property indicates how rounded do we want our element.
  
**Example:**
  
```
<div style="background-color: green; height: 50px; border-radius: 10px;">
  <text style="color: rgb(255, 255, 255);">Hello there!</text>
</div>
```
  
![image](https://user-images.githubusercontent.com/58167190/180064041-29fec313-0924-4d11-9bca-5c0b8ed4bff9.png)
  
### border-style
  
This element indicates how do we want to show the border line in case wanted. Must go with [`border-width`]() property. Some possible values for the property are `dotted`, `dashed` and `solid`.
  
**Example:**
  
```
<div
  style="
    background-color: green;
    height: 50px;
    border-radius: 10px;
    border-style: solid;
    border-width: 5px;
  "
>
  <text style="color: rgb(255, 255, 255);">Hello there!</text>
</div>  
```
  
![image](https://user-images.githubusercontent.com/58167190/180064413-a5f7bfdd-682d-4515-96a6-e6f079844460.png)
  
### border-width
  
This property describes how wide do we want our borders.
  
**Example:**
  
```
<div
  style="
    background-color: green;
    height: 50px;
    border-radius: 10px;
    border-style: solid;
    border-width: 5px;
  "
>
  <text style="color: rgb(255, 255, 255);">Hello there!</text>
</div>  
```
  
![image](https://user-images.githubusercontent.com/58167190/180064413-a5f7bfdd-682d-4515-96a6-e6f079844460.png)
  
### border-color
  
This property allow us to set a color to the border. Must be used with `border-width` property.
  
**Example:**
  
```
<div
  style="
    background-color: green;
    height: 50px;
    border-radius: 10px;
    border-style: solid;
    border-width: 5px;
    border-color: red;
  "
>
  <text style="color: rgb(255, 255, 255);">Hello there!</text>
</div>  
```
  
![image](https://user-images.githubusercontent.com/58167190/180064981-0fc6caa6-2e59-403c-9a60-56f4962bf1c0.png)
  
### text-decoration-line
  
This property allow us to set different styles to a determined text. Some possible values are `underline`, `line-through`, `overline`, etc.
  
**Example:**
  
```  
<div>
  <text style="text-decoration: underline;">Hello there!</text>
  <text style="text-decoration: line-through;">Hello there!</text>
</div>
```
  
![image](https://user-images.githubusercontent.com/58167190/180065461-620fb24f-0448-4dfa-aec5-00377fb0242a.png)

### font-size
  
Self explanatory.
  
**Example:**
  
```
<div>
  <text style="font-size: 10px;">Size1</text>
  <text style="font-size: 15px;">Size2</text>
  <text style="font-size: 20px;">Size3</text>
</div>  
```
  
![image](https://user-images.githubusercontent.com/58167190/180065760-791067f4-6c8f-4111-b896-2133ef0f9006.png)
  
### text-align

This property allow us to distribute the text the way we want. Possible values `center`, `left` and `right`.
  
**Example:**
  
```
<div>
  <p style="text-align: left;">
    Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod
    tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim
    veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea
    commodo consequat. Duis aute irure dolor in reprehenderit in voluptate
    velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint
    occaecat cupidatat non proident, sunt in culpa qui officia deserunt
    mollit anim id est laborum.
  </p>
  <p style="text-align: center;">
    Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod
    tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim
    veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea
    commodo consequat. Duis aute irure dolor in reprehenderit in voluptate
    velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint
    occaecat cupidatat non proident, sunt in culpa qui officia deserunt
    mollit anim id est laborum.
  </p>
  <p style="text-align: right;">
    Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod
    tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim
    veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea
    commodo consequat. Duis aute irure dolor in reprehenderit in voluptate
    velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint
    occaecat cupidatat non proident, sunt in culpa qui officia deserunt
    mollit anim id est laborum.
  </p>
</div>
```
  
![image](https://user-images.githubusercontent.com/58167190/180066342-fb6244a1-ebe6-4982-9626-5fb667108500.png)
  
### font-style
  
This property allow us to change the style of a text, possible values are `normal`, `italic`, `oblique`.
  
**Example:**
  
```
<div>
  <text style="font-style: normal;">test1</text>
  <text style="font-style: italic;">test2</text>
  <text style="font-style: oblique;">test3</text>
</div>
```
  
![image](https://user-images.githubusercontent.com/58167190/180066833-8b0b53e6-4804-4797-b60d-c0d4832fc490.png)
  
### font-weight
  
This property let us choose how **bold** do we want our texts.
  
**Example:**
  
```
<div>
  <text style="font-weight: bold;">test1</text>
  <text style="font-weight: regular;">test2</text>
  <text style="font-weight: bolder;">test3</text>
</div>
```
  
![image](https://user-images.githubusercontent.com/58167190/180067325-5f344b5b-ac31-461e-a2d1-28c0f1d6be9d.png)
  
## Image manipulation
  
## Layout
  
Layout refers to the order and structure used for displaying the different present elements. It does not make sense to have all the elements together. It usually even in our notes that we take from classes, we structure our information in a manner that can keep calling our attention.
  
In CSS layout, we will find how to distribute the size of different graphic elements in an elegant manner. For such matter, we might use either `flexbox` or `grid` systems. We will review some of the most common layout CSS properties:
  
1. [`display`]()
2. [`flex`]()
3. [`flex-direction`]()
4. [`justify-content`]()
5. [`align-items`]()
6. [`align-content`]()
7. [`column-gap`]()
8. [`row-gap`]()

### display
### flex
### flex-direction
### justify-content
### align-items
### align-content
### column-gap
### row-gap
  
## Module Activity

## Sources

- [**Mozilla**](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [**W3Schools**](https://www.w3schools.com/css/default.asp)
