# Migration from `sp-request` 2.x to 3.x

`sp-request` 3.x uses [got](https://github.com/sindresorhus/got/) instead of [request-promise](https://github.com/request/request-promise/) (deprecated).

In most cases it has exactly the same API. However, some configuration options are different.

Please refer to the table below to see what have changed:

| old options property (request-promise) | new property (got) |
|--------------|--------------|
| `simple: true` | `throwHttpErrors: true` |
| `strictSSL: false` | `rejectUnauthorized: false`|
| `json: true` | `responseType: 'json'` |
|`resolveWithFullResponse: true`|`resolveBodyOnly: false`|
If you use any of the properties in the left column, you should use right equivalent instead in your code.

For example, your old 2.x code for `sp-request` might look like:

```javascript
spr.post("https://sharepoint.url", {
  json: true,
  body: {
    "Title": "hello world"
  },
  resolveWithFullResponse: false,
  simple: false
});
```

To have it in 3.x version, you should change as below:

```javascript
spr.post("https://sharepoint.url", {
  responseType: 'json'
  body: {
    "Title": "hello world"
  },
  resolveBodyOnly: true,
  simple: false,
  throwHttpErrors: false
});
```