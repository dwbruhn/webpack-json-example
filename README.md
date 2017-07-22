# json-loader parsing issue: U+2028 & U+2029

cf. https://github.com/webpack-contrib/json-loader/issues/50

Webpack's [json-loader dependency](https://github.com/webpack-contrib/json-loader) can't handle [U+2028 LINE SEPARATOR](http://www.fileformat.info/info/unicode/char/2028/index.htm) or [U+2029 PARAGRAPH SEPARATOR](http://www.fileformat.info/info/unicode/char/2029/index.htm) in JSON file, which are [valid characters in JSON strings](http://timelessrepo.com/json-isnt-a-javascript-subset):

```bash
$ npm run build

> webpack-json-example@1.0.0 build /Users/dbruhn/repos/webpack-json-example
> webpack ./index.js bundle.js

Hash: 51929351b6ec03c09e7d
Version: webpack 3.3.0
Time: 73ms
    Asset     Size  Chunks             Chunk Names
bundle.js  3.27 kB       0  [emitted]  main
   [0] ./index.js 122 bytes {0} [built]
   [1] ./lineSep.json 271 bytes {0} [built] [failed] [1 error]
   [2] ./paraSep.json 276 bytes {0} [built] [failed] [1 error]

ERROR in ./lineSep.json
Module parse failed: /Users/dbruhn/repos/webpack-json-example/lineSep.json Unterminated string constant (2:37)
You may need an appropriate loader to handle this file type.
| module.exports = {
| 	"value_with_line_separator_U+2028": "A B"
| };
 @ ./index.js 2:13-38

ERROR in ./paraSep.json
Module parse failed: /Users/dbruhn/repos/webpack-json-example/paraSep.json Unterminated string constant (2:42)
You may need an appropriate loader to handle this file type.
| module.exports = {
| 	"value_with_paragraph_separator_U+2029": "A B"
| };
 @ ./index.js 3:13-38
```

## Update

[Already fixed](https://github.com/webpack-contrib/json-loader/commit/3b3069fa3f9deb35cc625c6c388e234a240ee312) and [now published](https://www.npmjs.com/package/json-loader)!
