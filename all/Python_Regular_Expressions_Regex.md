Python Regular Expressions Cheat Sheet
================

A cheat sheet for working with `Python` Regular Expressions (aka `regex`). [Offical Regex Docs](https://docs.python.org/dev/library/re.html)


### Common Symbols 

`\d` Any digit, matches `[0-9]`

`\D` Any non-digit, matches `[^0-9]`, opposite of `\d`


`\w` Any character, matches `[a-zA-Z0-9_]`

`\W` Any non-character, matches `[^a-zA-Z0-9_]`, opposite of `\w`


`\s` Any space (or whitespace), matches `[ \t\n\r\f\v]` *See Note Below

`\S` Any non-space (or whitespace), matches `[^ \t\n\r\f\v]`, opposite of `\s`

> _Note_ `\t\n\r\f\v` refers to escaped characters (below). When using `\s` (or `\S`) the escaped characters will be treated as whitespace:
```
\t: Tab
\n: Newline
\r: Carriage return
\f: Formfeed
\v: Vertical Tab
```



### Basic Examples

```
import re

some_string = "Here is some text. We want to find matches in. Let's find the number 1234 and the number 5342 but not the number 942003. "

regex_pattern = re.compile(r"\D(\d{4})\D")
matching_numbers = re.findall(regex_pattern, some_string)

print(matching_numbers)

```

The important part here is the `regex pattern`. Let's break it apart into 3 sections:

`r"<first><desired_match><last>"`

`<first>` is `\D`

`desired_match` is `(\d{4})`

`<last>` is `\D`


`<first>` is telling python that anything that isn't a digit, just ignore it.

`<last>` is telling python that anythingn that isn't a digit, just ignore it.

`desired_match` is saying that the pattern in `()` should be considered as a match. 

Putting `\d` would yeild all 3 sets of numbers `1234`, `5342`, and `942003`. 

Putting `\d{4}` is saying that the digits must be a at least 4 digits to match. 

The `<last>` portion prevents digits larger than 4.











