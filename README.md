# php-http_request

The `HttpRequest` in `HttpRequest.php` will simplify cURL calls. This can be used to retrieve information from a server, or to communicate with backend APIs.

## Usage
You are able to perform `GET` or `POST` requests. To do so, just create the `HttpRequest` object with the URL

```php
$request = new HttpRequest("https://yourwebsite.com/api/person/add");
```

Next, set the parameters along with the request method

```php
$request->post(array(
	"first_name"=>"Michael",
	"last_name"=>"Cheng"
));
```

If no parameters are needed, simply `->get()` or `->post()`

```php
$request->get()
```

The result will be attached to the return value of the request method. Therefore, you may wish to set

```php
$result = $request->get();
```

## Advanced usage
In addition to the request methods stated above, public facing methods also include the following

### `setHeaders()`
You may set headers to send along with the request. Method chaining can be performed

```php
$request->setHeaders(...)->post();
```

### `getCurlInfo()`
The cURL info may be retrieved after the request has been sent.

```php
$request->post();
$info = $request->getCurlInfo();
```

See [`curl_getinfo()`](http://php.net/manual/en/function.curl-getinfo.php) for more information.

## Sample application
An sample application would be to retrieve weather information from a remote server. The OpenWeatherMap provides an API we can use.

```php
$request = new HttpRequest("http://api.openweathermap.org/data/2.5/weather");
$result = $request->get(array(
	"q"=>"Taipei,TW",
	"units"=>"metric"
));
```

This would return a result of

```
{"coord":{"lon":121.53,"lat":25.05},"sys":{"type":1,"id":7479,"message":0.024,"country":"TW","sunrise":1434575048,"sunset":1434624349},"weather":[{"id":803,"main":"Clouds","description":"broken clouds","icon":"04d"}],"base":"stations","main":{"temp":30.82,"pressure":1004,"humidity":49,"temp_min":28.89,"temp_max":32},"visibility":10000,"wind":{"speed":5.7,"deg":250,"var_beg":220,"var_end":280},"clouds":{"all":75},"dt":1434590837,"id":1668341,"name":"Taipei","cod":200}
```

Which you can then parse.
