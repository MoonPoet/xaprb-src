---
title: Browser variations in RegExp.exec()
date: "2006-01-14"
url: /blog/2006/01/14/browser-variations-in-regexpexec/
categories:
  - Web
---
IE6, Firefox 1.5 and Opera 8.5 handle regular expressions slightly differently. I analyzed them and learned some interesting things about the browsers. For this article, I'm using `abcde` as the input, and `/abc|d(e)/g` as the regular expression. The expression should match twice, and the second match should capture the letter "e" because it's in a capturing subexpression.

### Properties of match results

Calling `RegExp.prototype.exec()` with a global regular expression returns an Array object with some extra properties. IE and Opera don't quite agree with [ECMA-262](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf) -- they add extra properties and don't create properties that should exist (Firefox gets it right).

In case you don't know the ins and outs of JavaScript regexes, there is a subtlety about capturing subexpressions and global regular expressions. `exec` actually only looks for one match even though the expression is global, but sets the index at which the match happened. If I call it again, it keeps looking from where it left off, so I can loop through the successive matches. Each time the result is an array containing the current match, plus the captures and information about where the match occurred. As usual, index 0 of the array contains the text of the entire match, index 1 contains the first captured subexpression, and so on.

Here's what I get when I call `/abc|d(e)/g.exec("abcde")` twice in a row on the browsers in question:

| | Property | Value     | Property  | Value     |
|----------|-----------|-----------|-----------|-------|
| Firefox  |           | abc       |           | de    |
| Firefox  | 1         | undefined | 1         | e     |
| Firefox  | index     |           | index     | 3     |
| Firefox  | input     | abcde     | input     | abcde |
| IE       | input     | abcde     | input     | abcde |
| IE       | index     |           | index     | 3     |
| IE       | lastIndex | 3         | lastIndex | 5     |
| IE       |           | abc       |           | de    |
| IE       | 1         |           | 1         | e     |
| Opera    |           | abc       |           | de    |
| Opera    |           |           | 1         | e     |
| Opera    | index     |           | index     | 3     |
| Opera    | input     | abcde     | input     | abcde |

I got the results with a `for/in` loop, like so:

```JavaScript
var re = /abc|d(e)/g;
var result = re.exec("abcde");
for (var prop in result) {
  // ...
}
```

Here are the differences:

*        Opera doesn't enumerate over the first captured subexpression in the first result. In Firefox, it exists without a value (has the special value `undefined`), and in IE it exists **with a value** -- the empty string.
*        IE adds the proprietary `lastIndex` property to the result.

###      Subexpressions

I said Opera *doesn't enumerate over* the property named "1" in the first result. According to the spec, the property named "1" should still exist. Opera knows the property should exist, as I proved by examining the `length` property. Its value is 2 in all browsers, which is correct as specified by section 15.10.6.2 of the [spec](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf):

Performs a regular expression match of *string* against the regular expression and returns an Array object containing the results of the match, or **null** if the string did not match...  Let *n* be the length of *r*'s *captures* array. (This is the same value as 15.10.2.1's *NCapturingParens*.)

So, the length of the array *should* be 2 even in the first match, because the length of the array depends **only** on the number of capturing subexpressions in the pattern -- so the browsers are doing the right thing.

If the property exists, Opera should enumerate it in the `for/in` loop. The spec is clear about what properties are enumerable (section 15.2.4.7), and it never says such a property should get the `dontEnum` attribute, so I think Opera's behavior is incorrect. In fact, I'm pretty sure Opera is actually never creating the property. I ran some tests with an Array and set one of the properties to `undefined`. Opera still enumerates it, so it's not as though Opera doesn't enumerate properties that have no value. I think Opera is setting `length` to 2, but never creating properties for capturing subexpressions that don't participate in the match. Technically this does not violate the spec's instructions on an Array's `length` property, but it is suspicious.

The moral of the story is you shouldn't use a `for/in` loop when iterating through subexpressions. Just iterate from 0 through `length` minus one.

I take exception to IE giving the capture a value. The subexpression doesn't capture anything and doesn't participate in the match, so it should not have a value -- not even the empty string or `null`. I suppose this one is up for debate, but that's my personal opinion.

### IE's `lastIndex` property

Technically, this property shouldn't be there; it should be a property of the global `RegExp` object in ECMA-262, or the regex itself in later versions of JavaScript (I have no idea why you'd make it a property of a global object; that seems like it would cause all sorts of stupid bugs, so I think the way IE does it is probably a lot smarter than the spec).

### Other stuff

I spent a lot of time messing with the various browsers to see if I could find obscure bugs enumerating properties that don't exist, setting a value and then unsetting it on subsequent calls, and so forth. The good news is I didn't find any more bugs (though they could still exist!), and I found that the quasi-bugs discussed above are really trivial.
