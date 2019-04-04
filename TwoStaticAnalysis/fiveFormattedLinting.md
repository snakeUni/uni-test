# Validate all files are formatted when linting

You can’t force everyone on your project to use the prettier integration for their editor, so let’s add a validation script to verify that prettier has been run on all project files.

Fortunately for us, Prettier accepts a `--list-different` flag that you can use that will throw an error when code is not up to the standard of your project.

```js
提取码：gpbq
```

[观看视频](https://pan.baidu.com/s/1qpmiEHCfLLK6l_0tLFbG4w)

[Code](https://github.com/kentcdodds/static-testing-tools/tree/step-6)

## Transcript

In a project with multiple people on the team, you're going to have some people who have the editor integration going on with their project and everything looks great, and you'll have some people who don't. Let's see what we can do about making sure that people run the format script.

I'm going to open my default user settings. I'll disable this format on save. Now I can make some changes. Hit the save key. It doesn't format automatically.

example.js

```jsx
const name = 'Freddy'
typeof name === 'string'

if (!('serviceWorker' in navigator)) {
        // you have an old browser :-(
}

const greeting = 'hello'
console.log('${greeting} world!')
;[(1, 2, 3)].forEach(x => console.log(x))
```

This is what it would look like, potentially, if somebody who doesn't use Prettier in their editor went ahead and tried to save some code. Because ESLint isn't checking this kind of formatting for us, we want to have some sort of automated validation to make sure that things have been formatted properly.

One thing that we can do is if I run Prettier with npx and run it on source example, `npx prettier src/example.js`, then I can add the flag `--list-different`. It's going to list for me all the files that would be changed by Prettier.

Terminal Input

```jsx
npx prettier src/example.js --list-different
```

I'll go ahead and `--write` this. Then I'll run Prettier with `npx prettier` `src/example` again. I don't see any files listed.

Terminal Input

```jsx
npx prettier src/example.js --write
npx prettier src/example.js --list-different
```

This script will exit with a non-zero exit code, meaning the script will fail if any of these files are listed. We can make it part of a validation script. I'm going to make a new script in `package.json`, called `validate`. We'll `npm run lint`. Then we'll run our Prettier script here. We'll copy this. Instead of `--write`, we'll run `--list-different`.

package.json

```jsx
"scripts": {
    "lint": "eslint src",
    "format": "prettier --write \"**/*.+(js|jsx|json|yml|yaml|css|less|scss|ts|tsx|md|graphql|mdx)\"",
    "validate": "npm run lint && prettier --list-different \"**/*.+(js|jsx|json|yml|yaml|css|less|scss|ts|tsx|md|graphql|mdx)\"",
},
```

With that now, let's go ahead. I'll make a big mess of this. We'll throw a couple things all over the place.

example.js
![](http://res.cloudinary.com/dg3gyk0gu/image/upload/v1543908125/transcript-images/egghead-validate-all-files-are-formatted-when-linting-messy-example-js.png)

Now if I run `npm run validate`, I'll see my ESLint runs.

Terminal Input

```jsx
npm run validate
```

Everything passes ESLint, but Prettier is saying, "Hey, there's a file here that should have been formatted but wasn't." Then I can run `npm run format`. Then I'll run the `validate` script again. Everything passes fine.

Terminal Input

```jsx
npm run format
npm run validate
```

This is a little bit uncomfortable for me. We've got a huge string of text in `package.json` that we're repeating in both of these scripts. If we wanted to add a new file, we'd need to make sure to add it to both of them.

What I'm going to do is just a quick little clean-up. We'll add a `prettier` script. The `prettier` script will be responsible for this part. The flags will be handled by the individual scripts.

package.json

```jsx
"scripts": {
    "lint": "eslint src",
    "format": "prettier --write \"**/*.+(js|jsx|json|yml|yaml|css|less|scss|ts|tsx|md|graphql|mdx)\"",
    "prettier": "prettier \"**/*.+(js|jsx|json|yml|yaml|css|less|scss|ts|tsx|md|graphql|mdx)\"",
    "validate": "npm run lint && prettier --list-different \"**/*.+(js|jsx|json|yml|yaml|css|less|scss|ts|tsx|md|graphql|mdx)\""
},
```

Here, for our format, we'll run `npm run prettier`. Then we'll forward along the write flag, `-- --write`. For our `validate` script, we're going to run `npm run prettier`. We'll forward along the `--list-different` flag. We'll get rid of that. Now things look a little bit cleaner.

```jsx
"scripts": {
    "lint": "eslint src",
    "format": "npm run prettier -- --write",
    "prettier": "prettier \"**/*.+(js|jsx|json|yml|yaml|css|less|scss|ts|tsx|md|graphql|mdx)\"",
    "validate": "npm run lint && npm run prettier -- --list-different"
},
```

In review, to validate that all the files in the project have been formatted by Prettier, we can use a `--list-different` flag when we run Prettier. If there are any files that would be different if Prettier were to format them, then it will fail the script. Otherwise, the script will pass.