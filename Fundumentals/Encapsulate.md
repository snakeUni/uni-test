# Encapsulate and Isolate Tests by building a JavaScript Testing Framework

One of the limitations of the way that this test is written is that as soon as one of these assertions experiences an error, the other tests are not run. It can really help developers identify what the problem is if they can see the results of all of the tests.

Let’s create our own `test` function to allow us to encapsulate our automated tests, isolate them from other tests in the file, and ensure we run all the tests in the file with more helpful error messages.

```jsx
提取码：ecx4
```

[观看视频](https://pan.baidu.com/s/1nd28C4pRrK-XtkE-I48ixA)

[Code](https://codesandbox.io/s/7j4p6vqyoj)

## Transcript

One of the limitations of the way that this test is written is that as soon as one of these assertions experiences an error, the other tests are not run. It can really help developers identify what the problem is if they can see the results of all of the tests.

In addition to that, because we are throwing our error here, if we look at the stack trace after running our testing file, we see that the error was thrown on line 17 really directly. We know exactly where that's happening.

![](http://res.cloudinary.com/dg3gyk0gu/image/upload/v1543907669/transcript-images/javascript-build-a-javascript-testing-framework-stack-error.png)

We have to dig through the stack trace a little bit further to see which one of these is throwing the error. It's not readily apparent whether this `-4 is not equal to 10` is happening because the sum is broken or because the `subtract` is broken.

A testing framework's job is to help developers identify what's broken as quickly as possible. It can do that by making more helpful error messages and by running all of the tests. Let's go ahead and make that.

I am going to start with a function called the `test`. It's going to accept a `title` and a `callback`.

testing-framework.js

```jsx
function test(title, callback) {
  
}
```

Because this `test` could throw an error, I am going to wrap that in a try-catch. I'll call the `callback`. If that `callback` throws an error, then I'll `log` that error.

```jsx
function test(title, callback) {
  try {
    callback()
  } catch (error) {
    console.error(error)
  }
}
```

I'll also want to `console.error` the `title`. If it doesn't throw an error, then we'll get to this line where I can `console.log` the `title`. Let's add a little `✓` and an `✕` to make it more apparent what happened.

```jsx
function test(title, callback) {
  try {
    callback()
    console.log(`✓ ${title}`)
  } catch (error) {
    console.error(`✕ ${title}`)
    console.error(error)
  }
}
```

Next, let's make a function called `sumTest`. We'll move this code into `sumTest`.

```jsx
function sumTest(){
    result = sum(3, 7)
    expected = 10
    expect(result).toBe(expected)
}
```

We'll use our `test` utility, and we'll title this `sum adds numbers` and pass our `sumTest`.

```jsx
test('sum adds numbers', sumTest)
```

We'll do the same thing for our `subtractTest` and move that code up into our subtractTest, then we'll add a `test(subtract subtracts numbers)`.

We'll pass our `subtractTest`.

```jsx
function subtractTest(){
    result = subtract(7,3)
    expected = 4
    expect(result).toBe(expected)
}
test('subtract subtracts numbers', subtractTest)
```

Now, we'll run our test file again. Here, we'll see we had an error with `sum adds numbers` and the passing test with `subtract subtracts numbers`. We know that the problem isn't with `subtract`. It's with `sum`. It's readily apparent.

![](http://res.cloudinary.com/dg3gyk0gu/image/upload/v1543907671/transcript-images/javascript-build-a-javascript-testing-framework-sum-fails.png)

Let's refractor things a little bit to encapsulate our `test` better. I'll make this `const` and then we can get rid of this let declaration. I am actually going to turn this into an arrow function. We'll move this code into that arrow function. I'll do the same thing for `subtractTest`.

```jsx
test('sum adds numbers', () => {
  const result = sum(3, 7)
  const expected = 10
  expect(result).toBe(expected)
})

test('subtract subtracts numbers', () => {
  const result = subtract(7, 3)
  const expected = 4
  expect(result).toBe(expected)
})
```

In review, our test utility's job is to make it easier for people to quickly identify what's broken so they can fix it quickly. We do that by having a more helpful error message and by running all of the tests in our file.