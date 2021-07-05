# monaco-editor-locale
localization with esm

Use copy-webpack-plugin to copy the files of monaco-editor/min/vs into your project‘s build directory  in your webpack.config.js

```js

  const copyWebpackPlugin=reuqire('copy-webpack-plugin');

  model.exports={
    plugin:[
      new copyWebpackPlugin({
        patterns: [
          {
            from: 'node_modules/monaco-editor/min/vs',
            to: 'vs',
          },
        ],
      })
    ]
  }
```

put the monaco-editor's loader into your project's index.html

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>monaco-editor</title>
    <script src="/vs/loader.js"></script>
  </head>
  <body>
  </body>
</html>

```

follow the offical [demo](https://github.com/microsoft/monaco-editor-samples/blob/main/browser-amd-localized/index.html)

```javascript

			window.require.config({
        paths: { vs: '../node_modules/monaco-editor/min/vs' }
				'vs/nls': {
					availableLanguages: {
						'*': 'de'
					}
				}
			});

			window.require(['vs/editor/editor.main'], function () {
				var editor = monaco.editor.create(document.getElementById('container'), {
					value: ['function x() {', '\tconsole.log("Hello world!");', '}'].join('\n'),
					language: 'javascript'
				});
			});
```
use window.require not require to avoid webpack compile the require
