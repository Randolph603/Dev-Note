# Fetch has been blocked by CORS policy

> // Fetch the weather conditions in Kansas City, Missouri
  fetch("https://www.metaweather.com/api/location/2430683/");
>
> **Error**:
  Access to fetch at 'https://www.metaweather.com/api/location/2430683/'
  from origin 'http://localhost:4000' has been blocked by CORS policy: No
  'Access-Control-Allow-Origin' header is present on the requested
  resource. If an opaque response serves your needs, set the request's
  mode to 'no-cors' to fetch the resource with CORS disabled.


## Solution 1: Change from server side (API)
Add bellow similar lines into your server's response to permit/deny your requests.

>- Access-Control-Allow-Origin: http://permitted.origin.com
>- Access-Control-Allow-Methods: POST, GET, OPTIONS
>- Access-Control-Allow-Headers: Content-Type

## Solution 2: Add proxy server inside package.json
1. single proxy
```json
{
  "proxy": "https://api.weixin.qq.com"
}
```
``` js
const uri = `/cgi-bin/token?...`;

fetch(uri, { method:  'GET' })
.then(blob  =>  blob.json())
.then(response  =>console.log(response));
```

2. multiple proxy
```json
"proxy": {
   "/eg-api01": {
      "target": "http://my.example.com",
      "changeOrigin": true,
      "secure": false
    },
   "/eg-api02": {
      "target": "http://her.example.com",
      "changeOrigin": true,
      "secure": false
    }
}
```
``` js
const uri = `/cgi-bin/token?...`;

fetch(uri, { method:  'GET' })
.then(blob  =>  blob.json())
.then(response  =>console.log(response));
```

## Solution 3: use npm package "fetch-jsonp"

```js
import fetchJsonp from 'fetch-jsonp'
fetchJsonp(baseUrl + 'location=39,116&output=json', { method:  'GET' })
    .then( response => response.json() )
    .then(data => console.log(data))
```

***Not suggest this one as only work for GET**

## Solution 4: use proxy website "https://cors-anywhere.herokuapp.com/"

```js
 const uri = `https://api.weixin.qq.com/cgi-bin/token?grant_type...`;
 const proxyUrl = 'https://cors-anywhere.herokuapp.com/';
 fetch(proxyUrl + uri, { method: 'GET' })
      .then(blob => blob.json())
      .then(response => console.log(response));
```

## Solution 5: use npm package "http-proxy-middleware"
You can use this feature in conjunction with the **proxy** property in **package.json**, but it is recommended you consolidate all of your logic into **src/setupProxy.js**.

1. install http-proxy-middleware using npm or Yarn:

>$ npm install http-proxy-middleware --save
>
>$ yarn add http-proxy-middleware

2. create src/setupProxy.js and place the following contents in it:

```js
const { createProxyMiddleware } = require('http-proxy-middleware');

module.exports = function(app) {
  app.use(
    '/cgi-bin',
    createProxyMiddleware({
      target: 'https://api.weixin.qq.com',
      changeOrigin: true,
    })
  );

  app.use(
    '/cgi-bin2',
    createProxyMiddleware({
      target: 'https://api.weixin2.qq.com',
      changeOrigin: true,
    })
  );
};
```

ref: https://www.npmjs.com/package/http-proxy-middleware

ref: https://create-react-app.dev/docs/proxying-api-requests-in-development