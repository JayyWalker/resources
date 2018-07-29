
## Responsive Images
We use responsive images for two reasons:
1. Art direction (Using differently-cropped images depending on screen size.)
2. File size / resolution (Images with resolution/size appropriate to the user's screen are downloaded)

**1. "Art direction"**
Use the `<picture>` tag with media attribute:
```
<picture>
	<source srcset=“images/dog-crop-large.jpg” media=“(min-width: 1200px)”>
	<source srcset=“images/dog-crop-medium.jpg” media=“(min-width: 760px)”>
	<img src=“images/dog-crop-small.jpg” alt=“Puppy in the sand.”>
</picture>
```

**2. Image resolution / file size**
Use `srcset`. The number after each image denotes the width of the image The browser/device uses this to determine which is the most appropriate to download, and doesn’t download the alternatives.
```
<img srcset=“images/dog-res-small.jpg 570w, images/dog-res-medium.jpg 1200w, images/dog-res-large.jpg 1920w” alt=“Puppy in the sand”>
```
