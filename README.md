# Proposal: Modes

Champions:

* @JakobJingleheimer

Authors:

* @JakobJingleheimer

## [Stage](https://tc39.github.io/process-document/)

**Current**: 0

## The Problem

Code that needs to be conditionally executed in different contexts. This is currently hacked together with `process.env.NODE_ENV` (which doesn't exist outside of node et al); in a browser environment, that can't be used to affect the runtime's behaviour.

With a native flag, that could open the door for:

* Conditional code execution
  * Comparisons
  * Connecting to different external resources
  * Logging
* Special access that cannot be granted in a production context (Proxy, Constituents of expressions, Constituents of structure, Internal slots)

This could be broadly useful, in particular for the [Comparisons](https://github.com/JakobJingleheimer/proposal-comparisons) and [Inspector](https://github.com/tc39/proposal-inspector) proposals.

```js
PRODUCTION: if (!compare(a, b)) throw new Error('…');

NONPRODUCTION: inspect(b, { detectProxy: true });
```

The runtime would ensure "non-production" code cannot be executed in a production environment (such as limiting to `localhost`).
