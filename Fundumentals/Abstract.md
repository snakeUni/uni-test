# Abstract Test Assertions into a JavaScript Assertion Library

Let’s add a simple layer of abstraction in our simple test to make writing tests easier. The assertion library will help our test assertions read more like a phrase you might say which will help people understand our intentions better. It will also help us avoid unnecessary duplication.

```js
提取码：n8ma
```

[观看视频](https://pan.baidu.com/s/1ib-SAwylegNKvq8n1PBxRw)

[Code](https://codesandbox.io/s/k39kq1w96v)

## Transcript

We're pulling `sum` and `subtract` from this math module, and `sum` has a bug.

assertion-library.js

```jsx
const {sum, subtract} = require('../math')
```

We can reveal that bug with a simple test.

```jsx
result = sum(3, 7)
expected = 10
if (result !== expected) {
  throw new Error(`${result} is not equal to ${expected}`)
}
```

When we run this file with node, that assertion is throwing an error.

![](http://res.cloudinary.com/dg3gyk0gu/image/upload/v1543907669/transcript-images/node-js-build-a-javascript-assertion-library-sum-error.png)

Also, this code is pretty imperative. It'd be nice to write a little abstraction to make it read a little nicer. Let's go ahead and write a simple abstraction to encapsulate this assertion. I'll create a function down here called expect. That's going to accept an `actual`.

```jsx
function expect(actual){

}
```

We are going to return an object that has some assertions on it. Our first one here is going to be `toBe`, and that's going to take an `expected` value.

```jsx
function expect(actual) {
  return {
    toBe(expected) {
    }
  }
}
```

We're going to say if the `actual` is not equal to the `expected` value, then we'll `throw a new Error` that says, "Actual is not equal to expected."

```jsx
function expect(actual) {
  return {
    toBe(expected) {
      if (actual !== expected) {
        throw new Error(`${actual} is not equal to ${expected}`)
      }
    }
  }
}
```

We can take this duplicated code, remove that and replace it with:

```jsx
result = sum(3, 7)
expected = 10
expect(result).toBe(expected)
```

If we run that now, we are going to get the same error message. This function is like an assertion library. Fundamentally, it takes an actual value, and then it returns an object that has functions for different assertions that we can make on that actual value.

Here, we have `toBe`. We could also have a `twoEqual`, now it'd take an `expected` value, and maybe do a deep equality check.

We could also have a `toBeGreaterThan` or `toBeLessThan`, and then it could take an `expected` value. There're all kinds of assertions that we could add to our little assertion library here to make writing our test a little easier.