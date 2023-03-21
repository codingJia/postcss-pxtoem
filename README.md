# 参照pxtorem将单位修改为em

## Install

```shell
$ npm install postcss-px2em --save-dev
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
    rootValue: 16,
    unitPrecision: 5,
    propList: ['font', 'font-size', 'line-height', 'letter-spacing'],
    selectorBlackList: [],
    replace: true,
    mediaQuery: false,
    minPixelValue: 0,
    exclude: /node_modules/i
}
```

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
