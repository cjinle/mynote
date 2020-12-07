# Python:用urllib2库，带Cookie请求URL页面

### 方法一：
```python
import urllib2
opener = urllib2.build_opener()
opener.addheaders.append(('Cookie', 'cookiename=cookievalue'))
f = opener.open("http://example.com/")
```


### 方法二：
```python
import urllib2
import urllib
from cookielib import CookieJar

cj = CookieJar()
opener = urllib2.build_opener(urllib2.HTTPCookieProcessor(cj))
# input-type values from the html form
formdata = { "username" : username, "password": password, "form-id" : "1234" }
data_encoded = urllib.urlencode(formdata)
response = opener.open("https://page.com/login.php", data_encoded)
content = response.read()
```