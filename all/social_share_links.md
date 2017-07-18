Social Sharing with Anchor Tags
======

Use html anchor tags to share links on major social networks.

Basic URL Text Encoder: [http://meyerweb.com/eric/tools/dencoder/](http://meyerweb.com/eric/tools/dencoder/)


## Facebook

```
<a href="https://www.facebook.com/sharer/sharer.php?u=http://CodingForEntrepreneurs.com/">
Share on Facebook
</a>
```
Naturally you can replace `http://CodingForEntrepreneurs.com/` with your own link.


## Twitter

```
<a href="https://twitter.com/home?status=I'm%20going%20to%20learn%20to%20Code...%20Come%20build%20an%20web%20apsp%20with%20me!%20%23CFE%20and%20@justinmitchel%20http://codingforentrepreneurs.com/">
Share on Twitter
</a>
```
Now, Twitter is a little trickier. It needs to be url-encoded text. So something like this:

```
I'm%20going%20to%20learn%20to%20Code...%20Come%20build%20web%20apps%20with%20me!%20%23CFE%20and%20@justinmitchel%20http://codingforentrepreneurs.com/

```
Is actually:
```
I'm going to learn to Code... Come build web apps with me! #CFE and @justinmitchel http://codingforentrepreneurs.com/
```
Notice that spaces are `%20` and hash tags `#` are `%23` instead of actual space. This format will ensure it's shared properly. 

So, here's how it is:

``` 
Base url: <a href="https://twitter.com/home?status=">Share on Twitter</a>

Set "?status=" to your html string like: 

I'm%20going%20to%20learn%20to%20Code...%20Come%20build%20web%20apps%20with%20me!%20%23CFE%20and%20@justinmitchel%20http://codingforentrepreneurs.com/

Then your <a> tag becomes:

<a href="https://twitter.com/home?status=I'm%20going%20to%20learn%20to%20Code...%20Come%20build%20an%20web%20apsp%20with%20me!%20%23CFE%20and%20@justinmitchel%20http://codingforentrepreneurs.com/">
Share on Twitter
</a>

```

## Google Plus

Google Plus is pretty easy. Use this:
```
<a href='https://plus.google.com/share?url=http://codingforentrepreneurs.com'>Share on Google+</a>
```
Replace `http://codingforentrepreneurs.com` with your url



## LinkedIn

Very similiar to Twitter:
```
<a href="https://www.linkedin.com/shareArticle?mini=true&url=http://swiftforentrepreneurs.com/&title=Be%20first%20%7C%20Join%20Swift%20for%20Entrepreneurs&summary=Swift%20for%20Entrepreneurs%20is%20a%20project-based%20programming%20course%20for%20non-technical%20founders.%20We'll%20learn%20how%20to%20build%20iOS%20apps%20from%20scratch%20using%20Apple's%20new%20programming%20language:%20Swift.%20Be%20first%20and%20learn%20with%20me!&source=http://swiftforentrepreneurs.com/">
Share on Linkedin
</a>
```
Base url:  https://www.linkedin.com/shareArticle

Optional attributes: mini, url, title, summary, source


Add your attributes to the base url as needed
```
mini = True #or false

url = http://codingforentrepreneurs.com/ 
#Your website's url

title = Be%20first%20%7C%20Join%20Swift%20for%20Entrepreneurs 
#The title for your linkedin article title

summary = Swift%20for%20Entrepreneurs%20is%20a%20project-based%20programming%20course%20for%20non-technical%20founders.%20We'll%20learn%20how%20to%20build%20iOS%20apps%20from%20scratch%20using%20Apple's%20new%20programming%20language:%20Swift.%20Be%20first%20and%20learn%20with%20me! 
# this is the actual message

source = http://swiftforentrepreneurs.com/
# Where your article orginiated.

```

Now that you have different attributes you add them to your base URL as such:

```
https://www.linkedin.com/shareArticle?mini=...&url=...&title=...&summary=...&source=...

```
Replace the "..." with the values you want.


## Reddit

A lot like Twitter and LinkedIn

```
<a href="http://www.reddit.com/submit?url=http://swiftforentrepreneurs.com/&title=Unlock%20to%20Learn%20Swift%20for%20Free!%20By%20Swift%20for%20Entrepreneurs.%20Made%20for%20Non%20Techincals.">Share on Reddit</a>
```

Base URL and Attributes
```
base_url = http://www.reddit.com/submit
attributes = url, title
```
In this example the url and title are:
```
url = http://swiftforentrepreneurs.com/
title = Unlock%20to%20Learn%20Swift%20for%20Free!%20By%20Swift%20for%20Entrepreneurs.%20Made%20for%20Non%20Techincals.
```

Add them all together like:

```
http://www.reddit.com/submit?url=...&title=...
```
Replace "..." with the value of the attribute.



## Pinterest
First add the `Javascript` to your `base.html` file if you're using Django. 

```
<script async defer src="https://assets.pinterest.com/js/pinit.js"></script>
```

Then add the anchor/img tags. What you have to do here is replace the <img> tag with your own image source. 

```
<a data-pin-do="buttonBookmark" href="//www.pinterest.com/pin/create/button/"><img src="//assets.pinterest.com/images/pidgets/pinit_fg_en_rect_gray_20.png" /></a>
```
Something in `Django` might look like:

```
<a data-pin-do="buttonBookmark" href="//www.pinterest.com/pin/create/button/"><img src="{{ object.image.url }}" /></a>

```





