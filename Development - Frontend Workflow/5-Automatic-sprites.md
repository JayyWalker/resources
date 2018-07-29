# Automatic Sprites

Configure Gulp to automatically create an Icon Sprite. Make our site load faster for visitors

**1.**
Install svg-sprite package `npm install gulp-svg-sprite@1.3.1 --save-dev`

**2.**
In gulp/tasks create *sprites.js*

```javascript
var gulp = require('gulp');
svgSprite = require('gulp-svg-sprite');

var config = {
  mode: {
    css: {
      render: {
        css: {
          template: './gulp/templates/sprite.css'
        }
      }
    }
  }
}

gulp.task('createSprite', function(){
  return gulp.src('./app/assets/images/icons/**/*.svg')
    .pipe(svgSprite(config))
    .pipe(gulp.dest('./app/temp/sprite/'));
});
```
**3.**
Add to *gulpfile.js*`require('./gulp/tasks/sprites');`

**4.**
Create folder and file *gulp/templates/sprite.css*. In the sprite.css file add the following (moustache template `{`)

```CSS
{{#shapes}}
  .icon--{{base}} {
    width: {{width.outer}}px;
    height: {{height.outer}}px;
    background-image: url('/temp/sprite/css/{{{sprite}}}');
    background-position: {{position.relative.xy}};
  }
{{/shapes}}
```

**5.**
Copy *sprite.css* file to *app/assets/styles/modules/_sprite.css* & Rename file to *_sprite.css* to match existing code

Install rename package `npm install gulp-rename --save-dev`

Edit *sprites.js*

`rename = require('gulp-rename');`

```javascript
gulp.task('copySpriteCSS', ['createSprite'], function(){
  return gulp.src('./app/temp/sprite/css/*.css')
    .pipe(rename('_sprite.css'))
    .pipe(gulp.dest('./app/assets/styles/modules'));
});

gulp.task('icons', ['createSprite', 'copySpriteCSS']);
```

Add to *app/assets/styles/styles.css* `@import "modules/_sprite";`

**6.**
Move svg files from temp folder to assets folder by Editing sprites.js

```javascript
var config = {
  mode: {
    css: {
      sprite: 'sprite.svg',
      render: {
        css: {
          template: './gulp/templates/sprite.css'
        }
      }
    }
  }
}

gulp.task('copySpriteGraphic', ['createSprite'], function(){
  return gulp.src('./app/temp/sprite/css/**/*.svg')
    .pipe(gulp.dest('./app/assets/images/sprites'));
});

gulp.task('icons', ['createSprite','copySpriteGraphic', 'copySpriteCSS']);
```

Edit *sprite.css* to remove repetitive icon urls
```javascript
.icon{
  background-image: url('/assets/images/sprite/{{{sprite}}}');
}

{{#shapes}}
  {{#first}}
    .icon{
      background-image: url('/temp/sprite/css/{{{sprite}}}');
    }
  {{/first}}
  .icon--{{base}} {
    width: {{width.outer}}px;
    height: {{height.outer}}px;
    background-position: {{position.relative.xy}};
  }
{{/shapes}}

```
Use sprite icons in *index.html* `<span class="icon icon--star"></span>`

**7.**
Clean task to delete duplicate .svg files (e.g, if you delete one icon, the new sprite file will not replace the old one and create another version of the .svg file)

Install del package `npm install del --save-dev`

Updating *gulpfile.js* by creating beginClean task and adding it to `icons` task.

```javascript
del = require('del');
gulp.task('beginClean', function(){
  return del(['./app/temp/sprite', './app/assets/images/sprites']);
});
```

**8.**
End the clean task to delete temp sprite folder

```javascript
gulp.task('endClean', ['copySpriteGraphic', 'copySpriteCSS'], function(){
    return del('./app/temp/sprite');
});
```
