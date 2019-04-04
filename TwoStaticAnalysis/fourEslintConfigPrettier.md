# Disable Unnecessary ESLint Stylistic Rules with eslint-config-prettier

Because prettier can automatically fix a lot of stylistic issues in our codebase, it’s not necessary to have eslint check for those and it can actually be kind of annoying if it does. So let’s see how we can use `eslint-config-prettier` to disable all rules that are made irrelevant thanks to prettier.

```js
提取码: fbeh
```

[观看视频](https://pan.baidu.com/s/1aMBadbUoRkiOIdciRzIENA)

[Code](https://github.com/kentcdodds/static-testing-tools/tree/step-5)

## Transcript

As you go about configuring ESLint and extending other configurations, you might end up extending a configuration that conflicts with Prettier. In that case, you'll want to specifically configure a certain rule.

`"semi": ["error", "never"]` No semicolons in this project, for example. Even in this case, this can be pretty annoying.

.eslintrc

```jsx
  "rules": {
    "semi": ["error", "never"],
    "no-console": "off"
  },
```

If I go to my project now and add a semicolon after 'hello', I'm going to see a little red underline saying there's an extra semicolon. I'll want to remove that.

The red goes away, but that's annoying. We have our Prettier integration with my editor. If I hit `cmd+s` to save, then that semicolon will go away automatically for me, thanks to Prettier.

That in itself is annoying. I don't want to even see the red underline. What I really want is to have this rule just be completely disabled. I'll say, `off` Now I have that semicolon. It's not a big deal for me because I can hit `cmd+s` and it'll go away anyway.

```jsx
 "rules": {
    "semi": "off",
    "no-console": "off"
  },
```

This applies to any of the rules that you have. If you want to make sure that you always have the parentheses around or you want to make sure those parentheses are gone for these arrow functions, you don't want to see a red underline for something that Prettier is going to remove for you anyway.

There's a configuration that we can extend that will automatically disable all the rules that Prettier renders irrelevant. We're going to `npm install` as a dev dependency, `--save-dev eslint-config-prettier`.

Terminal Input

```jsx
npm install --save-dev eslint-config-prettier
```

While that's installing, I'll go to my `.eslintrc` here. At the very end, I'll add `eslint-config-prettier`. The configurations that come at the end will win in a conflict for rules for all the configurations that come before it.

.eslintrc

```jsx
{
  "parserOptions": {
    "ecmaVersion": "2018"
  },
  "extends": [
    "eslint:recommended", "eslint-config-prettier"
  ],
  "rules": {
    "semi": "off",
    "no-console": "off"
  },
  "env": {
      "browser": true
  }
}
```

Then the rules that I specify myself here will win in a conflict with any of the rules specified by these configurations. I can get rid of this `"semi": "off"`, because `eslint-config-prettier` is going to disable that for me.

```jsx
"rules": {
    "no-console": "off"
  },
```

I'll save this configuration. I look in `example.js`. I can add this semi-colon after 'hello'. I can add parentheses around my arrow functions. No configurations are going to get mad at me for things that Prettier is going to fix for me anyway.

example.js

```jsx
const greeting = 'hello';
console.log(`${greeting} world!`)
;[(1, 2, 3)].forEach((x) => console.log(x))
```

In review, all that we needed to do for this was add as a dev dependency `eslint-config-prettier` and then extend `eslint-config-prettier` in our ESLint configuration.
