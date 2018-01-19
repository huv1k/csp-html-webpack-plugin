# CSP HTML Webpack Plugin

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/slackhq/csp-html-webpack-plugin/blob/master/LICENSE)
[![npm](https://img.shields.io/npm/v/csp-html-webpack-plugin.svg)](https://www.npmjs.com/package/csp-html-webpack-plugin)
[![Code Style](https://img.shields.io/badge/code%20style-prettier-brightgreen.svg)](https://github.com/prettier/prettier)
[![Build Status](https://travis-ci.org/slackhq/csp-html-webpack-plugin.svg?branch=master)](https://travis-ci.org/slackhq/csp-html-webpack-plugin)
[![codecov](https://codecov.io/gh/slackhq/csp-html-webpack-plugin/branch/master/graph/badge.svg?token=cBemDmnz85)](https://codecov.io/gh/slackhq/csp-html-webpack-plugin)

## About

This plugin will generate meta content for your Content Security Policy tag and input the correct data into your HTML template, generated by [html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin/).

All inline JS and CSS will be hashed, including all entry and async chunks, and inserted into the policy.


## Installation

Install the plugin with npm:
```
npm i --save-dev csp-html-webpack-plugin
```

## Basic Usage

In the plugins section of your webpack config file, include the following:

```
new HtmlWebpackPlugin()
new CspHtmlWebpackPlugin()
```

Finally, add the following tag to your HTML template where you would like to add the CSP policy:
```
<meta http-equiv="Content-Security-Policy" content="%%CSP_POLICY%%">
```

## Configuration

This `CspHtmlWebpackPlugin` accepts 2 params with the following structure:
* `{object}` Policy (optional) - a flat object which defines your CSP policy. Valid keys and values can be found on the [MDN CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) page. Values can either be a string or an array of strings.
* `{object}` Additional Options (optional) - a flat object with the optional configuration options:
  * `{string}` hashingMethod - accepts 'sha256', 'sha384', 'sha512' - your node version must also accept this hashing method.

This plugin also adds another option to the `HtmlWebpackPlugin`
* `{RegExp}` cspAssetRegex (optional) - if defined, only assets which match the regex will be hashed and added to the policy. Dependencies of these assets will also be added to the policy regardless of whether they match the regex or not.
  * Note: If you are using a manifest plugin, you should make sure your manifest asset is matched in this regex as well

#### Default Policy:

```
{
  'base-uri': "'self'",
  'object-src': "'none'",
  'script-src': ["'unsafe-inline'", "'self'", "'unsafe-eval'"],
  'style-src': ["'unsafe-inline'", "'self'", "'unsafe-eval'"]
};
```

#### Default Additional Options:

```
{
  hashingMethod: 'sha256'
}
```

#### Full Configuration with all options:
```
new HtmlWebpackPlugin({
  cspAssetRegex: /some-regex-here/
}),

new CspHtmlWebpackPlugin({
  'base-uri': "'self'",
  'object-src': "'none'",
  'script-src': ["'unsafe-inline'", "'self'", "'unsafe-eval'"],
  'style-src': ["'unsafe-inline'", "'self'", "'unsafe-eval'"]
}, {
  hashingMethod: 'sha256'
})
```

## Contribution

Contributions are most welcome! Please see the included contributing file for more information.

## License

This project is licensed under MIT. Please see the included license file for more information.
