# Support Async Tests with JavaScripts Promises through async await

Our testing framework works great for our synchronous test. What if we had some asynchronous functions that we wanted to test? We could make our callback functions `async`, and then use the `await` keyword to wait for that to resolve, then we can make our assertion on the `result` and the `expected`.

Let’s make our testing framework support promises so users can use async/await.

```js
提取码：36e3
```

[观看视频](https://pan.baidu.com/s/13TcETbD81dJEpnZWHTCZ2g)

[Code](https://codesandbox.io/s/ym5y960j1)

## Transcript

Our testing framework works great for our synchronous test. What if we had some asynchronous functions that we wanted to test? We could make our callback functions `async`, and then use the `await` keyword to wait for that to resolve, then we can make our assertion on the `result` and the `expected`.

async-await.js

```jsx
test('sumAsync adds numbers asynchronously', async () => {
  const result = await sumAsync(3, 7)
  const expected = 10
  expect(result).toBe(expected)
})

test('subtractAsync subtracts numbers asynchronously', async () => {
  const result = await subtractAsync(7, 3)
  const expected = 4
  expect(result).toBe(expected)
})
```

This approach has a little bit of a problem though. If we run our test, we are going to see that they both pass, and then after that, we have an `UnhandledPromiseRejectionWarning`. That is the actual error coming from our `sumAsync` function being broken.

![](http://res.cloudinary.com/dg3gyk0gu/image/upload/v1543907670/transcript-images/javascript-support-async-tests-with-javascripts-promises-unhandled.png)

Because this is an async function, this function will return a promise. When this error is thrown, it's going to reject that promise. Here inside of our `test` function, this `callback` is going to return a promise. If we turn this `test` into an `async` function, and then `await` that `callback`, if that promise is rejected, then we'll land in our catch block.

If no error is thrown, then we'll continue on inside the try block. This will work for both our synchronous and our asynchronous tests.

```jsx
async function test(title, callback) {
  try {
    await callback()
    console.log(`✓ ${title}`)
  } catch (error) {
    console.error(`✕ ${title}`)
    console.error(error)
  }
}
```

With that, we can run our test again, and things happen exactly as we expect.

![](http://res.cloudinary.com/dg3gyk0gu/image/upload/v1543907672/transcript-images/javascript-support-async-tests-with-javascripts-promises.png)