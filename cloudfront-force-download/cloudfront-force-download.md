# Force Download a file in a browser on Cloudfront
## type: Lambda@edge

```js
'use strict';
exports.handler = (event, context, callback) => {
    const querystring = event.Records[0].cf.request.querystring;
    const response = event.Records[0].cf.response;
    if (querystring.includes('download=true')){
        response.headers = {
            ...response.headers,
            "content-type": [
              {
                "key": "Content-Type",
                "value": "application/octet-stream"
              }
            ]
        }
    }
    callback(null, response);
};
```