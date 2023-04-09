# FCC---FEDL---SASS

Intro to SASS (Syntactically Awesome StyleSheets)

## Store Data with Sass Variables

- One feature of Sass that is different from CSS is that it utilizes variables, which are declared and set to store data, similar to JS
- Sass variables are defined using `$` followed by the variable name.

```html
<style>
$main-fonts: Arial, sans-serif;
$headings-color: green;

$text-color: red;

h1 {
    font-family: $main-fonts;
    color: $headings-color;
}

.blog-post, h2 {
    color: $text-color;
}
</style>
```

- Use of variables is convenient because, for example, if you need to change the primary text color of the web page, the only place to edit the code is the variable value.

## Nest CSS with Sass

- Sass allows nesting of CSS rules.
- It makes it convenient to organize a stylesheet.

```html
<style>
nav {
  background-color: red;
}

nav ul {
  list-style: none;
}

nav ul li {
  display: inline-block;
}
```

- Above is a regular CSS rule format.
- With Sass, you can nest child style rules within the respective parent elements, as shown below.

```html
<style>
nav {
  background-color: red;

  ul {
    list-style: none;

    li {
      display: inline-block;
    }
  }
}
</style>
```

- Be mindful of where to place the closing curly braces.