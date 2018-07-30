# Post-css mixins

Media queries for mobile responsiveness.
Start css with a mobile-first approach by adding baseline smallest screen size then add mixin mediaqueries for progressively larger screens.

**1.**
Install mixin package
```
npm install postcss-mixins --save-dev
```

Edit partial *gulpfile.js* i.e, *gulp/tasks/styles.js*:
`mixins = require('postcss-mixins');`

and update pipe in same file:
`.pipe(postcss([cssImport, mixins, cssvars, nested, autoprefixer]))`

**2.**
Create reusable mixin blocks in file *app/assets/styles/base/_mixins.css*
```CSS
@define-mixin atSmall {
  @media (min-width: 530px) {
    @mixin-content;
  }
}

@define-mixin atMedium {
  @media (min-width: 800px) {
    @mixin-content;
  }
}

@define-mixin atLarge {
  @media (min-width: 1200px) {
    @mixin-content;
  }
}
```

Import this file in *styles.css* `@import “base/_mixins.css”;`

**3.**
We can now use `@mixin [mixinName]` in stylesheets. Nest in selectors as follows:

```javascript
.row{


	@mixin atMedium{
		  &__medium-4{
			    float: left;
			    width: 33.33%;
		  }

		  &__medium-8{
			    float: left;
			    width: 66.66%;
		  }
	}

}

```
