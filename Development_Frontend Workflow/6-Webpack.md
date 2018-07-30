# Webpack

Blueprint in JavaScript (classes in other OOP languages). ECMA5 way of creating "classes". Later, after installing Babel, we can use the ECMA6 class constructor.

```javascript
function Person(fullName, profession) {
this.name = fullName;
this.profession = profession;
this.greet = function() {
	console.log("Hi, my name is " + this.name + " and I am a " + this.profession " .");
	}
}
```

**1.**
Create: app/assets/scripts/App.js app/assets/scripts/modules/

Modules (e.g. Person.js) will go in the modules/ folder. Then, require them at the top of App.js e.g.
`var Person = require(‘./modules/Person’);`

Webpack will compile all the js modules into a single file that the browser can then read.

**2.** Install webpack globally `npm install webpack -g`

**3.** Create *webpack.config.js* in the project root folder

```javascript
module.exports = {
		 entry: __dirname + "/app/assets/scripts/App.js",
		 output: {
		 path: __dirname + "/app/temp/scripts",
		 filename: "App.js"
	 }
}
```

**4.** Run 'webpack' in node.js command prompt

**5.** Update path to script file in index.html to point to assets/temp/scripts/App.js

Each js module (e.g. Person.js) will need an export line at the end, so that Webpack knows what to do with it.
`module.exports = Person;`

**6.** Webpack can also require third-party modules such as jquery.
If using jquery in project, first install it with `npm install jquery --save`. Then, in each module that uses jquery, at the top put `var $ = require('jquery');`


## Integrate Webpack in Gulp Automation  

Browsersync will automatically update if a .js file is edited:

**1.** Install webpack locally `npm install webpack --save-dev`

**2.** Create *gulp/tasks/scripts.js*

**3.** Edit *gulpfile.js* by adding `require(‘./gulp/tasks/scripts’);`

**4.** Add the following to *gulp/tasks/scripts.js*

```javascript
var gulp = require(‘gulp’),
webpack = require(‘webpack’);

gulp.task('scripts', function(callback) {
	webpack(require('../../webpack.config.js'), function(err, stats) {
		if (err) {
			console.log(err.toString());
		}
		console.log(stats.toString());
		callback();

	});
});
```

**5.** In watch.js, after 'css' and 'watch' tasks, add:

```javascript
watch('./app/assets/scripts/**/*.js'), function() {
	gulp.start('scriptsRefresh');
})

gulp.task('scriptsRefresh', ['scripts'], function() {
	browserSync.reload();
)};
```
