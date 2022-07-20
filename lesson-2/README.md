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

**Important note: **

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

## Sources

- [**Mozilla**](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [**W3Schools**](https://www.w3schools.com/css/default.asp)
