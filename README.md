# How to make a PUT request to aws s3 presigned url

#### FETCH API (upload json data)
```
// example s3 buckect signed url
let signedUrl = "https://adilo-encoding.s3.us-east-2.wasabisys.com/mjhvjgftrFGgdf/gCdSgSsu/gCdSgSsu.mp3?partNumber=1&uploadId=3oj4R1F8tyjrns82scnorAfwR4E2jF2YtEsPA34TK8opZXSj3V3gKsOLL7BF1gddshgdssRHs4l8ui0OnPKip9Im7DZizPwi_EGFw4dn70wydOaaTidl0JDR4yq9R58nMQk6jI8M&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=B3HSNGHP0MKECQHXBMdsfsaea22%f2F20220124%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Date=20220124T053944Z&X-Amz-SignedHeaders=host&X-Amz-Expires=1200&X-Amz-Signature=0be0b1dfbd24215b0d872960ed5a71e4ac7b3704d33b6cb294d52a304a9c1132";

let data = {
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
};

fetch(signedUrl, {
      method: 'PUT',
      headers: {
        'Content-type': 'application/json'
      },
      body: JSON.stringify(data)
}).then(response => response.json())
.then(data => { console.log(data) });
```

#### Node.js (upload a video file)
```
var request = require('request');
var fs = require('fs');

// example s3 buckect signed url
let signedUrl = "https://adilo-encoding.s3.us-east-2.wasabisys.com/mjhvjgftrFGgdf/gCdSgSsu/gCdSgSsu.mp3?partNumber=1&uploadId=3oj4R1F8tyjrns82scnorAfwR4E2jF2YtEsPA34TK8opZXSj3V3gKsOLL7BF1gddshgdssRHs4l8ui0OnPKip9Im7DZizPwi_EGFw4dn70wydOaaTidl0JDR4yq9R58nMQk6jI8M&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=B3HSNGHP0MKECQHXBMdsfsaea22%f2F20220124%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Date=20220124T053944Z&X-Amz-SignedHeaders=host&X-Amz-Expires=1200&X-Amz-Signature=0be0b1dfbd24215b0d872960ed5a71e4ac7b3704d33b6cb294d52a304a9c1132";

// path to file
let filePath = './exampleFile.mp4';

// make request
request({
  method: 'PUT',
  url: signedUrl,
  body: fs.readFileSync(filePath),
  headers: {
    'Content-type': 'video/mp4',
  },
}, function (error, response, body) {
    if (error) {
      return console.error('upload failed: ', error);
    }
    console.log('Upload successful!  Server responded with: ', body);
});

```

#### PHP (upload a video file)
```
use GuzzleHttp\Client;

// example s3 buckect signed url
$signedUrl = "https://adilo-encoding.s3.us-east-2.wasabisys.com/mjhvjgftrFGgdf/gCdSgSsu/gCdSgSsu.mp3?partNumber=1&uploadId=3oj4R1F8tyjrns82scnorAfwR4E2jF2YtEsPA34TK8opZXSj3V3gKsOLL7BF1gddshgdssRHs4l8ui0OnPKip9Im7DZizPwi_EGFw4dn70wydOaaTidl0JDR4yq9R58nMQk6jI8M&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=B3HSNGHP0MKECQHXBMdsfsaea22%f2F20220124%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Date=20220124T053944Z&X-Amz-SignedHeaders=host&X-Amz-Expires=1200&X-Amz-Signature=0be0b1dfbd24215b0d872960ed5a71e4ac7b3704d33b6cb294d52a304a9c1132";

// path to file
$filePath = './exampleFile.mp4';

$headers = [
  'Content-Type' => 'video/mp4',
  'accept'       => 'application/json',
];

$client = new \GuzzleHttp\Client(['headers' => $headers]);

$result = $client->request('PUT', $signedUrl, [
  'body' => file_get_content($filePath)
]);

$response = $result->getBody()->getContents();
$data = json_decode($response, true);

```
