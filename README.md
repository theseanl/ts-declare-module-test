# Demonstration of [tsickle#1039](https://github.com/angular/tsickle/issues/1039)

## How to reproduce

First, execute
```
tsickle --extern=externs.js
```
from the project root, then it will generate `uses_my_module.js` and `externs.js` files.

Next, `cd` into `node_modules/my_module`, then execute
```
tsickle --extern=externs.js
```
Then it will generate `node_modules/my_module/uses_my_module.js` and `node_modules/my_module/externs.js` files.

Then check how `node_modules/my_module/externs.js` is fine but `externs.js` is problematic, in particular, it generated externs for `node_modules/my_module/augments.d.ts` on a different namespace.

This is weird, because [Typescript spec on ambient modules](https://github.com/Microsoft/TypeScript/blob/master/doc/spec.md#12.2) prevents usage of relative paths in `declare module "..."` but it works nevertheless, and is used by a popular library.

