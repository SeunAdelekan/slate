---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='https://www.eyowo.com'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction

The Eyowo Developer API is a [RESTful](https://en.wikipedia.org/wiki/Representational_state_transfer) web service that provides developers with a powerful set of resources that can be utilized to build rich applications backed by Eyowo payment services.

The API makes use of standard HTTP request methods and response codes. The Developer API supports both form-encoded  and standard JSON requests. All responses rendered by the API are in JSON format.

Feel free to make use of the [sandbox]() to test integrations with the provided endpoints. It is a secure space created specifically for you to familiarize yourself with our services. 

We are constantly working on new features to help you build more feature rich applications. As such we constantly update this documentation with new resources. Follow us [@eyowo](https://twitter.com/eyowo) to stay up to date on new API releases.

# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

## Validate User

```shell
curl --location --request POST "https://api.console.eyowo.com/v1/users/auth/validate" \
  --header "Content-Type: application/json" \
  --header "X-App-Key: 842e87acd5ef90caae15fb7bcdf882e9" \
  --header "X-IV: 62d7d6e0bffa5d475a56f97b423bf368" \
  --data "{
	\"authData\": \"/YjqH1Fmv4wd5vZxE8FQxGQvNaYhldTNlNGDkrbVPBE=\"
}"
```

```ruby
require 'net/http'
require 'json'

uri = URI('https://api.console.eyowo.com/v1/users/auth/validate')
res = Net::HTTP.start(uri.host, uri.port, use_ssl: true) do |http|
  req = Net::HTTP::Post.new(uri)

  req['Content-Type'] = 'application/json'
  req['X-App-Key'] = '842e87acd5ef90caae15fb7bcdf882e9'
  req['X-IV'] = '62d7d6e0bffa5d475a56f97b423bf368'
  
  req.body = { authData: '/YjqH1Fmv4wd5vZxE8FQxGQvNaYhldTNlNGDkrbVPBE=' }.to_json
  http.request(req)
end

puts res
```

```javascript
const http = require('http');

const body = JSON.stringify({
    authData: '/YjqH1Fmv4wd5vZxE8FQxGQvNaYhldTNlNGDkrbVPBE=',
});

const request = new http.ClientRequest({
    hostname: 'https://api.console.eyowo.com',
    port: 80,
    path: '/v1/users/auth/validate',
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'Content-Length': Buffer.byteLength(body),
        'X-App-Key': '842e87acd5ef90caae15fb7bcdf882e9',
        'X-IV': '62d7d6e0bffa5d475a56f97b423bf368',
    }
});

request.end(body)
```
> Response

```json
{
  "success": true,
  "data": {
    "user": {
      "id": "OKHN8E4SS",
      "mobile": "2349095801772"
    }
  },
  "message": "Validation successful"
}
```

This endpoint facilitates the validation of a user via a given mobile number. Requests should be forwarded to the  `/v1/users/auth/validate` URL path.

### Request Body.
The request body of the validate user request consists of a single attribute.

Parameter | Type | Required | Description
--------- | ------- | ------ | -----------
mobile | string | true | Any string representation of a valid Nigerian mobile number.

### Response
A successful request receives a response with an HTTP 200 status code with a response body containing a data object consisting of the details of the validated user.

The `user` object contains the following attributes:

Parameter | Type | Description
--------- | ------- | -----------
id | string | The unique identifier of the Eyowo user.
mobile | string | The corresponding phone number of the registered user. 

## User Login

```shell
curl --location --request POST "https://api.console.eyowo.com/v1/users/auth/validate" \
  --header "Content-Type: application/json" \
  --header "X-App-Key: 842e87acd5ef90caae15fb7bcdf882e9" \
  --header "X-IV: 62d7d6e0bffa5d475a56f97b423bf368" \
  --data "{
	\"authData\": \"/YjqH1Fmv4wd5vZxE8FQxGQvNaYhldTNlNGDkrbVPBE=\"
}"
```

```ruby
require 'net/http'
require 'json'

uri = URI('https://api.console.eyowo.com/v1/users/auth/validate')
res = Net::HTTP.start(uri.host, uri.port, use_ssl: true) do |http|
  req = Net::HTTP::Post.new(uri)

  req['Content-Type'] = 'application/json'
  req['X-App-Key'] = '842e87acd5ef90caae15fb7bcdf882e9'
  req['X-IV'] = '62d7d6e0bffa5d475a56f97b423bf368'
  
  req.body = { authData: '/YjqH1Fmv4wd5vZxE8FQxGQvNaYhldTNlNGDkrbVPBE=' }.to_json
  http.request(req)
end

puts res
```

```javascript
const http = require('http');

const body = JSON.stringify({
    authData: '/YjqH1Fmv4wd5vZxE8FQxGQvNaYhldTNlNGDkrbVPBE=',
});

const request = new http.ClientRequest({
    hostname: 'https://api.console.eyowo.com',
    port: 80,
    path: '/v1/users/auth/validate',
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'Content-Length': Buffer.byteLength(body),
        'X-App-Key': '842e87acd5ef90caae15fb7bcdf882e9',
        'X-IV': '62d7d6e0bffa5d475a56f97b423bf368',
    }
});

request.end(body)
```
> Response

```json
{
  "success": true,
  "message": "Please enter the passcode sent to 2349095801772"
}
```

Call this endpoint to initiate and validate user login requests. Requests should be forwarded to the  `/v1/users/auth` 
URL path.

### Request Body.
The request body of the validate user request consists of a single attribute.

Parameter | Type | Required | Description
--------- | ------- | ------ | -----------
mobile | string | true | Any string representation of a valid Nigerian mobile number.
factor | string | true | The login verification method to be used. The currently supported value for this attribute is`sms`.
passcode | string | false | The passcode send to the verification medium of the user. Eyowo passcodes are numeric strings of length `6`.

### Login Initiation Request
To initiate a user login request, call the user login endpoint with the `mobile` and `factor` request attributes.
Upon successful login initiation a passcode will be sent to the user's device via SMS. This passcode will be used in the
login validation step.

### Login Initiation Response
A successful request receives a response with an HTTP 200 status code. The table below describes the response parameters
received from a successful login initiation request. 

Parameter | Type | Description
--------- | ------- | -----------
success | boolean | The unique identifier of the Eyowo user.
message | string | A success message. 

### Login Authorization Request
To authorize a user login request, call the user login endpoint with the `mobile`, `factor`, and `passcode` request
attributes. Upon successful authorization the user will be logged in successfully.

### Login Authorization Response
A successful request receives a response with an HTTP 200 status code. The table below describes the response parameters
received from a successful login initiation request. 

Parameter | Type | Description
--------- | ------- | -----------
success | boolean | The unique identifier of the Eyowo user.
message | string | A success message. 
data | object | A JSON object containing an `accessToken`, `refreshToken` and `expiresIn` attribute - which defining the time in seconds to token expiry. 

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

