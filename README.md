# KSS Exploration

I've dissected and documented my journey with [KSS (Knyle Style Sheets)](http://warpspire.com/kss/) for my needs. Maybe you'll find this helpful too?

## First steps

I'd like to use KSS to create style guides for Drupal 8 projects. `kss-node` is a project that expands on the original KSS spec and adds some useful additions (such as markup).

* Install [kss-node](https://github.com/kss-node/kss-node) into your directory with `npm install --save-dev kss-node`. 
* You could install it globally, but why?
* So how do you run it from the local package? `./node_modules/.bin/kss`. No one has time for that.
* `npm install -g npm-run`. Yes, globally. [This'll let you run local modules](https://www.npmjs.com/package/npm-run) like a champ. 
* `npm-run kss` to see kss options.

## There are a lot of options

* To see what a generated style guide looks like run `npm-run kss --demo`. It'll create a styleguide for you to check out.
* That's great. How do I write my own style guide?
* [Download the `demo` folder](https://github.com/kss-node/kss-node/tree/master/demo) from the project to dissect it.
* :headdesk:
* :headdesk:
* [RTFM](https://github.com/kss-node/kss/blob/spec/SPEC.md)
* 🎉
* We'll talk about writing the style guide stuff in a bit.

## Right now, I want to talk about styling the style guide itself

* `kss-node` uses "builders" to create style guides. You can get your hands on one with `npm-run kss --clone custom-builder`
* The `custom-builder` folder only has handlebars stuff. I want to use twig.
* #$%&
* Ransack the `kss-node` repo and steal `builder/twig` and rename that to `custom-builder`, though honestly you can name it whatever you like. I like to take my chances with the fact that I'll probably overwrite it by accident.
* `builder.js` does the magic. Leave it be.
* `index.twig` JACKPOT. This is the template that'll get used to create the style guide pages.
* Use your ✨HTML MAGIC ✨ to make it yours.
* Come back to the project later and rename `custom-builder` to `custom-builder-twig`.
* Once you have your template ready for primetime, run `npm-run kss --source [sourceFiles] --builder [templateFolder]`

## Can we create a config file?

* **Yes**
* Create `any-sensible-name.json` and define options.

```
{
  "//": "The source and destination paths are relative to this file.",
  "source": "./",

  "//": "The css and js paths are URLs relative to the style guide destination.",
  "css": [
    "styles.css"
  ],
  "js": [],
  "builder": "../custom-builder-twig",

  "title": "Amazing Rando's Style Guide",
  "verbose": true
}
```
* Run `npm-run kss --config demo/any-sensible-name.json`.

## So let's talk about those source files now.

* `kss-node` produces a microsite with one or more pages that show off your design work. Make it good.
* It does it's work based on the files in your source folder. We'll call that source folder `demo`, which is short for `demon`.
* We're going to go over a few key points. Your own arrangement and organization is up to you.
* `homepage.md` is the content of the style guide's homepage. Make it useful.
* If you've looked at `index.twig` you'll see that a menu is dynamically generated for you.
* So how do the other pages get created? Good question...
* Inside your CSS will be a line that starts with `Style guide:`. If you enter `Style guide: demo` there will be a root page "Demonstration of Styles".
* But how does KSS turn "demo" into "Demonstration of Styles"?
* At the top of your KSS comment in the CSS you gave it the title "Demonstration of Styles". [RTFM](https://github.com/kss-node/kss/blob/spec/SPEC.md)

```
// Demonstration of Styles
//
// Description of the work you're showing off. Blah, blah, [you're a winner](http://can-include-links.com).
//
// Style guide: demo
```
* Great now I can create `demo.buttons` and `demo.typography`.
* Render the style guide ... and buttons comes before typography, but I think that typography should come first.
* You work with Drupal, so you'll be familiar with the concept of Weight. -10 needs to eat a cheesburger and 10 is John Candy. This lets us sort by Weight, then by Alpha.

```
// Buttons
//
// Press 'em while they're hot.
//
// Weight: 1
//
// Style guide: demo.buttons
.buttons { ... }

// Typography
//
// Handcrafted, artisinal Comic Sans.
//
// Weight: -1
//
// Style guide: demo.typography
h1 { ... }
```

* Each section after the first adds a numbered subsection to the rendered Style Guide, so `demo.typography.headers` would be 1.1.1 and `demo.buttons.call-to-action` would be 1.1.14 (assuming 13 other button sections).
* Want more pages? `Style guide: typography`, `Style guide: buttons`, creates two pages sorted by Weight and Alpha.

## So what is in this repo? What do I do with it?

This repo is my collection of files to remind me of what to do with KSS.

* `custom-builder-twig` is the template for generated Style Guides.
* `demo` is setup with examples and is used as the basis for a Style Guide.
* `node_modules` isn't in this repo. C'mon!
* `styleguide` is the generated Style Guide.





