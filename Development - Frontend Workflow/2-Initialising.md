# Initialising a new project

**1.**
CD into the project folder and run `npm init`. This sets up NPM for the project, and creates *package.json*, which will store config info on the packages used in the project.

**2.**
To install jquery run `npm install jquery --save`.
(If node modules get deleted or outdated, run `npm install` to get fresh version of packages listed in package.json)

**3.**
Install gulp cli. `npm install gulp-cli -global`.
Run `gulp -v` to check CLI version.

**4.**
Install gulp package in your project. `npm install gulp --save-dev`

**5.**
Create *gulpfile.js* in project root `touch gulpfile.js `. Add placeholder tasks to the file:

```javascript
var gulp = require(‘gulp’);

	gulp.task('default', function() {
  		console.log("Yay, Gulp default task");
	});

	gulp.task(‘html’, function() {
		console.log(“Woohoo!! html task”);
	});

	gulp.task(‘styles’, function() {
		console.log(“Yippee..styles task”);
	});
```

**6.**
Install the gulp-watch package `npm install gulp-watch --save-dev`

add to *gulpfile.js*:

```javascript
watch = require('gulp-watch');

gulp.task('watch', function() {
  watch('./app/index.html',
    function(){
      gulp.start('html');
    });
});
```

**7.**
Set up **post-css** with **autoprefixer** (automatic webkit prefixes to ensure browser css compatibility); **simple-vars** (use variables in css); **nested** (nesting selectors in css) and **import** (write modular css across different files).

```javascript
npm install gulp-postcss --save-dev
npm install autoprefixer --save-dev
npm install postcss-simple-vars --save-dev
npm install postcss-nested --save-dev
npm install postcss-import --save-dev
```

add to *gulpfile.js*:
```javascript
postcss = require('gulp-postcss'),
autoprefixer = require(‘autoprefixer’),
cssvars = require('postcss-simple-vars'),
nested = require('postcss-nested'),
cssImport = require('postcss-import');

gulp.task('styles', function() {
  return gulp.src('app/assets/styles/styles.css')
    .pipe(postcss([cssImport, cssvars, nested, autoprefixer]))
    .pipe(gulp.dest('app/temp/styles'));
});
```
**8.**
Adding stylesheet to *app/index.html*:

```
<link rel="stylesheet" href="temp/styles/styles.css">
```

**9.**
CSS Architecture - Modular CSS
````
|-app
	index.html
		|- assets
			|-fonts
			|-images
			|-styles
				styles.css
				|-base
					_global.css
				|-modules
					_header.css
					_footer.css

````

**10.**
Import css modules in *styles.css*

```
@import “base/_global.css”;
@import “modules/_footer.css”;

```

## BrowserSync
Update gulp to auto-refresh the web browser whenever there is a change html/css.

**1.**
Gulp watch `npm install gulp-watch --save-dev`

**2.**
BrowserSync package `npm install browser-sync --save-dev`

**3.**
Update *gulpfile.js*
```javascript
var watch = require('gulp-watch'),
browserSync = require('browser-sync').create();
```

Update the watch task:
```javascript
gulp.task('watch', function() {

  browserSync.init({
    server: {
      baseDir: "app"
    }
  });

  watch('./app/index.html', function() {
    browserSync.reload();
  });

  watch('./app/assets/styles/**/*.css', function() {
    gulp.start(‘cssInject’);
  });
});
```
Adding cssinject task to *gulpfile.js*:

```javascript
gulp.task('cssInject', ['styles'], function() {
  return gulp.src('app/temp/styles/**/*.css')
    .pipe(browserSync.stream());
});
```
