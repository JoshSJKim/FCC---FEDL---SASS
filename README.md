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