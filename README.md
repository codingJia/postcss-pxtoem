## Install

```shell
$ npm install postcss-plugin-pxtoem --save-dev
```

### Input/Output

*With the default settings, only font related properties are targeted.*

```css
// input
h1 {
    margin: 0 0 20px;
    font-size: 32px;
    line-height: 1.2;
    letter-spacing: 1px;
}

// output
h1 {
    margin: 0 0 20px;
    font-size: 2em;
    line-height: 1.2;
    letter-spacing: 0.0625em;
}
```

### options

Type: `Object | Null`  
Default:
```js
{
    rootValue: 100,
    unitPrecision: 5,
    propList: ['font', 'font-size', 'line-height', 'letter-spacing'],
    selectorBlackList: [],
    replace: true,
    mediaQuery: false,
    minPixelValue: 0,
    exclude: /node_modules/i
}
```
- `rootValue` (Number|Object) The root element font size. Default is 100.
    - If rootValue is an object, for example `{ px: 50, rpx: 100 }`, it will
    replace rpx to 1/100 em , and px to 1/50 em.
- `unitPrecision` (Number) The decimal numbers to allow the em units to grow to.
- `propWhiteList` (Array) The properties that can change from px to em.
    - Default is an empty array that means disable the white list and enable all properties.
    - Values need to be exact matches.
- `propBlackList` (Array) The properties that should not change from px to em.
    - Values need to be exact matches.
- `exclude` (Reg)  a way to exclude some folder,eg. /(node_module)/.
- `selectorBlackList` (Array) The selectors to ignore and leave as px.
    - If value is string, it checks to see if selector contains the string.
        - `['body']` will match `.body-class`
    - If value is regexp, it checks to see if the selector matches the regexp.
        - `[/^body$/]` will match `body` but not `.body`
- `ignoreIdentifier` (Boolean/String)  a way to have a single property ignored, when ignoreIdentifier enabled, then `replace` would be set to `true` automatically.
- `replace` (Boolean) replaces rules containing ems instead of adding fallbacks.
- `mediaQuery` (Boolean) Allow px to be converted in media queries.
- `minPixelValue` (Number) Set the minimum pixel value to replace.

### A message about ignoring properties
Currently, the easiest way to have a single property ignored is to use a capital in the pixel unit declaration.

```css
// `px` is converted to `em`
.convert {
    font-size: 16px; // converted to 1em
}

// `Px` or `PX` is ignored by `postcss-pxtoem` but still accepted by browsers
.ignore {
    border: 1Px solid; // ignored
    border-width: 2PX; // ignored
}
```
