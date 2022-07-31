# sass-interpolate
Interpolate a CSS property on different screen dimensions

## Installation

```bash
npm install sass-interpolate
```

## Usage

```scss
@use "sass-interpolate" as i;

@include i.interpolate(834px 1440px, (
    font-size: 18px 22px,
    line-height: 34px 51px,
));
```

## Use cases

[//]: # (TODO)

+ Fluid typography:
  + [Fluid Typography | CSS-Tricks](https://css-tricks.com/snippets/css/fluid-typography/)
  + [Fun Tip: Use calc() to Change the Height of a Hero Component | CSS-Tricks](https://css-tricks.com/fun-tip-use-calc-to-change-the-height-of-a-hero-component/)
+ Responsive layout

## Theory

[//]: # (TODO)

## History

Despite being useful for defining typography, this tool was initially created for serving a different purpose.

Back in 2020 I was making frontend for a simple company website. The biggest part of it was two landing pages. I had a quite elaborate design from a colleague of mine: it had variations for desktop, laptop, tablet and mobile devices.

The problem was, many of the elements on the design had some minor tweaks between different devices in a way that you couldn't tell which tweak is supposed to be at which breakpoint for sure. I could have gathered all of them and ask the designer. But I didn't want to spend a lot of time on discussion and chatting about the things that seem too minor for that.

So I've thought of an idea. What if I just had "something in the middle" between those design variations?

And I've started researching.

For the sake of simplicity, let's assume the design had a rectangle that needed to be `200px` wide on `600px` viewport width and `300px` wide on `1400px` viewport width.

Using `vw` instead of hardcoded `px` inside `@media` queries would make the layout more fluid and look similar to what I was trying to do. It had a dependency on the viewport width, a good start. But that wasn't enough, as I needed to match the property values on the desired breakpoints exactly.

I've constructed a `calc()` expression that looked something like this: `width: calc(0.125vw + 125px)`. It worked! And to me, it looked very similar to a [linear function](https://en.wikipedia.org/wiki/Linear_function). It came to me quickly that what I was trying to do is called [linear interpolation](https://en.wikipedia.org/wiki/Interpolation).

At first, online calculators helped to build more of these linear interpolation formulas. But I quickly realised that I need to craft those expressions in Sass directly. Time to research more!

I don't exactly remember what were the keywords I've entered into search engine, but I (sadly) couldn't find the implementation I was looking for... The only useful thing I've come around was [Jake Wilson's `linear-interpolation` function](https://gist.github.com/Jakobud/7414f91142e0f540f221a3e3cafdf856). So I've decided to transform that into a mixin.

I was very close to finding the [poly-fluid-sizing](https://github.com/Jakobud/poly-fluid-sizing) library from the same author, but that didn't happen. I found it only now, in July 2022, shortly after creating this repo and doing additional minor research.

So here we are. I'm sharing this implementation publicly mainly because I would like to reuse it across my projects, but at the same time I would be happy if this would be of use to you, dear reader. Hope it serves you a great purpose! :)

## Alternatives

+ [poly-fluid-sizing](https://github.com/Jakobud/poly-fluid-sizing)
+ [scss-slope-calc](https://github.com/unionco/scss-slope-calc)

## Related

[//]: # (TODO)

+ [Fluid Responsive Typography With CSS Poly Fluid Sizing — Smashing Magazine](https://www.smashingmagazine.com/2017/05/fluid-responsive-typography-css-poly-fluid-sizing/)
+ [The 100% correct way to do CSS breakpoints | by David Gilbertson | Medium](https://medium.com/free-code-camp/the-100-correct-way-to-do-css-breakpoints-88d6a5ba1862)
