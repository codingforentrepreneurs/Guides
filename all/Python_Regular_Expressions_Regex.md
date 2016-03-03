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

`*` Means 0 or more characters are needed for match. `\d*` Must be 0 digits or more

`+` Means 1 or more characters are needed for match. `\d+` Must be 1 digit or more

`^` Denotes start of string

`$` Denotes end of string

`\b`: Matches empty string before or after a word

`|`: Used for `or` matches such as `(match|this|or|that)`


### Basic Examples

#### Example: Find 4 Digits in a String
```python
import re

some_string = "Here is some text. We want to find matches in. Let's find the number 1234 and the number 5342 but not the number 942003. "

regex_pattern = re.compile(r"\D(\d{4})\D")
matching_numbers = re.findall(regex_pattern, some_string)

print(matching_numbers)

```python

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


#### Example: Extract Capitalized Words

```python
import re

txt = "Can you find A Match with some words: Car, House, Shirt, Apple, Google, Facebook."

regex_pattern = re.compile("([A-Z]{1}[a-z]+)\s?")
matches = re.findall(regex_pattern, txt)

print(matches)
```



All items in `()` are what we want to return

`[A-Z]{1}` means matching item has 1 capital letter

`[a-z]+` means the matching item has lower case letter(s). If we change this portion to: `[a-z]*` we would also have `A` in our results.

`\s` means: do not include spaces in the result

`?` means repeat the previous pattern as needed, or repeat `([A-Z]{1}[a-z]+)\s` as many as needed.


#### Example: Capitalized and Punctuated. 

```python
import re

txt = "this is poor syntax"
txt2 = "This isn't poor syntax."

regex_pattern = re.compile("^[A-Z](.*)[\.\?\!]$")
matches = re.match(regex_pattern, txt2)

print(matches)
```

`^` Denotes start of string

`$` Denotes end of string

`^[A-Z]` means string must start capitalized

`(.*)` nearly any value in between start and end of the string

`[\.\?\!]$` Means that the string must end with `.`, `?`, or `!`


#### Example: Named Groups

```python
import re

p1 = re.compile(r'(?P<word>\b\w+\b)')

m1 = p1.search( '(((( Lots of punctuation )))' )

m1.group('word')

m1.group(1)


p2 = re.compile(r'(?P<slug>[\w-]+)/(?P<slug2>[\w-]+)')

m2 = p2.search( '/some-another/new-slug/' )

m2.group('slug')
m2.group(1)

m2.group('slug2')

m2.group(2)


p3 = re.compile(r'^(?P<id>\d+)')

m3 = p3.search('some-another/4232/')

if m3:
    print(m3.group("id"))

m4 = p3.search('4232/adsfs/asdf')

if m4:
    print(m4.group('id'))

txt = "123/string"

new_ = re.findall(p3, txt)

print(new_)

```


#### Example: Search & Replace


```python
import re

"""
Simple Replacement
"""
txt = "The flag is orange, purple, and white."

regex_pattern = re.compile( '(green|orange|black|purple)')

replace_with = 'Yellow'

new_str = re.sub(regex_pattern, replace_with, txt)

print(new_str)



"""
Below is replace with a function
"""

txt = "The flag is orange, purple, and white."

regex_pattern = re.compile( '(green|orange|black|purple)')

def replace_func(matchobj):
        print(matchobj.group(0))
        name = matchobj.group(0)
        if name == 'green': 
            return 'blue'
        elif  name == "orange": 
            return 'red'
        elif name == "black":
            return "white"
        else:
            return "flag"


new_str = re.sub(regex_pattern, replace_func, txt)

print(new_str)



new_string = regex_pattern.sub(replace_func, 'orange car and black interior')

print(new_string)


new_string = regex_pattern.sub( 'rad', 'orange car and black interior')

print(new_string)


"""
Include Count of Subtitutions occured
"""

new_string = regex_pattern.subn( 'rad', 'orange orange car and black interior')

print(new_string) #returns tuple



"""
Replacement (Substitution) with Groups and Named Groups
"""


regex_pattern_str = r'def\s+([a-zA-Z_][a-zA-Z_0-9]*)\s*\(\s*\):'

re.sub(regex_pattern_str,
        r'Make sure you use the function "\1"',  
         'def myfunc():')


named_regex_pattern = r'def\s+(?P<name>[a-zA-Z_][a-zA-Z_0-9]*)\s*\(\s*\):'

re.sub(named_regex_pattern,
        r'Make sure you use the function "\g<name>"',  
         'def myfunc():')



"""
Regex Replacement vs Python String Subsitution
"""


# Regex Replacement


letter = """
Dear {{ name }},

You're awesome! I love to see how hard you have been working in the
course! I would like to complement you, {{ name }}, because it's not always
easy to keep up this level of enthusiasm while you're working on 
something great.

That reminds me, {{ nam }}, would you please share what your idea is? 
{{ name }}, I'd like to tell you that I strongly believe that you can 
do anything you put your mind to. With belief, {{ name }}, you can 
build the life you've always wanted.

Cheers!

Justin
Team CFE
"""

regex_pattern = r'\{\{\s*([A-Za-z]{4})\s*\}\}'
replac_string = 'John'

new_letter = re.sub(regex_pattern, replac_string, letter)

print(new_letter)



regex_pattern = r'\{\{\s*(?P<name>[A-Za-z]{3,4})\s*\}\}'

def replace_func(matchobj):
        name = matchobj.group(0)
        if name: 
            return "John"

new_letter = re.sub(regex_pattern, replace_func, letter)
print(new_letter)



# Python String Subsitution

letter = """
Dear {name},

You're awesome! I love to see how hard you have been working in the
course! I would like to complement you, {name}, because it's not always
easy to keep up this level of enthusiasm while you're working on 
something great.

That reminds me, {name}, would you please share what your idea is? 
{name}, I'd like to tell you that I strongly believe that you can 
do anything you put your mind to. With belief, {name}, you can 
build the life you've always wanted.

Cheers!

Justin
Team CFE
""".format(name='John')

print(letter)

```




#### Validating Django Common Regex Patterns for URL Mapping
For each validation, be sure to `import re`.

Email Regex
```python
email = 'email@email.com' 
email_pattern = re.compile(r"^(?P<email>[\w.@+-]+)$")
result = email_pattern.search(email)
print(result.groups())
```

Username Regex
```python
username = 'myuser.name-abc'
spaced_str = "My name"
username_pattern = re.compile(r"^(?P<username>[\w.@+-]+)$")
result2 = username_pattern.search(username)
print(result2.groups())
invalid_username = username_pattern.search(spaced_str)
if not invalid_username:
    print("Yeah it's invalid")
"""
if you do print(invalid_username.groups()), you will see the following error: 
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'NoneType' object has no attribute 'groups'
"""
```

Email + Username Regex
```python
email = 'email@email.com'
username = 'myuser.name-abc'
invalid_username = "Some spaced username"

username_email_pattern = re.compile(r"^(?P<username_email>[\w.@+-]+)$")


result_username = username_email_pattern.search(username)
print(result_username.groups())

result_email = username_email_pattern.search(email)
print(result2.groups())

result_invalud_username = username_email_pattern.search(invalid_username)
if not result_invalud_username:
    print("Yeah it's invalid")
```


Slug Regex
```python
slug = "my-name-is-slug"
slug_pattern = re.compile(r"^(?P<slug>[\w-]+)$")

result = slug_pattern.search(slug)
print(result.groups())
```

ID Regex
```python

id_pattern = re.compile(r"(?P<order>\d+)")

result = id_pattern.search(id)
print(result.groups())

```

2 Regex Patterns (like a URL)
```python

username = 'myuser.name-abc'
id = "101"
url_path = "%s/%s/"%(username, id)
two_url_patterns = re.compile(r"^(?P<username>[\w.@+-]+)/(?P<order>\d+)/$")


result = two_url_patterns.search(url_path)
print(result.groups())
```


Years & Advanced Digits
```python
year_pattern = re.compile(r"^(?P<year>\d{4})$") 
year_pattern_adv = re.compile(r"^(?P<year>(20|19)\d{2})$") 
month_pattern = re.compile(r"^(?P<month>\d{2})") 
month_pattern_adv = re.compile(r"^(?P<month>([0]*[0-9]|1[0-2]))$") 
 
result = year_pattern.search("2015")  # must pass string for validation
print(result.groups())

re.match(year_pattern, "2015") # must pass string for validation
re.match(year_pattern_adv, "2015")
re.match(year_pattern_adv, "1020")

re.match(month_pattern, "12")
re.match(month_pattern, "20")
re.match(month_pattern, "2")

re.match(month_pattern_adv, "20")
re.match(month_pattern_adv, "2")
re.match(month_pattern_adv, "12")
```



##### Django Project Urls.py Patterns Examples
In Django, the matching regex group(s) (ie `?P<month>`, `?P<id>`, `?P<username>`) will be passed as a Keyword Argument (`**kwarg`) to the matching view.


```python
#urls.py

"""
Django 1.9+ Pattern Syntax
"""

from blog.views import (
        ArticleView,
        YearArchiveView,
        MonthArchiveView,
        PostSlugView,
        PostIdView,
        function_based_view,
    )

from orders.views import (
        OrderView,
        UserOrderView,
    )

from profiles.views import (
        ProfileView,
)

urlpatterns = [
    url(r'^about/$', function_based_view),
    url(r'^article/(?P<slug>[\w-]+)/$', ArticleView.as_view()),
    url(r'^blog/(?P<year>\d{4})/$', YearArchiveView.as_view()),
    url(r'^blog/(?P<year>\d{4})/(?P<month>\d{2})/$', YearArchiveView.as_view()),
    url(r"^order/(?P<order>\d+)/$", OrderView.as_view()),
    url(r"^order/(?P<username>[\w.@+-]+)/(?P<order>\d+)/$", UserOrderView.as_view()),
    url(r'^profile/(?P<username>[\w.@+-]+)/$', ProfileView.as_view()),
]


"""
Django 1.5-1.8 Pattern Syntax
"""
from blog.views import (
        ArticleView,
        YearArchiveView,
        MonthArchiveView,
        PostSlugView,
        PostIdView,
    )

from orders.views import (
        OrderView,
        UserOrderView,
    )

from profiles.views import (
        ProfileView,
)

urlpatterns = patterns('',
    url(r'^about/$', "blog.views.function_based_view"),
    url(r'^article/(?P<slug>[\w-]+)/$', ArticleView.as_view()),
    url(r'^blog/(?P<year>\d{4})/$', YearArchiveView.as_view()),
    url(r'^blog/(?P<year>\d{4})/(?P<month>\d{2})/$', YearArchiveView.as_view()),
    url(r"^order/(?P<order>\d+)/$", OrderView.as_view()),
    url(r"^order/(?P<username>[\w.@+-]+)/(?P<order>\d+)/$", UserOrderView.as_view()),
    url(r'^profile/(?P<username>[\w.@+-]+)/$', ProfileView.as_view()),
)


```




