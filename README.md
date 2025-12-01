# autosizes

Automatic `sizes` attribute calculation for responsive images.

This library automatically calculates and sets the `sizes` attribute for responsive images based on the actual rendered width of the image
element.

> **Note:** This is not an original library. It is extracted from [lazysizes](https://github.com/aFarkas/lazysizes) with functionality
> limited to automatic `sizes` calculation only. All lazy loading features have been removed to create a lightweight, focused solution (~2.6KB
> vs 7.8KB).

## Features

- 🎯 Automatic calculation of `sizes` attribute
- 📦 Tiny size (2.6KB minified)
- 🚀 High performance with RAF batching
- 🖼️ Smart `<picture>` element support - only `<img>` needs the class
- 🔄 Auto-updates on resize
- 🎨 Customizable via events and CSS classes
- 📱 Works with any responsive image setup
- ✨ Adds class to processed elements for easy styling

## Installation

```bash
npm install autosizes
```

### Import Methods

```javascript
// ES modules (auto-executes)
import 'autosizes';

// CommonJS
require('autosizes');

// Or with explicit import
import autoSizes from 'autosizes';
// Now you can use: autoSizes.init(), autoSizes.updateAll(), etc.
```

### Browser (script tag)

```html
<script src="autosizes.min.js"></script>
<!-- or from CDN when published -->
```

## Usage

### Basic Usage

```html
<img
  class="autosizes"
  sizes="auto"
  srcset="image-300.jpg 300w, image-600.jpg 600w, image-900.jpg 900w"
  src="image-300.jpg"
  alt="Responsive image"
/>

<script src="autosizes.js"></script>
```

The library will automatically:

1. Find elements with class `autosizes` and `sizes="auto"`
2. Calculate the correct `sizes` value based on rendered width
3. Update the `sizes` attribute (e.g., `sizes="450px"`)
4. Add the `autosized` class to mark it as processed

### With Picture Element

When using `<picture>` elements, you only need to add the `autosizes` class to the `<img>` element. All `<source>` and `<img>` elements with
`sizes="auto"` inside the same `<picture>` will be automatically updated:

```html
<picture>
  <source
    sizes="auto"
    srcset="image-300.jpg 300w, image-600.jpg 600w"
    media="(max-width: 600px)"
  />
  <source
    sizes="auto"
    srcset="image-600.jpg 600w, image-900.jpg 900w"
    media="(min-width: 601px)"
  />
  <img
    class="autosizes"
    sizes="auto"
    srcset="image-900.jpg 900w, image-1200.jpg 1200w"
    src="image-900.jpg"
    alt="Art directed image"
  />
</picture>
```

**Note:** Sources without `sizes="auto"` will not be modified, allowing you to have mixed automatic and manual sizing in the same picture.

### Result After Processing

**Simple image:**

```html
<!-- Before -->
<img class="autosizes" sizes="auto" srcset="..." />

<!-- After -->
<img class="autosizes autosized" sizes="450px" srcset="..." />
```

**Picture element:**

```html
<!-- Before -->
<picture>
  <source sizes="auto" srcset="..." />
  <img class="autosizes" sizes="auto" srcset="..." />
</picture>

<!-- After -->
<picture>
  <source sizes="450px" srcset="..." />
  <img class="autosizes autosized" sizes="450px" srcset="..." />
</picture>
```

### Manual API

```javascript
// Update a specific element
autoSizes.updateElem(imageElement);

// Update all elements
autoSizes.updateAll();

// Initialize (if auto-init is disabled)
autoSizes.init();
```

## Configuration

You can customize the behavior by setting `window.autoSizesConfig` before loading the script:

```javascript
window.autoSizesConfig = {
  // Minimum size threshold (elements smaller than this will look up parent chain)
  minSize: 40,

  // Target class for finding elements to process
  targetElementClass: 'autosizes',

  // Class added after sizes is calculated
  processedElementClass: 'autosized',

  // Attribute name for sizes
  sizesAttr: 'sizes',

  // Auto-initialize on load
  init: true
};
```

### Configuration Options Explained

- **`minSize`** (default: `40`): If element width is less than this value, the library will traverse up the DOM tree to find a parent with
  sufficient width
- **`targetElementClass`** (default: `'autosizes'`): CSS class used to identify elements that need automatic sizes calculation
- **`processedElementClass`** (default: `'autosized'`): CSS class added to elements after sizes has been calculated (useful for styling or
  debugging)
- **`sizesAttr`** (default: `'sizes'`): Attribute name to check for `"auto"` value. If it contains a prefix (like `'data-sizes'`), both the
  prefixed attribute AND the base `sizes` attribute will be set
- **`init`** (default: `true`): Whether to auto-initialize on page load

### Attribute Prefix Support

If `sizesAttr` contains a prefix (e.g., `'data-sizes'`, `'x-sizes'`), the library will set **both** attributes:

```javascript
window.autoSizesConfig = {
  sizesAttr: 'data-sizes'
};
```

```html
<!-- Input -->
<img class="autosizes" data-sizes="auto" srcset="..." />

<!-- Output - both attributes are set -->
<img class="autosizes autosized" data-sizes="450px" sizes="450px" srcset="..." />
```

This is useful for:

- Compatibility with frameworks that use data attributes
- Preserving the original attribute for debugging
- Working with tools that expect both attributes

## Events

### beforeSizesUpdate

Fired before the `sizes` attribute is set. Can be used to customize the calculated width:

```javascript
image.addEventListener('beforeSizesUpdate', function(e) {
  // Modify the calculated width
  e.detail.width = Math.ceil(e.detail.width / 100) * 100;

  // Or prevent the update
  // e.preventDefault();
});
```

### afterSizesUpdate

Fired after the `sizes` attribute has been set:

```javascript
image.addEventListener('afterSizesUpdate', function(e) {
  console.log('Sizes updated to:', e.detail.width + 'px');
});
```

## Styling Processed Images

Use the `processedClass` to style images after they've been processed:

```css
/* Show a subtle indicator when sizes is calculated */
img.autosized {
  outline: 2px solid green;
}

/* Or use it for transitions */
img.autosizes {
  opacity: 0.5;
  transition: opacity 0.3s;
}

img.autosized {
  opacity: 1;
}
```

## Browser Support

Works in all modern browsers that support:

- `srcset` and `sizes` attributes
- `classList` API
- `requestAnimationFrame`

Tested and working in:

- Chrome/Edge 90+
- Firefox 88+
- Safari 14+
- Mobile browsers (iOS Safari, Chrome Mobile)

## Extracted from lazysizes

This library extracts and focuses solely on the automatic `sizes` calculation feature from the
excellent [lazysizes](https://github.com/aFarkas/lazysizes) library. Use this if you:

- Want automatic sizes calculation without lazy loading
- Use native `loading="lazy"`
- Use a different lazy loading solution
- Want a smaller, focused library

## Credits

This library is extracted from the excellent [lazysizes](https://github.com/aFarkas/lazysizes) by Alexander Farkas.

**If you need advanced lazy loading features**, we highly recommend using the full lazysizes library instead. It provides:

- Automatic lazy loading of images, iframes, scripts
- Low quality image placeholders (LQIP)
- Progressive image loading
- Responsive image polyfills
- Extensive plugin ecosystem
- Battle-tested performance optimizations

This library exists for projects that:

- Already have a lazy loading solution
- Use native `loading="lazy"`
- Want only the automatic `sizes` calculation feature
- Need the smallest possible bundle size

## License

MIT
