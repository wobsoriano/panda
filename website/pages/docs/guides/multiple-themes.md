---
title: Multi-Theme Tokens
description: Panda supports advance token definition beyond just light/dark mode; theming beyond just dark mode. You can define multi-theme tokens using nested conditions.
---

# Multi-Theme Tokens

Panda supports advance token definition beyond just light/dark mode; theming beyond just dark mode. You can define
multi-theme tokens using nested conditions.

Let's say your application supports a pink and blue theme, and each theme can have a light and dark mode. Let's see how
to model this in Panda.

We'll start by defining the following conditions for these theme and color modes:

```js
const config = {
  conditions: {
    light: '[data-color-mode=light] &',
    dark: '[data-color-mode=dark] &',
    pinkTheme: '[data-theme=pink] &',
    blueTheme: '[data-theme=blue] &'
  }
}
```

> Conditions are a way to provide preset css selectors or media queries for use in your Panda project

Next, we'll define a `colors.text` semantic token for the pink and blue theme.

```js
const theme = {
  // ...
  semanticTokens: {
    colors: {
      text: {
        value: {
          _pinkTheme: '{colors.pink.500}',
          _blueTheme: '{colors.blue.500}'
        }
      }
    }
  }
}
```

Next, we'll modify `colors.text` to support light and dark color modes for each theme.

```js
const theme = {
  // ...
  semanticTokens: {
    colors: {
      text: {
        value: {
          _pinkTheme: { base: '{colors.pink.500}', _dark: '{colors.pink.300}' },
          _blueTheme: { base: '{colors.blue.500}', _dark: '{colors.blue.300}' }
        }
      }
    }
  }
}
```

Now, you can use the `text` token in your styles, and it will automatically change based on the theme and the color
scheme.

```jsx
// use pink and dark mode theme
<html data-theme="pink" data-color-mode="dark">
  <body>
    <h1 className={{ color: 'text' }}>Hello World</h1>
  </body>
</html>

// use pink and light mode theme
<html data-theme="pink">
  <body>
    <h1 className={{ color: 'text' }}>Hello World</h1>
  </body>
</html>
```
