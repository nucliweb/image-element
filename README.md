# image-element

Repository to collect best practices for web images

## Respinsive images

### With media

You can use `media` to define a mediaquiery as a breckpoint to load a responsive image.

```html
<picture>
  <source srcset="image-wide.jpg" media="(min-width: 600px)">
  <source srcset="image-ultrawide.jpg" media="(min-width: 1200px)">
  <!-- The <img> tag is a fallback image (required in the <picture> tag) -->
  <img src="image.jpg" height="600" width="400" alt="Awesome image">
</picture>
```

> In the above code, the browser load the `image.jpg` in mobile version, the `image-wide.jpg` in tablets resolutions or bigger, and the `image-ultrawide.jpg` will be loaded in screen resolutions bigger than 1200px.

<hr>

## Acknowledgment

- [Addy Osmani](https://github.com/addyosmani), for this [image](images/image-assy-ormani.jpg) and for all the tips that he are sharing with the community.