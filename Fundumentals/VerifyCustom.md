# Verify Custom JavaScript Tests with Jest

Up to this point we’ve created all our own utilities. As it turns out, the utilities we’ve created mirror the utilities provided by Jest perfectly! Let’s install Jest and use it to run our test!

```js
提取码：mdij
```

[观看视频](https://pan.baidu.com/s/1Ip09Apdha99Ce5f_VO9mCQ)

[Code](https://codesandbox.io/s/oj2n255o76)

## Transcript

The testing framework we've written actually looks remarkably a lot like Jest. Rather than running `node --require`, and then instead of globals and so on and so forth, we could actually just use Jest directly.

If I run `npx jest`,

Terminal

```js
npx jest
```

jest will automatically pick up our `jest.test.js` file based off of that convention.

jest.test.js

```js
const {sumAsync, subtractAsync} = require('../math')

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

It will show us really helpful error messages, and even a code frame to show us exactly where in our code that error was thrown.

![](http://res.cloudinary.com/dg3gyk0gu/image/upload/v1543907670/transcript-images/javascript-verify-custom-javascript-tests-with-jest.png)

These are some of the things that make jest such an awesome testing framework because the error messages are so clear.