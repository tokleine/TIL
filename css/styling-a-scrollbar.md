# How to style scrollbars
## tl;dr
Be cautious when using [scrollbar-width](https://developer.mozilla.org/en-US/docs/Web/CSS/scrollbar-width) property in css!

## Description
I was recently trying to style a scrollbar on a C# + TypeScript frontend with CSS. The scrollbar had been developed by someone else and I wanted to tweak its look. None of my changes were reflected in the rendered page correctly. It turns out that ``scrollbar-width`` is a fallback property used mainly by non-webkit browsers and that by setting it your sneakely override any and all other styling like e.g. ``border-top-left-radius: 10px;``. As soon as I removed the property, my styling was applied as expected. Problem solved :-)
