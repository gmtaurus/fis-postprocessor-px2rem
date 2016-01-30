# fis-postprocessor-px2rem

According to one stylesheet, generate rem version and @1x, @2x and @3x stylesheet.

## Usage

The raw stylesheet only contains @2x style, and if you

* don't intend to transform the original value, eg: 1px border, add `/*no*/` after the declaration
* intend to use px by force，eg: font-size, add `/*px*/` after the declaration

**Attention: Dealing with SASS or LESS, only `/*...*/` comment can be used, in order to have the comments persisted**

## Install
* install fis-postprocessor-autoprefixer  
    `npm install -g fis-postprocessor-px2rem`
* modify fis-conf.js  
    ```
    fis.match('*css', {
        postprocessor: fis.plugin('px2rem')
    });
    ```

### Options

    ```
    {
        baseDpr: 2,             // base device pixel ratio (default: 2)
        threeVersion: false,    // whether to generate @1x, @2x and @3x version (default: false)
        remVersion: true,       // whether to generate rem version (default: true)
        remUnit: 75,            // rem unit value (default: 75)
        remPrecision: 6         // rem precision (default: 6)
    }
    ```

### Example

#### Pre processing:

One raw stylesheet: `test.css`

```
.selector {
    width: 150px;
    height: 64px; /*px*/
    font-size: 28px; /*px*/
    border: 1px solid #ddd; /*no*/
}
```

#### After processing:

Rem version: `test.css`

```
.selector {
    width: 2rem;
    border: 1px solid #ddd;
}
[data-dpr="1"] .selector {
    height: 32px;
    font-size: 14px;
}
[data-dpr="2"] .selector {
    height: 64px;
    font-size: 28px;
}
[data-dpr="3"] .selector {
    height: 96px;
    font-size: 42px;
}
```

@1x version: `test1x.css`

```
.selector {
    width: 75px;
    height: 32px;
    font-size: 14px;
    border: 1px solid #ddd;
}
```

@2x version: `test2x.css`

```
.selector {
    width: 150px;
    height: 64px;
    font-size: 28px;
    border: 1px solid #ddd;
}
```

@3x version: `test3x.css`

```
.selector {
    width: 225px;
    height: 96px;
    font-size: 42px;
    border: 1px solid #ddd;
}
```

