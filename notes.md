# Notes

## Don't use `esModuleInterop`

If you enable esModuleInterop then consumers of your code will need to do the same.

CJS and ESM imports are mostly interoperable. The problem cases are:

### Namespace imports

Use a namespace import rather than destructuring the default import

_legacy.js_

```
function product(a, b) {
  return a * b;
}

module.exports = { product };
```

_main.ts_

```
import * as legacy from './legacy';
legacy.product(3, 4);
```

### Top-level callable imports

Use require in the import statement rather than using default.

_legacy.js_

```
function product(a, b) {
  return a * b;
}

module.exports = product;
```

_main.ts_

```
import product = require('./legacy');
product(3, 4);
```

### CJS exports in TS

In TS assign to `export` rather than `module.exports`

_legacy.ts_

```
function product(a: number, b: number): number {
  return a * b;
}

export = product;
```
