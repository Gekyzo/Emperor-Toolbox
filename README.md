# Emperor Toolbox

Enhance the generation of stylesheets with the power of Sass.



## Features

### Auto import from Google fonts

Declare your fonts once in the `variables` file and the library will automatically import them.

**Example**

```scss
// variables.scss
$fonts: (
    primary: 'Source Sans Pro',
    secondary: 'Open Sans',
    accent: 'Montserrat',
);

// Compiles as:
@import url("https://fonts.googleapis.com/css?family=Source Sans Pro");
@import url("https://fonts.googleapis.com/css?family=Open Sans");
@import url("https://fonts.googleapis.com/css?family=Montserrat");
```

Remember to keep `$loadFromGoogle` set to `true`.

### Facilitates the use of variables

Thanks to the built-in tools you can easily load any variable with an improved method.

**Example**

```scss
// Autoload fallback fonts
body {
    font-family: font(primary);
}

label {
    font-family: font(accent, secondary);
}

// Compiles as:
body {
  font-family: "Source Sans Pro", arial, sans-serif;
}

label {
  font-family: "Montserrat", "Open Sans", arial, sans-serif;
}
```

### Debugger overlay

Set the `$debug` to true and you will be able to easily know which rules are being applied.

You can debug box layout, the media queries, etc.



## Output styles

There are two working modes, **development** and **production**, each one has a specific npm command. The value of this modes is given by the tasks each one provides.

While running the `dev` command, you will be able to see the sourcemap of your files, all the selectors on extended mode, and all your comments on the CSS file. You can be as explicit as you want with the documentation on the files.

The `prod` command generates a smaller file, faster for the server to load.



## Architecture

This projects defines the following folder structure.

### core

This folder contains various required variables and tools for the library.

> :warning: You don't need to edit any of this files.

### settings

Your variables, lists and maps. Set all your variables in this folder.

> :recycle: You can override any of this settings to your liking.

Its recommended that you name your variables by its abstract key. Avoid specific names such as `$black`, naming `$dark` would be a better practice.


### elements

Redefine the styles for the bare HTML selectors, like h1, table, input...

**Example**

```scss
// elements/_tables.scss
table {
    // The specific rules for this element
}
tr {
    // The specific rules for this element
}
```

### pages

Specific pages styles. Each page has to have it's own sass file. The first line of each file will be its id selector.

**Example**

```scss
// pages/_contact.scss
#page_contact {
    // The specific rules for this page
}
```

### components

Custom classes or ids.

```scss
// components/_product.scss
.product {
    // The specific rules for this element
}
```



## Media queries

You can set your breakpoints on `settings/variables`. Each media query uses some of those variables.

**The breakpoints must define the width when there is a media query change** (including the unit `px`). For example, if you set `s: 480px`, the mobile media query will be applied to devices from 0 - 479px. At 480px the next media query will be applied.

This are the defined media queries. They should cover most of your needs.

-   mobile: small screens. From 0 to `s` (exluded).
-   tablet: medium screens. From `s` (included) to `m` (exluded).
-   desktop: large screens. From `m` (included) onwards.
-   from-tablet: same as tablet AND desktop. From `s` (included) onwards.
