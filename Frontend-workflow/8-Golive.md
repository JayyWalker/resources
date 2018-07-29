
## Preparing files to go live

**1.** create *dist* folder

**2.** Install imagemin for image compression
`npm install gulp-imagemin --save-dev`

Install del so we can delete old files when creating a new build
`npm install del --save-dev`

**3.** create *gulp/tasks/build.js*

#### Process images

**1.** Add following to *gulp/tasks/build.js*

```
var gulp = require('gulp'),
imagemin = require('gulp-imagemin');

gulp.task('optimizeImages', function() {
  return gulp.src("./app/assets/images/**/*")
  .pipe(imagemin({
    progressive: true,
    interlaced: true,
    multipass: true
  }))

  .pipe(gulp.dest("./dist/assets/images"));
});

gulp.task('build', ['optimizeImages']);
```

**2.** In *gulpfile.js* add `require(‘./gulp/tasks/build’);

**3.** Add 'deleteDistFolder' task to *build.js* to clear out dist folder before each new build

```
var gulp = require('gulp'),
imagemin = require('gulp-imagemin'),
del = require('del'); //so we can delete the dist folder at start of each build

gulp.task('deleteDistFolder', function() {
  return del("./dist");
});

gulp.task('optimizeImages', ['deleteDistFolder'], function() {
  return gulp.src("./app/assets/images/**/*")
  .pipe(imagemin({
    progressive: true,
    interlaced: true,
    multipass: true
  }))

  .pipe(gulp.dest("./dist/assets/images"));
});

gulp.task('build', ['deleteDistFolder', 'optimizeImages']);

```
N.B. 'deleteDistFolder' has been added as a dependency in the last line.

#### Process CSS and Javascript with Usemin
We want to
-copy to dist folder
-compress
-revision (make unique filename that forces browsers that have cached our page to d/load new versions)

**1.** `npm install gulp-usemin —save-dev`

**2.** add to *build.js* so it looks like following:
```
var gulp = require('gulp'),
imagemin = require('gulp-imagemin'),
del = require('del'), //so we can delete the dist folder at start of each build
usemin = require('gulp-usemin');

gulp.task('deleteDistFolder', function() {
  return del("./dist");
});

gulp.task('optimizeImages', ['deleteDistFolder'], function() {
  return gulp.src("./app/assets/images/**/*")
  .pipe(imagemin({
    progressive: true,
    interlaced: true,
    multipass: true
  }))

  .pipe(gulp.dest("./dist/assets/images"));
});

gulp.task('usemin', ['deleteDistFolder'], function() {
  return gulp.src("./app/index.html")
  .pipe(usemin())
  .pipe(gulp.dest("./dist"));
});

gulp.task('build', ['deleteDistFolder', 'optimizeImages', 'usemin']);
```

**3.** So that the dist version of *index.html* points to the correct, dynamically-named versions of the CSS and JS files, wrap the references in comments as follows:
```
<!-- build:css assets/styles/styles.css -->
<link rel="stylesheet" href="temp/styles/styles.css">
<!-- endbuild -->
```
```
<!-- build:js assets/scripts/App.js -->
<script src="assets/scripts/App.js"></script>
<!-- endbuild -->
```

**4.** run `gulp build`
this will create index.html in dist folder with usemin comments removed, and create script and css files in appropriate dist subfolders.

#### Compression and versioning

**1.** `npm install gulp-rev gulp-cssnano gulp-uglify --save-dev`
(gulp-rev revisions files; gulp-cssnano compresses css; gulp-uglify compresses javascript)

**2.** at top of *build.js* add:
```
rev = require('gulp-rev'),
cssnano = require('gulp-cssnano'),
uglify = require('gulp-uglify');
```

**3.** Update 'usemin' task:
```
gulp.task('usemin', ['deleteDistFolder'], function() {
  return gulp.src("./app/index.html")
  .pipe(usemin({
    css: [function() {return rev()}, function() {return cssnano()}],
    js: [function() {return rev()}, function() {return uglify()}]
  }))
  .pipe(gulp.dest("./dist"));
});
```
NB If you're using ECMA6 syntax (e.g. arrow functions) in your JS and are not using Babel, uglify will throw an error.

**4.** Add a previewDist task to *build.js* that will let us preview our dist files using Browsersync:

```
var gulp = require('gulp'),
imagemin = require('gulp-imagemin'),
del = require('del'), //so we can delete the dist folder at start of each build
usemin = require('gulp-usemin'),
rev = require('gulp-rev'),
cssnano = require('gulp-cssnano'),
uglify = require('gulp-uglify'),
browserSync = require('browser-sync').create();

gulp.task('previewDist', function() {
  browserSync.init({
    notify: false,
    server: {
      baseDir: "dist"
    }
  });
});
gulp.task('deleteDistFolder', function() {
  return del("./dist");
});

gulp.task('optimizeImages', ['deleteDistFolder'], function() {
  return gulp.src("./app/assets/images/**/*")
  .pipe(imagemin({
    progressive: true,
    interlaced: true,
    multipass: true
  }))

  .pipe(gulp.dest("./dist/assets/images"));
});

gulp.task('usemin', ['deleteDistFolder', 'styles'], function() {
  return gulp.src("./app/index.html")
  .pipe(usemin({
    css: [function() {return rev()}, function() {return cssnano()}],
    js: [function() {return rev()}]
  }))
  .pipe(gulp.dest("./dist"));
});

gulp.task('build', ['deleteDistFolder', 'optimizeImages', 'usemin']);
```
note that  styles was added as a dependency of usemin. if we had a scripts task, as in the original tutorial, this would also be added as a dependency here.

#### Copying other files to our dist folder with build
**1.**
Add the following to *build.js*:
```
gulp.task('copyGeneralFiles', ['deleteDistFolder'], function(){
  var pathsToCopy = [
    './app/**/*',
    '!./app/index.html',
    '!./app/assets/images/**',
    '!./app/assets/styles/**',
    '!./app/assets/scripts/**',
    '!./app/temp',
    '!./app/temp/**'
  ]

  return gulp.src(pathsToCopy)
  .pipe(gulp.dest("./dist"));
});
```
**2.**
Update build task at end of same file:
```
gulp.task('build', ['deleteDistFolder', 'copyGeneralFiles', 'optimizeImages', 'usemin']);
```
