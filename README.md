# webpack-json-example

cf. https://github.com/webpack-contrib/json-loader/issues/50

Webpack (or json-loader dependency?) can't handle [U+2028 LINE SEPARATOR](http://www.fileformat.info/info/unicode/char/2028/index.htm) in JSON file, which is [a valid character in JSON strings](http://timelessrepo.com/json-isnt-a-javascript-subset):

```bash
$ npm run build

> webpack-json-example@1.0.0 build /Users/dbruhn/repos/webpack-json-example
> webpack ./index.js bundle.js

Hash: e9dbec11b587d5d18459
Version: webpack 3.3.0
Time: 71ms
    Asset     Size  Chunks             Chunk Names
bundle.js  2.89 kB       0  [emitted]  main
   [0] ./index.js 73 bytes {0} [built]
   [1] ./lineSep.json 271 bytes {0} [built] [failed] [1 error]

ERROR in ./lineSep.json
Module parse failed: /Users/dbruhn/repos/webpack-json-example/lineSep.json Unterminated string constant (2:37)
You may need an appropriate loader to handle this file type.
| module.exports = {
| 	"value_with_line_separator_U+2028": "A B"
| };
 @ ./index.js 2:12-37
```
