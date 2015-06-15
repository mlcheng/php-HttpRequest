# php-http_request

The `HttpRequest` in `http_request.php` will simplify cURL calls. This can be used to retrieve information from a server, or to communicate with backend APIs.

## Usage
You are able to perform `GET` or `POST` requests so far. To do so, just create the `HttpRequest` object with the URL

```php
$request = new HttpRequest("https://yourwebsite.com/api/person");
```

Next, set the parameters along with the request method

```php
$request->get(array(
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
