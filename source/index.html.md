---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python

toc_footers:
  - <a href='http://data.nhm.ac.uk'>The Data Portal</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Data Portal API docs!

The Natural History Museum in London, UK shares a wealth of its research data via the [Data Portal](http://data.nhm.ac.uk) website. The API provides a RESTful interface to this information.

Please feel free to [contact us](http://data.nhm.ac.uk/contact) if you have any questions!

# Basics

## Access

> We do not currently have any packages providing an easy syntax for accessing the API; access is just via URLs.

```python
import requests

base_url = 'http://data.nhm.ac.uk/api/3'
```

The base URL for the API is `http://data.nhm.ac.uk/api/3`.

Use of the Data Portal API does not currently require a key or any kind of authentication.

<aside class="notice">
Please use common sense when using the API, and cache results wherever possible. We reserve the right to suspend API access if you continuously make multiple calls per second.
</aside>

## Results

> A basic successful result looks like this:

```json
{
  "help": "A description of the action.",
  "success": true,
  "result": ["item1", "item2"]
}
```

> An unsuccessful result looks like this:

```json
{
  "help": "A description of the action.",
  "success": false,
  "error": {
    "message": "This is what you did wrong.",
    "__type": "ErrorType"
  }
}
```

Results are returned in JSON format, with two basic keys: `help` (which describes the action called) and `success` (a boolean indicating whether the request was successful or not).

If the request was successful, the items will be returned under the `result` key.

If the action was valid but the parameters were not, you will get `success: false` and an error message.

# Datasets

## List datasets

```python
requests.get(base_url)
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
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

Datasets are sometimes also referred to as _packages_.

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

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
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
