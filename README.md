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
<style type='text/scss'>
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
<style type='text/scss'>
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

## Create Reusable CSS with Mixins

- In SASS, a `mixin` is a group of CSS declaration that can be reused throughout the stylesheet.
- As new CSS features are introduced, it takes time before they are fully adopted for use in all browsers.
- As features are added to browsers, CSS rules using them may need vendor prefixes

```html
<style type="text/scss">

div {
  -webkit-box-shadow: 0px 0px 4px #fff;
  -moz-box-shadow: 0px 0px 4px #fff;
  -ms-box-shadow: 0px 0px 4px #fff;
  box-shadow: 0px 0px 4px #fff;
}

</style>
```

- If it becomes necessary to re-write this rule for all elements that have `box-shadow`, it'll be a lot of typing.
- `mixins` are like functions for CSS.

```html
<style type="text/scss">

  @mixin box-shadow($x, $y, $blur, $c){ 
  -webkit-box-shadow: $x $y $blur $c;
  -moz-box-shadow: $x $y $blur $c;
  -ms-box-shadow: $x $y $blur $c;
  box-shadow: $x $y $blur $c;
}

</style>
```

- The definition begins with `@mixin` followed by a custom name.
- The parameters are optional.
- Call a `mixin` using the `@include` directive

```html
<style type="text/scss">

  @mixin border-radius($radius) {
    -webkit-border-radius: $radius;
    -moz-border-radius: $radius;
    -ms-border-radius: $radius;
    border-radius: $radius;
  }

  #awesome {
    width: 150px;
    height: 150px;
    background-color: green;
    @include border-radius(15px);
  }

</style>

<div id="awesome"></div>
```

- the above code will display a 150px by 150px green box with 15px border radius

## Use @if and @else to Add Logic To Your Styles

- The `@if`, `@else if`, and `@else` directives in Sass is useful to test for a specific case
- It works just like the `if` statement in JS

```html
<style type="text/scss">

@mixin border-stroke($val) {
  @if $val == light {
    border: 1px solid black;
  }
  @else if $val == medium {
    border: 3px solid black;
  }
  @else if $val == heavy {
    border: 6px solid black;
  }
  @else {
    border: none;
  }
}

#box {
  width: 150px;
  height: 150px;
  background-color: red;
  @include border-stroke(medium);
}
</style>

<div id="box"></div>
```

- The above code will display a 150px by 150px red box with a 'medium' (3px solid black) border.

## Use @for to Create a Sass Loop

- the `@for` directive adds styles in a loop in a manner very similar to the `for` loop in JS
- There are two ways to the `@for`
  - "start through end" includes the end number as part of the count
  - "start to end" excludes the end number as part of the count

Example

```html
<style type="text/scss">
  @for $i from 1 through 12 {
    .col-#{$i} { width: 100%/12 * $1; }
  }
</style>
```

- the `#{$i}` part is the syntax to combine a variable (i) with text to make a string.
- When the Sass file is converted to CSS, it will look like the following

```html
<style type="text/scss">
  .col-1 {
    width: 8.33333%;
  }

  .col-2 {
    width: 16.66667%;
  }

  ...

  .col-12 {
    width: 100%;
  }
</style>
```

- The `@for` generated 12 options for column widths available as CSS classes.

Another example

```html
<style type='text/scss'>

@for $j from 1 to 6 {
  .text-#{$j} {font-size: 15px * $j}
}

</style>

<p class="text-1">Hello</p>
<p class="text-2">Hello</p>
<p class="text-3">Hello</p>
<p class="text-4">Hello</p>
<p class="text-5">Hello</p>
```

- The above code will display the text "Hello" starting from 15px and increase the font size by 15px * the index value.

## Use @each to Map Over Items in a List

- `@each` directive loops over each item in a list or map.
- On each iteration, the variable gets assigned to the current value from the list or map.

List

```html
<style type="text/scss">

@each $color in blue, red, green {
  .#{$color}-text {color: $color;}
}
</style>
```

map

```html
<style type="text/scss">
$colors: (color1: blue, color2: red, color3: green);

@each $key, $color in $colors {
  .#{$color}-text {color: $color;}
}
</style>
```

- the `$key` variable is required to reference the key values in the map.
- Both of the above codes are converted into the following CSS

```html
<style type="text/scss">
  .blue-text {
    color: blue;
  }

  .red-text {
    color: red;
  }

  .green-text {
    color: green;
  }
</style>
```

Another example

```html
<style type="text/scss">

@each $color in blue, black, red {
  .#{$color}-bg {background-color: $color;}
}


  div {
    height: 200px;
    width: 200px;
  }
</style>

<div class="blue-bg"></div>
<div class="black-bg"></div>
<div class="red-bg"></div>
</style>
```

- the specified colors will be assigned to the variable $color in `.color-bg` class.
- each class will apply the respective color when converted to CSS
- The above code will display three boxes, 200px tall and 200px wide with the specified colors in respective order.

## Apply a Style Until a Condition is Met with @while

- `@while` in Sass works very similarly with the `while` loop in JS.

```html
<style type="text/scss">

$i: 1;
@while $i <= 5 {
  .text-#{$i} {font-size: 15px * $i;}
  $i: $i + 1;
}

</style>
```

- declare a variable `i` and assign it a value of 1.
- while `i` is less than or equal to 5,
- Append the value of `i` to the `.text-` class.
- For each of the `.text-` class, multiply the font size (15px) by the value of the current `i`.
- increment the value of `i` by 1 for every iteration to prevent an infinite loop.
