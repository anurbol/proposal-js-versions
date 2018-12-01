# Proposal to introduce versions to Javascript (ECMAScript)

This [proposal](https://github.com/tc39/proposal-global) led me to the idea of versioning Javascript. The mentioned proposal suggested some ridiculous and wide-discussed thing such as **globalThis**. You can read about it on the proposal's repo, but the reason why it was introduced is backwards-compatibility. And what is the solution to a swelling backward-compatibility problem? It's versioning.

## Examples

With versioning ugly things like **globalThis** can be avoided in favor of desired-by-everyone **global**:

```js
use 10 // turn on features of 10th version of JS

console.log(global) // exists in browsers too
```
So cool, progressive kids would enjoy new features and old programs would still work fine.

Also, old weirdness like this can be eliminated:

```js
typeof null // 'null', not 'object'!
```

Or some deprecated stuff can be disallowed:
```js
var foo // error "`var` is deprecated, use `let` or `const`"
```

## A note on environment checking

This may be considered as an off-topic, and should be in a separate proposal. However, left it here for demonstration purposes.

A big showstopper for introducing `global` to browsers was the fact that folks 
check the environment like this:

```js
if (global) {
   // run code for node.js
} else {
   // run code for browsers
}

```

Obviously the above code looks hackish and does not show the intention of the developer.

With the proposed feature it should be and can be something like this:

```js
if (global.environment === 'node') {
    // run code for node.js
} else if (global.environment === 'browser') {
    // run code for browsers
} else { /* other platforms */}
```

## Previous art

There is already the strict mode that is used extensively, so versioning is not something impossible:

```
use strict
```

