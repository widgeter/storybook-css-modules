# Storybook CSS Modules preset &middot; [![npm package](https://img.shields.io/npm/v/storybook-css-modules?color=green&label=npm&style=flat-square)](https://www.npmjs.com/package/storybook-css-modules)

Storybook preset addon to add _CSS Modules_ capabilities.

<br />

## Installation

```sh
npm install -D storybook-css-modules
```

<br />

## Configuration

Next, update `.storybook/main.js` to the following:

```js
// .storybook/main.js

module.exports = {
  stories: [
    // ...
  ],
  addons: [
    // Other Storybook addons

    "storybook-css-modules", // 👈 The addon registered here
  ],
};
```

By default this preset configured _CSS Modules_ with this options:

```json
{
  "importLoaders": 1,
  "modules": {
    "localIdentName": "[path][name]__[local]--[hash:base64:5]"
  }
}
```

If you need specific different options, override this in `.storybook/main.js` using _cssModulesLoaderOptions_, example:

```js
// .storybook/main.js

const { getLocalIdentName } = require("css-loader-shorter-classnames");
const getLocalIdent = getLocalIdentName();

module.exports = {
  stories: [
    // ...
  ],
  addons: [
    // Other Storybook addons

    {
      name: "storybook-css-modules",
      options: {
        cssModulesLoaderOptions: {
          importLoaders: 1,
          modules: {
            getLocalIdent,
          },
        },
      },
    },
  ],
};
```

<br />

## Usage

This Storybook addon automatically imports all ".modules.css" files as CSS Modules using the specified options. 

(Code for ReactJs, find your framework in [examples](#examples))

<br />

```js
// Button.stories.jsx

import React from "react";
import Button from "./Button.jsx"
import styles from "./Button.modules.css"

export default {
  title: "Button",
  component: Button,
};

const Template = (args) => <Button {...args}>Button</Button>

export const Default = (args) => <Template {...args} />;

// Story using CSS Modules
export const WithCSSModules = () => (
  <Template 
    {...args}
    className={styles.Button}  // 👈 
  />
);

```


```css
/* Button.module.css */

.Button {
  background: #000;
  color: #fff;
  border: 1px solid #000;
  height: 36px;
  padding: 5px 10px;
}
```

<br />

## Examples

- [React](https://github.com/onwidget/storybook-css-modules/tree/main/examples/react)
- [Preact](https://github.com/onwidget/storybook-css-modules/tree/main/examples/preact)
- [Vue 3](https://github.com/onwidget/storybook-css-modules/tree/main/examples/vue3)