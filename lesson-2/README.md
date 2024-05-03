# CSS

[**Cascading Style Sheets (CSS)**](https://developer.mozilla.org/en-US/docs/Web/CSS) is a stylesheet language used to describe the presentation of a document written in HTML or other markup languages (non relevant to this course). CSS describes how elements should be rendered on screen. In simple words: HTML provides document structure and CSS provides styles for such structure.

## Module content

- [CSS insertion](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#css-insertion)
- [Common CSS properties](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#common-css-properties)
- [Image manipulation](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#image-manipulation)
- [Layout](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#layout)
- [Module Activity](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#module-activity)
- [Sources](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#sources)

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
  <h1 style="color:blue;p-align:center;">This is a heading</h1>
  <p style="color:red;">This is a paragraph.</p>
</body>
</html>
```

**Note:** An inline style loses many of the advantages of a style sheet (by mixing content with presentation). Use this method sparingly.
  
**Another note:** Please notice that when using **multiple CSS properties**, this are separated using `;` symbol.
  
## Common CSS Properties
  
When dealing with daily frontend tasks, is very likely to face the following type of properties with CSS:

1. [`background-color`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#background-color)
2. [`color`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#color)
3. [`width`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#width)
4. [`height`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#height)
5. [`border-radius`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#border-radius)
6. [`border-style`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#border-style)
7. [`border-width`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#border-width)
8. [`border-color`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#border-color)
9. [`text-decoration-line`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#text-decoration-line)
10. [`font-size`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#font-size)
11. [`text-align`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#text-align)
12. [`font-style`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#font-style)
13. [`font-weight`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#font-weight)
  
### background-color
  
As the name suggests, allow us to change the color of an element's background.
  
The CSS colors can be specified in different manners:
  
1. RGB: `rgb(255, 99, 71)`
2. Strings: `white`
3. HEX: `#ff6347`
4. HSL: `hsl(9, 100%, 64%)`
  
**Tip:** Google color picker.
  
**Example:**
  
```
<div style="background-color: red">
  <p>Some cool p</p>
</div>  
```
  
![image](https://user-images.githubusercontent.com/58167190/180062050-f7697bb2-1acc-4973-9172-f94d943ea22f.png)
  
### color
  
Allow us to change the "front" color of an element. Mostly used for ps, icons and more.
  
**Example:**
  
```
<div style="color: #248f03">
  <p style="color: white">Hello there!</p>
</div>  
```
  
![image](https://user-images.githubusercontent.com/58167190/180062497-098144dd-c216-4d44-b692-8c98e2fe0dda.png)
  
### width
  
Self explanatory. Please notice that the **units** can be `px`, `rem`, `%` and more. Look at the references for more info about this.
  
**Example:**
  
```
<div style="background-color: green; width: 400px;">
  <p style="color: rgb(255, 255, 255);">Hello there!</p>
</div>
<div style="background-color: red; width: 200px;">
  <p style="color: rgb(255, 255, 255);">Hello there!</p>
</div> 
```
  
![image](https://user-images.githubusercontent.com/58167190/180063034-089879fd-367e-442f-9f2a-bf124ed28410.png)
  
### height
  
Self explanatory.
  
**Example:**
  
```
<div style="background-color: green; height: 400px;">
  <p style="color: rgb(255, 255, 255);">Hello there!</p>
</div>
<div style="background-color: red; height: 200px;">
  <p style="color: rgb(255, 255, 255);">Hello there!</p>
</div> 
```
  
![image](https://user-images.githubusercontent.com/58167190/180063305-fe09dc89-4d33-4255-a628-d83461a6c4ea.png)
  
### border-radius
  
This property indicates how rounded do we want our element.
  
**Example:**
  
```
<div style="background-color: green; height: 50px; border-radius: 10px;">
  <p style="color: rgb(255, 255, 255);">Hello there!</p>
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
  <p style="color: rgb(255, 255, 255);">Hello there!</p>
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
  <p style="color: rgb(255, 255, 255);">Hello there!</p>
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
  <p style="color: rgb(255, 255, 255);">Hello there!</p>
</div>  
```
  
![image](https://user-images.githubusercontent.com/58167190/180064981-0fc6caa6-2e59-403c-9a60-56f4962bf1c0.png)
  
### text-decoration-line
  
This property allow us to set different styles to a determined p. Some possible values are `underline`, `line-through`, `overline`, etc.
  
**Example:**
  
```  
<div>
  <p style="text-decoration: underline;">Hello there!</p>
  <p style="text-decoration: line-through;">Hello there!</p>
</div>
```
  
![image](https://user-images.githubusercontent.com/58167190/180065461-620fb24f-0448-4dfa-aec5-00377fb0242a.png)

### font-size
  
Self explanatory.
  
**Example:**
  
```
<div>
  <p style="font-size: 10px;">Size1</p>
  <p style="font-size: 15px;">Size2</p>
  <p style="font-size: 20px;">Size3</p>
</div>  
```
  
![image](https://user-images.githubusercontent.com/58167190/180065760-791067f4-6c8f-4111-b896-2133ef0f9006.png)
  
### text-align

This property allow us to distribute the p the way we want. Possible values `center`, `left` and `right`.
  
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
  
This property allow us to change the style of a p, possible values are `normal`, `italic`, `oblique`.
  
**Example:**
  
```
<div>
  <p style="font-style: normal;">test1</p>
  <p style="font-style: italic;">test2</p>
  <p style="font-style: oblique;">test3</p>
</div>
```
  
![image](https://user-images.githubusercontent.com/58167190/180066833-8b0b53e6-4804-4797-b60d-c0d4832fc490.png)
  
### font-weight
  
This property let us choose how **bold** do we want our ps.
  
**Example:**
  
```
<div>
  <p style="font-weight: bold;">test1</p>
  <p style="font-weight: regular;">test2</p>
  <p style="font-weight: bolder;">test3</p>
</div>
```
  
![image](https://user-images.githubusercontent.com/58167190/180067325-5f344b5b-ac31-461e-a2d1-28c0f1d6be9d.png)
  
## Image manipulation
  
The images rendered through HTML might require some adjustments in order to have the desired look and feel. While many `style` properties can be used in the `<img>` tag, there are some others that are specific for this tag. The most relevant: `object-fit` with `fill`, `contain` and `cover` values.
  
1. `fill`
  
![image](https://user-images.githubusercontent.com/58167190/180069520-9a07a696-9ac7-4f0d-9e12-a782f29f7e55.png)

2. `contain`
  
![image](https://user-images.githubusercontent.com/58167190/180069564-77fa782f-c573-4220-92a5-9a6635b4620d.png)

3. `cover`
  
![image](https://user-images.githubusercontent.com/58167190/180069620-4d8f78c2-af5c-4f90-9b9b-b421815b4ff0.png)
  
## Layout
  
Layout refers to the order and structure used for displaying the different present elements. It does not make sense to have all the elements together. It usually even in our notes that we take from classes, we structure our information in a manner that can keep calling our attention.
  
In CSS layout, we will find how to distribute the size of different graphic elements in an elegant manner. For such matter, we might use either `flexbox` or `grid` systems. We will review some of the most common layout CSS properties:
  
1. [`display`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#display)
2. [`flex`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#flex-direction)
3. [`flex-direction`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#justify-content)
4. [`justify-content`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#align-items)
5. [`align-items`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#align-items)
6. [`margin`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#margin)
7. [`padding`](https://github.com/JMRMEDEV/frontend-course/blob/master/lesson-2/README.md#padding)

### display

This CSS property as it is may have different use-cases. But for our purposes we will only focus on the most relevant layout values: `flex` and `grid`. This property tells the container how should display its children. In this course, we will not study `grid` deeply.

**Examples:**

```
<div style="display: flex; background-color: yellow; height: 200px;">
  <div style="background-color: red;">
    <p>Hello there</p>
  </div>
  <div style="background-color: blue;">
    <p>Hello there</p>
  </div>
  <div style="background-color: pink;">
    <p>Hello there</p>
  </div>
</div>
```

![image](https://user-images.githubusercontent.com/58167190/180071615-900677bb-c2c0-4422-9fab-345e2639a2b5.png)

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Static Template</title>
    <style>
      .grid-container {
        display: grid;
        grid-template-columns: auto auto auto;
        background-color: #2196f3;
        padding: 10px;
      }
      .grid-item {
        background-color: rgba(255, 255, 255, 0.8);
        border: 1px solid rgba(0, 0, 0, 0.8);
        padding: 20px;
        font-size: 30px;
        p-align: center;
      }
    </style>
  </head>
  <body>
    <div class="grid-container">
      <div class="grid-item">1</div>
      <div class="grid-item">2</div>
      <div class="grid-item">3</div>
      <div class="grid-item">4</div>
      <div class="grid-item">5</div>
      <div class="grid-item">6</div>
      <div class="grid-item">7</div>
      <div class="grid-item">8</div>
      <div class="grid-item">9</div>
    </div>
  </body>
</html>
```

![image](https://user-images.githubusercontent.com/58167190/180072195-781c5638-b565-4ed8-bcf4-fdda5185ecb0.png)

### flex

This property tell us how much proportion will take the child of a `flex` container. The value (number) set in the flex property, will divide the total space of the container into fractions of the container. For example, if we set three items with `flex: 1`, the space will be divided into three parts and each child will take one of those three parts.

**Example:**

```
<div style="display: flex; background-color: yellow; height: 200px;">
  <div style="background-color: red; flex: 1;">
    <p>Hello there</p>
  </div>
  <div style="background-color: blue; flex: 1;">
    <p>Hello there</p>
  </div>
  <div style="background-color: pink; flex: 1;">
    <p>Hello there</p>
  </div>
</div>
```

![image](https://user-images.githubusercontent.com/58167190/180072769-9697efcc-f869-421e-9580-dfbf47718d92.png)

But... What would happen if we set a `flex: 2` to one of those inner `div`s? Well, now the parent space would be **`4`**: flex `1` + flex `1` + flex `2` = `4` flexes. An the item with `flex: 2` will take `2/4` of the total flex-space:

```
<div style="background-color: red; flex: 2;">
  <p>Hello there</p>
</div>
<div style="background-color: blue; flex: 1;">
  <p>Hello there</p>
</div>
<div style="background-color: pink; flex: 1;">
  <p>Hello there</p>
</div>
```

![image](https://user-images.githubusercontent.com/58167190/180073200-5df1d1f3-1703-4369-a3c3-07bf2376d0b7.png)

What about if we set each `flex` property to `2`? Now we would end with flex `2` + flex `2` + flex `2` = `6` flexes. But as we are taking `2` flex for each element, at the end, we would end with practically the same as setting `flex` to `1`.

```
<div style="display: flex; background-color: yellow; height: 200px;">
  <div style="background-color: red; flex: 2;">
    <p>Hello there</p>
  </div>
  <div style="background-color: blue; flex: 2;">
    <p>Hello there</p>
  </div>
  <div style="background-color: pink; flex: 2;">
    <p>Hello there</p>
  </div>
</div>
```

![image](https://user-images.githubusercontent.com/58167190/180073692-eb00b280-6959-44f6-8799-b5de4ef9e0bb.png)

### flex-direction
  
This property allow us to change the direction of the flex children items. Can be `row`, `column` and their reverse variants `row-reverse` and `column-reverse`.
  
**Example:**
  
```
<div
  style="
    display: flex;
    background-color: yellow;
    height: 200px;
    flex-direction: column;
  "
>
  <div style="background-color: red; flex: 2;">
    <p>Hello there</p>
  </div>
  <div style="background-color: blue; flex: 2;">
    <p>Hello there</p>
  </div>
  <div style="background-color: pink; flex: 2;">
    <p>Hello there</p>
  </div>
</div>  
```
 
![image](https://user-images.githubusercontent.com/58167190/180074467-ebeb5e7b-a903-4c66-98d6-e6f38ca2ac84.png)
  
```
<div
  style="
    display: flex;
    background-color: yellow;
    height: 200px;
    flex-direction: row-reverse;
  "
>
  <div style="background-color: red; flex: 2;">
    <p>Hello there</p>
  </div>
  <div style="background-color: blue; flex: 2;">
    <p>Hello there</p>
  </div>
  <div style="background-color: pink; flex: 2;">
    <p>Hello there</p>
  </div>
</div>
```
  
![image](https://user-images.githubusercontent.com/58167190/180074652-5af37794-87c5-484c-b772-e8bba4389d55.png)
  
### justify-content
  
Let us justify `x-axis` the content of the `flex-container`. Accepts `center`, `flex-start`, `flex-end` and more.
  
```
<div
  style="
    display: flex;
    background-color: yellow;
    height: 200px;
    justify-content: center;
  "
>
  <div style="background-color: red;">
    <p>Hello there</p>
  </div>
  <div style="background-color: blue;">
    <p>Hello there</p>
  </div>
  <div style="background-color: pink;">
    <p>Hello there</p>
  </div>
</div>  
```
  
![image](https://user-images.githubusercontent.com/58167190/180075601-a4fe30a3-bd8d-4b02-907f-f62c840186bc.png)

```
<div
  style="
    display: flex;
    background-color: yellow;
    height: 200px;
    justify-content: flex-end;
  "
>
  <div style="background-color: red;">
    <p>Hello there</p>
  </div>
  <div style="background-color: blue;">
    <p>Hello there</p>
  </div>
  <div style="background-color: pink;">
    <p>Hello there</p>
  </div>
</div>  
```
  
![image](https://user-images.githubusercontent.com/58167190/180075737-2ea7289b-ea94-4628-a1f5-f23b5963f6e3.png)
  
### align-items
  
Let us align the `flex` items in the `y-axis`. Accepts `center`, `flex-start`, `flex-end` and more.
  
```
<div
  style="
    display: flex;
    background-color: yellow;
    height: 200px;
    align-items: flex-end;
  "
>
  <div style="background-color: red;">
    <p>Hello there</p>
  </div>
  <div style="background-color: blue;">
    <p>Hello there</p>
  </div>
  <div style="background-color: pink;">
    <p>Hello there</p>
  </div>
</div>  
```
  
![image](https://user-images.githubusercontent.com/58167190/180076134-13874462-fc3b-4ef9-a7af-5d02c149cb04.png)

```
<div
  style="
    display: flex;
    background-color: yellow;
    height: 200px;
    align-items: center;
  "
>
  <div style="background-color: red;">
    <p>Hello there</p>
  </div>
  <div style="background-color: blue;">
    <p>Hello there</p>
  </div>
  <div style="background-color: pink;">
    <p>Hello there</p>
  </div>
</div>
```
  
![image](https://user-images.githubusercontent.com/58167190/180076306-e2f3e4b6-c3d9-483b-b54e-d7561f074736.png)
  
### margin
  
This property let us set a margin (space into the given direction) to an element. It can be on the `right`, `left`, `top` and `bottom`.
  
**Example:**
  
```
<div
  style="
    display: flex;
    background-color: yellow;
    height: 200px;
    align-items: center;
  "
>
  <div style="background-color: red; margin-top: 40px;">
    <p>Hello there</p>
  </div>
  <div style="background-color: blue; margin-bottom: 50px;">
    <p>Hello there</p>
  </div>
  <div style="background-color: pink; margin-left: 20px;">
    <p>Hello there</p>
  </div>
</div>
```
  
![image](https://user-images.githubusercontent.com/58167190/180077445-1e775202-150a-4f29-a9fb-efec50f83593.png)
  
### padding

This property let us assign a padding (a space that the item itself will take as extra) to an item.
  
**Example:**
  
```
<div
  style="
    display: flex;
    background-color: yellow;
    height: 200px;
    align-items: center;
  "
>
  <div style="background-color: red; padding-top: 40px;">
    <p>Hello there</p>
  </div>
  <div style="background-color: blue; padding-bottom: 50px;">
    <p>Hello there</p>
  </div>
  <div style="background-color: pink; padding-left: 20px;">
    <p>Hello there</p>
  </div>
</div>  
```
  
![image](https://user-images.githubusercontent.com/58167190/180077736-de792e03-c8bc-425a-a9fa-f382c956bcb3.png)
  
## Module Activity
  
By using all that we have learnt in this lesson, we will recreate the follwing calculator:
  
![image](https://user-images.githubusercontent.com/58167190/180083707-c21852c2-a319-43c6-b4e3-2a069ddfa5b5.png)

**Notes:** Inline styling is accepted, but if is achieved through this, the activity will have to be redone with external CSS.

## Sources

- [**Mozilla**](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [**W3Schools**](https://www.w3schools.com/css/default.asp)
