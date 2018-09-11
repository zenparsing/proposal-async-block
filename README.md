# Async blocks for JavaScript

Eliminating IIAAFE from modules and scripts, so you don't have to.

## The Idea

We've all seen the IIAAFE pattern out in the wild:

```js
(async () => {
  // Use await in here
})();
```

And it's slightly more cordial cousin, the IIAMFD:

```js
async function main() {
  // Use await in here
}

main();
```

We see these patterns in the following scenarios:

- Documentation and education materials, where we want to demonstrate `await` usage but need to create an `async` context first.
- Program "main" files, where we want to run some startup code with `await` in it.

Async blocks are a simple syntactic feature that allows us to avoid abstruse patterns in order to convey simple ideas.

Also, it doesn't mess with the entire module system. It's like, orthogonal and stuff.

## Example

```js
async {
  let result = await fetch(someURL);
  let data = await result.json();
  console.log('fetched!');
}
```

*Works in scripts and modules, too!*

## The Details

Here's the grammar:

```
Statement:
  ...
  AsyncBlockStatement

AsyncBlockStatement :
  `async` [no LineTerminator here] `{` AsyncFunctionBody `}`
```

The body of an async block has the exact same semantics as an arrow function body.
