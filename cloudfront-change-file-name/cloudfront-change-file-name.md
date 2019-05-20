# Change file name for a file on Cloudfront
## type: Lambda@edge

```js
'use strict';
exports.handler = (event, context, callback) => {
    const querystring = event.Records[0].cf.request.querystring;
    const response = event.Records[0].cf.response;
    // filename should be the last or only query param
    if(querystring.includes('filename=')){
        const fileName = querystring.split('filename=')[1];
         response.headers = {
            ...response.headers,
            "content-disposition": [
              {
                "key": "Content-Disposition",
                "value": `attachment; filename="${fileName}"`
              }
            ]
        }
    }
    callback(null, response);
};

```