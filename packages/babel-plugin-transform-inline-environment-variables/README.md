# @tysonmatanich/babel-plugin-transform-inline-environment-variables

Inline environment variables and keep track of which environment variables were replaced

## Example

### In

```js
// assuming process.env.NODE_ENV is actually "development"
process.env.NODE_ENV;
```

### Out

```js
"development";
```

## Installation

```sh
npm install @tysonmatanich/babel-plugin-transform-inline-environment-variables --save-dev
```

## Usage

### JavaScript (Recommended)

```javascript
const babel = require("@babel/core");
const inlineEnvVarPlugin = require("@tysonmatanich/babel-plugin-transform-inline-environment-variables");

const transformed = await babel.transformFileAsync("{path-to-file}.js", {
  configFile: false,
  plugins: [
    babel.createConfigItem([
      inlineEnvVarPlugin,
      { include: [], exclude: [] },
    ]),
  ],
  retainLines: true,
});

console.log(transformed.metadata.keysReplaced);
```

### Via `.babelrc`

**.babelrc**

```json
// without options
{
  "plugins": ["transform-inline-environment-variables"]
}

// with options
{
  "plugins": [
    ["transform-inline-environment-variables", {
      "include": [
        "NODE_ENV"
      ]
    }]
  ]
}
```

### Via CLI

```sh
babel --plugins transform-inline-environment-variables script.js
```

### Via Node API

```javascript
require("@babel/core").transform("code", {
  plugins: ["transform-inline-environment-variables"]
});
```

## Options

+ `include` - array of environment variables to include
+ `exclude` - array of environment variables to exclude
