# JS Library to sort Tibetan 

After exploring different options for [tibetan collation](https://github.com/eroux/tibetan-collation) in JavaScript, there seems to be no viable option to sort Unicode Tibetan strings. This library hopes to fullfill this purpose in an elegant, modern and efficient manner.

### State of the art

The most logical option to sort Tibetan would by using [Intl.Collator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Collator). The problem is that all browsers seems to use [ICU](http://site.icu-project.org/) to implement this object, and ICU has a [bug on Tibetan collation](https://unicode-org.atlassian.net/browse/ICU-13224), which won't be fixed in the short term. It will take even more time for the fix to appear in mainstream browsers, so it's not even a middle term solution. Bugs have been filled for [Firefox](https://bugzilla.mozilla.org/show_bug.cgi?id=1370185), [ChakraCore](https://github.com/Microsoft/ChakraCore/issues/3175), [Chrome](https://bugs.chromium.org/p/chromium/issues/detail?id=729508) and Safari.

Pure Javascript implementations of `Intl.Collator` don't seem to exist, as the only `Intl` [polyfill](https://github.com/andyearnshaw/Intl.js/) [doesn't support it](https://github.com/andyearnshaw/Intl.js/#what-about-intlcollator).

The only library we found that would be of possible use is [lasca](https://github.com/atomgomba/lasca), but it proved very buggy and extremely inefficient.

### This implementation

This implementation aims at being very efficient, at the cost of difficult corner cases in Tibetan. As a consequence:
- it does not normalize strings (`\u0F77` is not treated like `\u0FB2\u0F71\u0F80`)
- it does not handle Sanskrit stacks very precisely (the ICU rule `&ཀར<ཀརྐ` is too difficult to handle)

## Installation

    yarn add tibetan-sort-js --save

## API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### compare

Compares two strings, can be used as argument of Array.compare(). 
The behavior is undefined if the arguments are not strings. Works
reasonably well with non-Tibetan strings.

**Parameters**

-   `a` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** first string to be compared.
-   `b` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** second string to be compared.

Returns **[number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** 0 if equivalent, 1 if a > b, -1 if a &lt; b

## TODO

- add an option to normalize strings

## Release history

See [change log](CHANGELOG.md).

## License

The code is Copyright 2017-2019 Buddhist Digital Resource Center, and is provided under the [MIT License](LICENSE).
