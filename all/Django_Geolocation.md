# Django & Geolocation 

A quick guide for setting up for getting a user's IP address and geolocation details (from IP Address). 

Docs here: [http://kirr.co/0osovv](http://kirr.co/0osovv)

1. `pip install geoip2 pytz`

2. Create a new directory in your django root (ie where manage.py is) call it: `geoip` 

3. In your `settings.py`, add the following: `GEOIP_PATH = os.path.join(BASE_DIR, "geoip")`

4. Download the city + country datasets [here](http://kirr.co/lb5cb7), up zip those folders, and move the upzipped files into your newly created "geoip" folder within your Django app.

5. Now you can use the IP address stuff like:

```
from django.contrib.gis.geoip2 import GeoIP2

def get_client_ip(request):
    x_forwarded_for = request.META.get('HTTP_X_FORWARDED_FOR')
    if x_forwarded_for:
        ip = x_forwarded_for.split(',')[0]
    else:
        ip = request.META.get('REMOTE_ADDR')
    return ip

def your_request_view(request):
    ip_address = get_client_ip(request)
    if ap_address:
       g = GeoIP2()
       local_data = None
       try:
            local_data = g.city(ip_address)
       except:
            pass
       print(local_data)
    return render(request, "template.html", {})
```
