# Throw an Error with a Simple Test in JavaScript

In this lesson, we’ll get the most fundamental understanding of what an automated test is in JavaScript. A test is code that throws an error when the actual result of something does not match the expected output.

Tests can get more complicated when you’re dealing with code that depends on some state to be set up first (like a component needs to be rendered to the document before you can fire browser events, or there needs to be users in the database). However, it is relatively easy to test pure functions (functions which will always return the same output for a given input and not change the state of the world around them).

[Code](https://codesandbox.io/s/0y3z2pxw1p)

## Transcript

We have a bug in the sum function. It's doing subtraction instead of addition. We could easily fix this, but let's go ahead and write an automated test that can make sure that this bug never surfaces again.

An automated test in JavaScript is code that throws an error when things are unexpected. Let's do that. Let's get our `result` from the `sum` of three and seven.

simple.js

```jsx
const result = sum(3, 7)
```

We will say our `expected` is 10. We can say if the `result` is not equal to the `expected` value, then we can throw a new error that says, "Result is not equal to expected."

```jsx
const expected = 10
if (result !== expected){
    throw new Error(`${result} is not equal to ${expected}`)
}
```

To run this, we can run `node lessons/simple.js`.

We will get our error, "-4 is not equal to 10."

![](http://res.cloudinary.com/dg3gyk0gu/image/upload/v1543907671/transcript-images/javascript-write-the-simplest-test-in-javascript-error.png)

If we replace this with addition and run that again, our script passes without throwing errors. This is the most fundamental form of a test.

```jsx
const sum = (a, b) => a + b
```

Let's go ahead and add another test for `subtract`. I am going to change this from `const` to `let`.

```jsx
const subtract = (a, b) => a - b
```

We will say, `result` is now equal to subtract of seven and three, and our `expected` is now equal to four."

```jsx
result = subtract(7, 3)
expected = 4
```

We will just copy and paste this here.

```jsx
if (result !== expected){
    throw new Error(`${result} is not equal to ${expected}`)
}
```

Save that and run our script again. It passes without error. In review, this is the most fundamental form of a test in JavaScript. It's simply a code that will throw an error when the result is not what we expect.

Let's go ahead and break this again. We'll run that script again. We're getting an error message. The Javascript testing framework is to make that error message as useful as possible so we can quickly identify what the problem is and fix it.