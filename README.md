# PHP module for HMAC Authentication with Kong

This is a PHP module for generating HTTP request headers for HMAC authentication with Kong. More specifically, [Kong's HMAC Authentication Plugin.](https://getkong.org/plugins/hmac-authentication/)

# Installation

composer.json

```
{
   "require":{
      "y-zono/kong-hmac":"0.1.*"
   }
}
```

# Usage

GET request:

```
<?php

require_once "vendor/autoload.php";

use KongHmac\KongHmac;

$userName = "user";
$secret = "secret";
$url = "https://example.com/items";

$headers = KongHmac::generateRequestHeaders($userName, $secret, $url);

$httpClient = new \GuzzleHttp\Client();
$response = $httpClient->request("GET", $url, ["headers" => $headers]);

print $response->getBody();
```

POST request:

```
<?php

require_once "vendor/autoload.php";

use KongHmac\KongHmac;

$userName = "user";
$secret = "secret";
$url = "https://example.com/items";
$data = ["a" => "x"];
$contentType = "application/json";

$headers = KongHmac::generateRequestHeaders($userName, $secret, $url, json_encode($data), $contentType);

$httpClient = new \GuzzleHttp\Client();
$response = $httpClient->request("POST", $url, ["json" => $data, "headers" => $headers]);

print $response->getBody();
```

# Reference
[peter-evans/kong-hmac-python](https://github.com/peter-evans/kong-hmac-python)

# License
MIT License - see the [LICENSE](https://github.com/y-zono/kong-hmac-php/blob/master/LICENSE) file for details