Common Regular Expressions for Django URLs
======

A list of common regular expressions for use in django url's regex.


Example Django URLs patterns:

```python
from django.conf.urls import url, include
# Django 1.9 and Up (required in Django 1.10+)
# urls.py

from django.conf.urls import url, include
from appname.views import (
              AboutView,
              article_detail, 
              ContactView,
              home_view, 
              profile_detail,
              )


urlpatterns = [
    # Examples:
    url(r'^$', home_view, name='home'),
    url(r'^contact/$', ContactView.as_view(), name='contact'),
    url(r'^about/$', AboutView.as_view(), name='about'),
    url(r'^profile/(?P<username>[\w.@+-]+)/$', profile_detail, name='profile'),
    url(r'^article/(?P<slug>[\w-]+)/$', article_detail, name='article'),
    url(r'^blog/', include("blog.urls")),
    url(r'^admin/', admin.site.urls),
]


# Django 1.8 and below
# urls.py
from appname.views import (
              AboutView,
              ContactView,
              )
              
              
urlpatterns = patterns('',
    url(r'^$', 'appname.views.home_view', name='home'),
    url(r'^contact/$', ContactView.as_view(), name='contact'),
    url(r'^about/$', AboutView.as_view(), name='about'),
    url(r'^profile/(?P<username>[\w.@+-]+)/$', 'appname.views.profile_detail', name='about'),
    url(r'^article/(?P<slug>[\w-]+)/$', 'appname.views.article_detail', name='about'),
    url(r'^blog/', include('blog.urls')),
    url(r'^admin/', include(admin.site.urls)),
)

```




### Username (user's username)

Regex:

```
(?P<username>[\w.@+-]+)
```

##### Example:

Parameters:

```python
username = 'email@email.com' 
or 
username = 'myusername' ## this paramater can be either email or username fields
```

Query:

```python
object = UserModel.objects.get(username=username)
```

Url:

```
url(?P<username>[\w.@+-]+)$', 'appname.views.show_user'),
```

View:

```python
def show_user(request, username):
    ...
    return ...
```

Live usage:

```
yourdomain.com/email@email.com/

or

yourdomain.com/myusername/

```


### Object ID (user id, profile id, group id, etc)
Regex:

```
(?P<order>\d+)
```

##### Example

Parameters:

```python
id = 1
```

Query:

```python
object = Model.objects.get(id=id)
```

Url:

```
url(r'^(?P<id>\d+)$', 'appname.views.item_id'),
```

View:

```python
def item_id(request,id):
    ...
    return ...
```

Live usage:

```
yourdomain.com/12/
```


### Username with Object Order
Regex:
```
(?P<username>[\w.@+-]+)/(?P<order>\d+)
```

##### Example

Parameters: 
```python
username = "myusername"

order = 13
```

Query:

```python
user_object = UserModel.objects.get(username=username)
queryset = UserItem.objects.filter(order=order, user=user)
```

Url:

```
url(r'^(?P<username>[\w.@+-]+)/(?P<order>\d+)/$', 'appname.views.item_home', name='home'),
```

View:

```python
def item_home(request, username, order):
    ...
    return ...
```

Live usage:
```
yourdomain.com/useritem/myusername/13/
```



### Slugs
Regex:
```
(?P<slug>[\w-]+)
```

##### Example

Parameters: 
```python
slug = "slugged-item"
```

Query:
```python
object = Articles.objects.get(slug=slug)
```

Url:
```
url(r'^(?P<slug>[\w-]+)/$', 'appname.views.article'),
```

View:
```python
def article(request,article):
    ...
    return ...
```

Live usage:
```
yourdomain.com/your-slug/
````


### Digits and Dates (through digits)

Regex:

```
4 Digits like 2015
(?P<year>\d{4})

2 Digits like 12
(?P<month>\d{2})

Any Digits like 1231 or 123438192
(?P<article_id>\d+)
``` 

##### Example

Parameters: 
```python
year = 2015
month = 01
article_id = 412
```

Query:
```python
year_queryset = Articles.objects.filter(year=year)
months_in_year_queryset = Articles.objects.filter(year=year).filter(month=month)
article_object = Articles.objects.get(id=article_id)
```

Url:
```
(r'^articles/(?P<year>\d{4})/$', views.year_archive),
(r'^articles/(\d{4})/(?P<month>\d{2})/$', views.month_archive),
(r'^articles/(?P<year>\d{4})/(?P<month>\d{2})/(?P<article_id>\d+)/$', views.article_detail),
```

View:
```python
def year_archive(request, year):
    return ..

def month_archive(request, month):
    return ..

def article_detail(request, year, month, article_id):
    ...
    return ...
```

Live usage:

```
yourdomain.com/2015/
yourdomain.com/2015/03/
yourdomain.com/2015/03/21/
```
    



If you find other regular expressions you are unsure of their meaning, feel free to [contact us](mailto:codingforentrepreneurs@gmail.com).

Thank you!

Coding for Entrepreneurs
