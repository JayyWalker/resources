# Babel

Babel enables us to write ES6 code, which it then converts to ES5 code to ensure browser compatibility.

**1.** Install Babel packages `npm install babel-core babel-loader babel-preset-es2015 --save-dev`

**2.** Edit *webpack.config.js* so the whole thing reads as follows. Webpack will run the code through Babel before creating the dist version of App.js.

```javascript
module.exports = {
	entry: "./app/assets/scripts/App.js",
	output: {
		path: "./app/temp/scripts",
		filename: "App.js"
		},
		modules: {
			loaders: [
				{
					loader: 'babel',
					query: {
						presets: ['es2015']
					},
					test: /\.js$/,
					exclude: /node_modules/
					}
				]
			}
}
```
## ECMA6 refactor - imports / exports

Additionally, as ECMA6 supports importing from external .js files, in *App.js* we can replace

`var Person = require(‘./modules/Person’);` with `import Person from ‘./modules/Person’;`

and in *Person.js* replace

`module.exports = Person;` with `export default Person;`
