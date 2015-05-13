[![NPM version](https://badge.fury.io/js/dustify.svg)](http://badge.fury.io/js/dustify)

# dustify

Browserify plugin to convert [Dust.js] templates to Javascript. This is a distant fork of [dustjs-browserify](https://github.com/scottbrady/dustjs-browserify).

## Supports dust partials in the browser

This module performs static analysis to detect and browserify templates included using the dust partials syntax. If your script includes a template with a partial:

```
<p>hello</p>p>
{>"some/template"/}
```

## Installation

```
npm install dustify
```

## Example using callbacks

```javascript
{
  ...
  "browserify": {
    "transform": [
      ["dustify", {"path": "lib/templates"}]
    ]
  }
}
```

```javascript
var template = require('./template.dust');

template({ foo : 42 }, function (err, html) {
  if (err) { ... }
  ...
});
```

## Example using a promise library

Please note that `dustify` **does not** install any promise library of its own. It's expected that you install it yourself.

```javascript
{
  ...
  "browserify": {
    "transform": [
      [
        "dustify",
        {
          "path"     : "lib/templates",
          "promises" : "bluebird"
        }
      ]
    ]
  },
  ...
  "dependencies": {
    "bluebird": "*"
  }
}
```

You can also use ES6 promises provided by the browser:

```javascript
{
  ...
  "browserify": {
    "transform": [
      [
        "dustify",
        {
          "path"     : "lib/templates",
          "promises" : true
        }
      ]
    ]
  }
}
```

```javascript
var template = require('./template.dust');

template({ foo : 42 })
  .then(function (html) {
    ...
  })
  .catch(function (error) {
    ...
  });
```

Both of these examples will work on the server and in the browser.

## Dust.js documentation

* [Dust Tutorial](https://github.com/linkedin/dustjs/wiki/Dust-Tutorial)
* [Dust little less know language constructs](https://github.com/linkedin/dustjs/wiki/Dust-little-less-know-language-constructs)
* [Demo of using template engines with express.js and node.js](https://github.com/chovy/express-template-demo)
* [Original Dustjs project by akdubya](http://akdubya.github.io/dustjs/)

## Security

* [Add additional security filters to Dustjs](https://github.com/linkedin/dustjs-filters-secure)

## License

MIT

[Dust.js]: http://www.dustjs.com