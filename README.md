# image-element

Repository to collect best practices for web images

## Respinsive images

### With media

We can use `media` to define a mediaquiery as a breckpoint to load a responsive image.

```html
<picture>
  <source srcset="image-wide.jpg" media="(min-width: 600px)">
  <source srcset="image-ultrawide.jpg" media="(min-width: 1200px)">
  <!-- The <img> tag is a fallback image (required in the <picture> tag) -->
  <img src="image.jpg" height="300" width="200" alt="Awesome image">
</picture>
```

> In the above code, the browser load the `image.jpg` in mobile version, the `image-wide.jpg` in tablets resolutions or bigger, and the `image-ultrawide.jpg` will be loaded in screen resolutions bigger than 1200px.

### With sizes

We can use [`sizes`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/sizes) allows you to specify the layout width of the image for each of a list of media conditions.

```html
<img 
  srcset="image-wide.jpg 600w,
  sizes="(min-width: 600px) 100vw, 600px,
         (min-width: 1200px) 100vw, 1200px"
          image-ultrawide.jpg 1200w"
  src="image.jpg" height="300" width="200" alt="Awesome image">
```

> In the above code (like with `media`), the browser load the `image.jpg` in mobile version, the `image-wide.jpg` in tablets resolutions or bigger, and the `image-ultrawide.jpg` will be loaded in screen resolutions bigger than 1200px.

## Serve a modern image formats

> Usually, the next-gen image format, like [`WebP`](https://developers.google.com/speed/webp), [`AVIF`](https://aomediacodec.github.io/av1-avif/) or [`JPEG XL`](https://jpeg.org/jpegxl/) can optimize image weight while maintaining good image quality.

With the HTML tag `<picture>` we can definte the `type` in the `<source>` tag. The type is the image format, and we can use it to serve modern image formats and the browser will be use the first image format that that can be rendered.

```html
<picture>
  <source type="image/webp" srcset="image.webp">
  <source type="image/jpeg" srcset="image.jpg">
  <!-- The <img> tag is a fallback image (required in the <picture> tag) -->
  <img src="image.jpg" height="300" width="200" alt="Awesome image">
</picture>
```

> In the above code, the browser load the first image format that can render, e.g. the Internet Explorer 11 or Safari 13 can't load the [WebP](https://developers.google.com/speed/webp) image format (a next-gen image format), so they will be load the `JPEG` image. 

```html
<picture>
  <source type="image/jxl" srcset="image.jxl">
  <source type="image/avif" srcset="image.avif">
  <source type="image/webp" srcset="image.webp">
  <source type="image/jpeg" srcset="image.jpg">
  <!-- The <img> tag is a fallback image (required in the <picture> tag) -->
  <img src="image.jpg" height="300" width="200" alt="Awesome image">
</picture>
```

> In the above code, we have all the modern image format, from "more optimized" to "less optimized". The browser will be show the first image that can load and render.

## Serve responsive and modern image formats

We can combine both approaches to serve modern image formats and responsive images to load the better image each device.

```html
<picture>
  <source
    sizes="(min-width: 600px) 100vw, 600px,
           (min-width: 1200px) 100vw, 1200px"
    srcset="image-wide.jpg 600w,
            image-ultrawide.jpg 1200w"
    type="image/jxl">
  <source
    sizes="(min-width: 600px) 100vw, 600px,
           (min-width: 1200px) 100vw, 1200px"
    srcset="image-wide.avif 600w,
            image-ultrawide.avif 1200w"
    type="image/avif">
  <source
    sizes="(min-width: 600px) 100vw, 600px,
           (min-width: 1200px) 100vw, 1200px"
    srcset="image-wide.webp 600w,
            image-ultrawide.webp 1200w"
    type="image/webp">
  <source
    sizes="(min-width: 600px) 100vw, 600px,
           (min-width: 1200px) 100vw, 1200px"
    srcset="image-wide.jpg 600w,
            image-ultrawide.jpg 1200w"
    type="image/jpeg">
  <!-- The <img> tag is a fallback image (required in the <picture> tag) -->
  <img src="image.jpg" height="300" width="200" alt="Awesome image">
</picture>
```
> In the above code, we have a combination of all modern image formats and thw sizes needes (as example, each site or projects needs diferents sizes, of course)

## Improve the Web Performance

To improve the Web Performance, aka **user experince**, we have a few attributes to inprove it.

- [`loading`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/loading) provides a hint to the user agent on how to handle the loading of the image which is currently outside the window's visual viewport. We can define as `eager` (default value) tells the browser to load the image as soon as the `<img>` element is processed, or `lazy` tells the user agent to hold off on loading the image until the browser estimates that it will be needed imminently.
- [`decoding`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/decoding) represents a hint given to the browser on how it should decode the image. The values are `sync` that decode the image synchronously for atomic presentation with other content, `async` to decode the image asynchronously to reduce delay in presenting other content, and `auto` (default mode) which indicates no preference for the decoding mode. The browser decides what is best for the user.
- [`fetchpriority`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/fetchPriority)  represents a hint given to the browser on how it should prioritize the fetch of the image relative to other images. The values are `high` that fetch the image at a high priority relative to other images, `low` to fetch the image at a low priority relative to other images, and `auto` (default mode) which indicates no preference for the fetch priority. The browser decides what is best for the user.

### Now we will use this attributes to improve the user experience of our images

```html
<picture>
  <source
    sizes="(min-width: 600px) 100vw, 600px,
           (min-width: 1200px) 100vw, 1200px"
    srcset="image-wide.jpg 600w,
            image-ultrawide.jpg 1200w"
    type="image/jxl">
  <source
    sizes="(min-width: 600px) 100vw, 600px,
           (min-width: 1200px) 100vw, 1200px"
    srcset="image-wide.avif 600w,
            image-ultrawide.avif 1200w"
    type="image/avif">
  <source
    sizes="(min-width: 600px) 100vw, 600px,
           (min-width: 1200px) 100vw, 1200px"
    srcset="image-wide.webp 600w,
            image-ultrawide.webp 1200w"
    type="image/webp">
  <source
    sizes="(min-width: 600px) 100vw, 600px,
           (min-width: 1200px) 100vw, 1200px"
    srcset="image-wide.jpg 600w,
            image-ultrawide.jpg 1200w"
    type="image/jpeg">
  <!-- The <img> tag is a fallback image (required in the <picture> tag) -->
  <img 
    loading="lazy"
    decoding="async"
    src="image.jpg"
    height="300"
    width="200"
    alt="Awesome image">
</picture>
```

> In the above code, we have a better code for all the images below the fold (outside the viewport) and the browser does not load these images (according to the [threshold](https://github.com/chromium/chromium/blob/main/third_party/blink/renderer/core/frame/settings.json5#L936-L968))

### Improve the image detected as [LCP](https://web.dev/lcp) element of the Core Web Vitals

The previous code cover the scenario for all images out off viewport. Usualy the [LCP](https://web.dev/lcp) metric is on about an image element, so we can iterate to improve it.

```html
<picture>
  <source
    sizes="(min-width: 600px) 100vw, 600px,
           (min-width: 1200px) 100vw, 1200px"
    srcset="image-wide.jpg 600w,
            image-ultrawide.jpg 1200w"
    type="image/jxl">
  <source
    sizes="(min-width: 600px) 100vw, 600px,
           (min-width: 1200px) 100vw, 1200px"
    srcset="image-wide.avif 600w,
            image-ultrawide.avif 1200w"
    type="image/avif">
  <source
    sizes="(min-width: 600px) 100vw, 600px,
           (min-width: 1200px) 100vw, 1200px"
    srcset="image-wide.webp 600w,
            image-ultrawide.webp 1200w"
    type="image/webp">
  <source
    sizes="(min-width: 600px) 100vw, 600px,
           (min-width: 1200px) 100vw, 1200px"
    srcset="image-wide.jpg 600w,
            image-ultrawide.jpg 1200w"
    type="image/jpeg">
  <!-- The <img> tag is a fallback image (required in the <picture> tag) -->
  <img 
    fetchpriority="high"
    decoding="sync"
    src="image.jpg"
    height="300"
    width="200"
    alt="Awesome image">
</picture>
```

> In the above code, we changed the attribute `decoding` to `sync` to priorice the decoding, removed the attribut `loading` becaouse the default behavior is `eager`, so we don't needed, and we add the attribute `fetchpriority="high"` to indicate to the browser that load the image soon as possible.

> Btw, we don need to add these attribute to all `<source>` tags, we need to add in `<img>` tag only.

## Use a CDN Image Service

We see that we need a lot of code to have the better option to improve the user experience 🙈.

We can use a CDN Image Service, like [Cloudinary](https://cloudinary.com/), to remove the part of code reference to image type because this service serve the better image supported by the browser.

The browser send in the [HTTP Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers) the [`accept`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept) header value to indicates which content types, expressed as [MIME types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types).

![Accept Headder](images/accept.png)

> In the screenshot we can see that my current version browser supports `image/avif,image/webp,image/apng,image/svg+xml,image/*,*/*;`, so with a service of automatic image format, the service will send me an `avif` image format to render in the browser.

```html
<picture>
  <img 
    sizes="(min-width: 600px) 100vw, 600px,
           (min-width: 1200px) 100vw, 1200px"
    srcset="
      https://res.cloudinary.com/nucliweb/image/upload/c_scale,f_auto,w_600/v1010101010/demo/image.png 600px,
      https://res.cloudinary.com/nucliweb/image/upload/c_scale,f_auto,w_1200/v1010101010/demo/image.png 1200px"
    src="https://res.cloudinary.com/nucliweb/image/upload/f_auto/v1010101010/demo/image.png"
    loading="lazy"
    decoding="async"
    height="300"
    width="200"
    alt="Awesome image">
</picture>
```

> Now we don't need to define the type because this is transparent for us, the service sends the best image format supported by the browser. Pay attention that the image in the samples is an `PNG` image, but the browser will load an `avif` image format.

<hr>

## Acknowledgment

- [Addy Osmani](https://github.com/addyosmani), for this [image](images/image-addy-osmani.jpg) and for all the tips that he are sharing with the community.
