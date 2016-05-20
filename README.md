# KSS Exploration

I've dissected and documented KSS for my needs. Maybe you'll find this helpful too?

## First steps

I'd like to use KSS to create style guides for Drupal 8 projects. `kss-node` is a project that expands on the original KSS and adds some useful additions.

* Install [kss-node](https://github.com/kss-node/kss-node) into your directory with `npm install --save-dev kss-node`. 
* You could install it globally, but why?
* So how do you run it from the local package? `./node_modules/.bin/kss`. No one has time for that.
* `npm install -g npm-run`. Yes, globally. [This'll let you run local modules](https://www.npmjs.com/package/npm-run) like a champ. 
* `npm run kss` to see kss options.

## There are a lot of options

* To see what a generated style guide looks like run `npm-run kss --demo`. It'll create a styleguide for you to check out.
* That's great. How do I write my own style guide?
* [Download the `demo` folder](https://github.com/kss-node/kss-node/tree/master/demo) from the project to dissect it.
* :headdesk:
* :headdesk:
* [RTFM](https://github.com/kss-node/kss/blob/spec/SPEC.md)
* :headdesk:
* 🎉
* We'll talk about writing the style guide stuff in a bit.

## Right now, I want to talk about styling the style guide itself

* `kss-node` uses "builders" to create style guides. You can get your hands on one with `kss --clone custom-builder`
* The `custom-builder` folder only has handlebars stuff. I want to use twig.
* #$%&
* Ransack the `kss-node` repo and steal `builder/twig` and rename that to `custom-builder`, though honestly you can name it whatever you like. I like to take my chances with the fact that I'll probably overwrite it by accident.






