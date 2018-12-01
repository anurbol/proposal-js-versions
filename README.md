# Proposal to introduce versions to Javascript (ECMAScript)

This [proposal](https://github.com/tc39/proposal-global) led me to the idea of versioning Javascript. The mentioned proposal suggested some ridiculous and wide-discussed thing such as **globalThis**. You can read about it on the proposal's repo, but the reason why it was introduced is backwards-compatibility. And what is the solution to a swelling backward-compatibility problem? It's versioning.

## Examples

With versioning ugly things like **globalThis** can be avoided in favor of desired-by-everyone **global**:

```
use 10 // turn on features of 10th version of JS

console.log(global.environment) // 'node', 'browser', etc.
```
So cool, progressive kids would enjoy new features and old programs would still work fine.

Also, old weirdness like this can be eliminated:

```
typeof null // 'null', not 'object'!

var foo // error "`var` is deprecated, use `let` or `const`"
```

## Previous art

There is already the strict mode that is used extensively, so versioning is not something impossible:

```
use strict
```

