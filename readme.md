# webext-dynamic-content-scripts [![Travis build status](https://api.travis-ci.org/bfred-it/webext-dynamic-content-scripts.svg?branch=master)](https://travis-ci.org/bfred-it/webext-dynamic-content-scripts) [![npm version](https://img.shields.io/npm/v/webext-dynamic-content-scripts.svg)](https://www.npmjs.com/package/webext-dynamic-content-scripts)

> Automatically inject your `content_scripts` on custom domains.

This is useful when you add extra domains via `chrome.permission`. For example [to support GitHub Enterprise](https://github.com/npmhub/npmhub/issues/29)

## Install

```sh
npm install --save webext-dynamic-content-scripts
```

## Usage

<details><summary>
### Plain files
</summary>

1. In your `manifest.json`, include the file as background and as content script:

	```js
	{
		"background": {
			"scripts": [
				"dist/webext-dynamic-content-scripts.js"
			]
		},
		"content_scripts": [
			{
				"js": [
					"dist/webext-dynamic-content-scripts.js",
					"content.js"
				]
			}
		]
	}
	```

</details>

2. In your background script **only**, run `dynamicContentScripts()`

### With a bundler

```js
// background.js
import dynamicContentScripts from 'webext-dynamic-content-scripts';
```

```js
// content.js
import 'webext-dynamic-content-scripts'; // needed to make sure that scripts aren't loaded twice
```

## API

#### dynamicContentScripts([tab])

This will inject all the `content_scripts` and their CSS files listed in `manifest.json`.

If `tab` is not specified, `dynamicContentScripts()` will automatically listen to new tabs and inject the scripts as needed.

##### tab

Type: `Tab` or `number` or `undefined`

A `Tab` object or just its `id` as defined here: https://developer.chrome.com/extensions/tabs#type-Tab

## Related

* [`webext-content-script-ping`](https://github.com/bfred-it/webext-content-script-ping): One-file interface to detect whether your content script have loaded.
* [`webext-options-sync`](https://github.com/bfred-it/webext-options-sync): Helps you manage and autosave your extension's options.
* [`webext-inject-on-install`](https://github.com/bfred-it/webext-inject-on-install): Automatically add content scripts to existing tabs when your extension is installed.
* [`Awesome WebExtensions`](https://github.com/bfred-it/Awesome-WebExtensions): A curated list of awesome resources for Web Extensions development.

## License

MIT © Federico Brigante — [Twitter](http://twitter.com/bfred_it)
