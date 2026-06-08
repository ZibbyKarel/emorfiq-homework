# Analyses

Current repo and documented proposed improvements:

1. [Accessibility](ACCESSIBILYTY.md) — semantic and WCAG issues in the product card.
2. [Performance](PERFORMANCE.md) — runtime, build, and font-loading improvements.

Note:
this repo was updated with claude code. In real life scenerio I would have a proper skills and agents set up in .claude directory. For speeding things up and that this was just a home assignemt I skipped that. 

I usually let claude investigate a project, explain to me what is where. Then I plan with Opus (we iterate until I'm ok with the plan) and code with it as well or change to Sonnet. 

For token savings I activelly using grapify and some other stuff I have globally installed like rtk.

---

original readme below:

# Requirements

1. Node >=16
2. Php
3. Figma

# Installation

1. npm i
2. run index.php in php http server

# Modes

You can switch modes in index.php:2.
In development the live reload will work in combination with node script development. The url in command line https://prnt.sc/cI4U0xLMEAzB is not working because there is no internal server included, it is just form Hot module replacement.

# Assets

## Css

1. Dir /assets/scss

### The idea of theming

1. If we need to change anything in our component (i.e. background in product-card) we use only variables to do it if it is possible.
2. If it is not possible we can add custom css but never modifying css in the component itself.
3. The example of theming in css is in assets/scss/theme/product-card/
4. In the html it is preferred not to change anything but if you have to you can do it.

## Js

1. Dir /assets/js
2. No javascript needed

## Images

1. Dir /public/images
