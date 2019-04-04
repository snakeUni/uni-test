# Configure Prettier

Prettier is a pretty opinionated tool, but it does allow for some customization. In this lesson we’ll check out [the prettier playground](https://prettier.io/playground/) and see what options we want to enable in our project’s `.prettierrc` file.

After adding in our custom configuration, we’ll create a `.prettierignore` file so that you can avoid formatting any files generated within the project such as `node_modules` or a `build` folder.

```jsx
提取码: heyk
```

[观看视频](https://pan.baidu.com/s/1RRqRG2P82xbetqaY2Vs27Q)

[Code](https://github.com/kentcdodds/static-testing-tools/tree/step-4)

## Transcript

When I ran Prettier on my code, it actually changed a couple things. Now,I have double quotes instead of single quotes, and I added semicolons. None of these things are actually changing the way that the program runs, but it is divergent from my personal style. Prettier allows you to configure some things with the way that it formats your code.

Let's take a look at the [Prettier Playground](https://prettier.io/playground) here to see what options are available. You can choose a `--parser`, but that'll be chosen based off of the file name, so we don't need to deal with that. There's also a `--print-width`, so we can make it out to the width that we specify.

![](http://res.cloudinary.com/dg3gyk0gu/image/upload/v1543908127/transcript-images/javascript-configure-prettier-playground.png)

I'll go ahead and leave the `--print-width` at 80. There's also a `--tab-width`, so four spaces versus two spaces. Even one space, or three, or four, whatever you want to do here. I like to leave it at two. You can also specify to use tab characters instead of spaces. I'll leave that off.

Then you can choose `--single-quote` instead of double quotes. There's also `--no-bracket-spacing`. That's something I prefer. These brackets around here go away right here. `--prose-wrap` applies to stuff like Markdown. I prefer that, so I'll say `always`.

I prefer no semicolons, so I'll remove those with `--no-semi`. JSX bracket next line, we'll put the closing bracket on the same line with `--jsx-bracket-same-line`. I don't like that, so we'll leave it. `--arrow-parens`, I like to avoid those. We can have them always be printed, but I'll avoid those. I like trailing all commas. That comma can be trailing there with `--trailing-comma`. I prefer that.

![](http://res.cloudinary.com/dg3gyk0gu/image/upload/v1543908126/transcript-images/javascript-configure-prettier-playground-settings.png)

Let's go ahead, and I'm going to create a configuration file that has all of these options enabled. Where we put that is right at the root. We'll add a `.prettierrc`, and then I'll just paste this code in here with all of those configuration options that I specified.

.prettierrc

```js
{
"arrowParens": "avoid",
"bracketSpacing": false,
"jsxBracketSameLine": false,
"printWidth": 80,
"proseWrap": "always",
"semi": false,
"singleQuote": true,
"tabWidth": 2,
"trailingComma": "all",
"useTabs": false
}
```

Now, if I run `npm run format`, it will run a formatting with the configuration options that I wanted.

Terminal Input

```js 
npm run format
```

Another bit of configuration that I want to do here is, in normal projects, you're going to have directories where it has generated code, whether that's for your coverage reports or your build files. We don't want to format those.

I'm going to add another file called `.prettierignore` with a dot in front. I want to ignore `node_modules`, which is the default, but I'll put this in here as well. I'll add `coverage`, `dist`, `build`, `.build`, whatever makes sense for your situation. We'll just say `etc`. With that, now, I won't worry about Prettier attempting to format my generated files in my project.

.prettierignore

```js
node_modules
coverage
dist
build
.build

# etc...
```

In review, all that we needed to do to configure Prettier is we added a `.prettierrc` file in our project, with all the configuration options that we wanted. Then we added also a `.prettierignore` file, so that we can make sure that Prettier doesn't attempt to format files that are generated.

With that configuration, we ran our `npm run format` script again, which runs `prettier --write` across all the files that Prettier supports. That reformatted our example to look the way that I wanted it to.