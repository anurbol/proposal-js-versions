# Proposal to introduce versions to Javascript (ECMAScript)

This [proposal](https://github.com/tc39/proposal-global) led me to the idea of versioning Javascript. The mentioned proposal suggested some arguably ridiculous and wide-discussed thing such as **globalThis**. You can read about it on the proposal's repo, but the reason why it was introduced is backwards-compatibility. And what is the solution to the swelling backward-compatibility problem? That would be versioning.

## Examples

With versioning weird things like **globalThis** can be avoided in favor of desired-by most of the people **global**:

```js
'use 10' // turn on the features of 10th version of JS

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

## Arguments against

There is an article on the web: http://exploringjs.com/es6/ch_one-javascript.html. While Axel Rauschmayer (the biggest authority not only for me) claims the reasons listed there are relevant and important, 
non of them seemed convincing enough for me. 

> Engines become bloated, because they need to implement the semantics of all versions

New versions don't necessarily implement heavy features. In the examples above, there is no single heavy feature to be implemented. Exposing `global` variable in new versions, instead of `globalThis` for all is not a heavy feature. Fixing `typeof null` and removing `var` is not something complex either.

> Programmers need to remember how the versions differ.

Programmers already need to remember how `strict mode` differs from sloppy mode. They also don't need to learn new versions, if they don't want. Likely, they don't need to learn new features, if they don't want. In the end, new versions are supposed to make life easier for programmers, not for some other people. 

> Code becomes harder to refactor, because you need to take versions into consideration when you move pieces of code.

This is already the case with `strict mode`. In general, yes, this is a problem, but is it really big enough to bear with things like `globalThis` (and other such things yet to come because of compromises)? Also, the whole programming is about trade-offs. You almost never can get something good without sacrificing some other thing.


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

There is already the strict mode that is used extensively:

```
'use strict'
```

therefore versioning of course is not something impossible.
