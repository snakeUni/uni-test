# Lint JavaScript by configuring and running ESLint

The static code analysis and linting tool [ESLint](https://eslint.org/) is the de-facto standard for linting JavaScript projects. In this lesson we’ll see how to install, run, and configure it for your preferences.

[Code](https://github.com/kentcdodds/static-testing-tools/tree/step-2)

## Transcript

Here I have a simple project with a couple of bugs in this example. I'm using `typeof` improperly. I've got a very subtle bug right here. I'm messing up this string interpolation, not using a template literal string.

example.js

```js
const name = 'Freddy'
typeof name === 'string'

if (!'serviceWorker' in navigator) {
  // you have an old browser :-(
}

const greeting = 'hello'
console.log('${greeting} world!')

[(1, 2, 3)].forEach(x => console.log(x))
```

I'm going to use eslit to make sure that I avoid these problems. I'm going to go ahead and `npm install --save-dev eslint`.

Terminal Input

```js
npm install --save-dev eslint
```

With that installed, if I check out my `package.json`, I'll see that that's in my `devDependencies`. I can configure eslint. There are various ways to do this. I'm going to use `.eslintrc`. This is a JSON file where I can configure eslint.

The first thing I need to configure is the version of JavaScript that I want it to be checking. I'm going to say `parserOptions`, and my ecmaVersion is 2018, `"ecmaVersion": "2018"`. I'm writing the latest version of JavaScript. Then I can specify some `rules`.

.eslintrc

```js
{
  "parserOptions": {
    "ecmaVersion": "2018"
  },
  "rules": {

  }
}
```

One rule that I'm particularly interested in right now is the `typeof`, to make sure that I don't have a typo when I'm checking the `typeof` something. Let's go ahead and add `"valid-typeof": "error"`. That's one of the built-in rules in eslint.

```js
{
  "parserOptions": {
    "ecmaVersion": "2018"
  },
  "rules": {
    "valid-typeof": "error"
  }
}
```

Now with that set, I can run `npx eslint` on my source directory, `src`, and I'll get an error for that particular rule. This error is actually going to fail my build if I were to put this eslint script into my build.

Terminal Input

```js
npx eslint src
```

If I didn't want this particular rule to fail my build, then instead of error, I could say `warn`.

.eslintrc

```js
{
  "parserOptions": {
    "ecmaVersion": "2018"
  },
  "rules": {
    "valid-typeof": "warn"
  }
}
```

Then if I run eslint again, I'm going to get a warning for that same rule failure. This will not fail my build, but it will let me know that there is a problem there. I can also disable this rule entirely by adding off. Now if I run eslint, it's not going to give me any output.

```js
{
  "parserOptions": {
    "ecmaVersion": "2018"
  },
  "rules": {
    "valid-typeof": "off"
  }
}
```

Another option that I have here is I can extend, add an `extends` property here. There are a lot of different configurations that I can install. There's a built-in configuration called `eslint:recommended`. With that, I can run `npx eslint src` and I get a whole bunch of errors here in the Terminal.

```js
{
  "parserOptions": {
    "ecmaVersion": "2018"
  },
  "extends": [
    "eslint:recommended"
  ],
  "rules": {
    "valid-typeof": "error"
  }
}

```

Then I can go into my `example.js`. I can fix each one of these to avoid the problems these eslint rules were written for. To save us some time, I'm going to go ahead and just paste in the fixed code. With that code fixed, now I can run `npx eslint src`. I'm getting a couple other errors that I'm going to configure eslint to avoid.

![](http://res.cloudinary.com/dg3gyk0gu/image/upload/v1543908125/transcript-images/eslint-install-run-and-configure-eslint-example-js-eslint-errors.png)

Next, we're going to go to our `.eslintrc` file and we're going to set the environment, `"env"`, for our code as `"browser": true`. Now if I run this again, I'm going to just see unexpected console statement. If I want to keep those there, then I can say `"no-console": "off"`. I'm going to remove `valid-typeof` because we're going to get a good configuration from the eslint recommended configuration.

.eslintrc

```js
{
  "parserOptions": {
    "ecmaVersion": "2018"
  },
  "extends": [
    "eslint:recommended"
  ],
  "rules": {
    "no-console": "off"
  },
  "env": {
      "browser": true
  }
}
```

With that, I can now run `npx eslint src` and everything is working.

Terminal Input

```js
npx eslint src
```

Let's go ahead and add this to our script so we don't have to run `npx` every time. We'll go to `package.json` to our `scripts`. We'll add a `"lint: "eslint src"`.

package.json

```js
"scripts": {
    "lint": "eslint src"
},
```

Now we can run `npm run lint`.

Terminal Input  

```js
npm run lint
```

In review, all we had to do here was install `eslint` as a dev dependency. We also added a `script` in our `package.json` for linting the `src` directory. Then we configured eslint in our `.eslintrc`, first specifying the version of JavaScript that we're going to be writing.

We also specified some custom rules, the environment that our JavaScript is going to be running in so it would know what global variables are available, and a configuration that we want to extend.

I'm going to do one more thing, and that is with most modern editors there is an eslint plugin that you can use. I'm going to go search for `eslint` in the extensions for VS Code here. I already have it installed. I'll just enable it.

Then I'll reload my editor. Now if I go to that` example.js` file and I make some sort of error, like change this to a regular string, I'm going to see an error here without having to run the `eslint` script in the terminal. This helps me have a much faster feedback loop as I'm editing the code.

![](http://res.cloudinary.com/dg3gyk0gu/image/upload/v1543908124/transcript-images/eslint-install-run-and-configure-eslint-example-js.png)