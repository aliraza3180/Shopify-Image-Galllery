# Shopify Image Gallery Lightbox

A powerful, customizable image gallery lightbox solution for Shopify themes using metaobjects. This implementation provides a native-like fullscreen experience with smooth transitions, thumbnail navigation, and mobile-friendly touch gestures.

## ✨ Features

- 🖼️ **Custom Lightbox**: Beautiful, performant lightbox with smooth fade transitions
- 📱 **Mobile Optimized**: Touch/swipe gestures, responsive thumbnails (3 on mobile, 6 on desktop)
- 🖥️ **Fullscreen Mode**: Native-like fullscreen experience with dedicated exit button
- ⌨️ **Keyboard Navigation**: Arrow keys, Escape key support
- 🎯 **Marker-Based Positioning**: Place galleries anywhere in your content using `[gallery:id]` markers
- 🔄 **Multiple Galleries**: Support for unlimited galleries with different metaobjects
- ♻️ **Reusable Galleries**: Use the same gallery ID multiple times in the same page
- 🚀 **Performance Optimized**: Lazy loading, DOM caching, optimized image sizes
- ♿ **Accessible**: ARIA labels, keyboard navigation, semantic HTML
- 🌐 **Cross-Browser Compatible**: Works on Chrome, Firefox, Safari, Edge with vendor prefixes

## 📋 Requirements

- Shopify theme with Liquid support
- Shopify metaobjects feature enabled
- Access to theme code editor

## 🚀 Installation

1. **Copy the snippet file** to your theme:
   ```
   snippets/lightbox-metaobject-gallery-marker.liquid
   ```

2. **Include the snippet** in your theme (typically in `theme.liquid` or article/blog templates):
   ```liquid
   {% render 'lightbox-metaobject-gallery-marker' %}
   ```

## ⚙️ Setup

### Step 1: Create Metaobject Definition

1. Go to **Settings → Custom Data → Metaobjects**
2. Click **Add definition**
3. Create a new metaobject type called `gallery_group` with the following fields:

   | Field Name | Type | Required | Description |
   |------------|------|----------|-------------|
   | `gallery_id` | Single line text | Yes | Unique identifier (e.g., `summer-collection`) |
   | `gallery_name` | Single line text | No | Display name for the gallery |
   | `images` | File reference (list) | Yes | Array of images for the gallery |

### Step 2: Create Gallery Metaobjects

1. Go to **Content → Metaobjects → gallery_group**
2. Click **Add gallery_group**
3. Fill in:
   - **gallery_id**: A unique identifier (e.g., `summer-collection`, `product-gallery-1`)
   - **gallery_name**: Display name (optional)
   - **images**: Upload your gallery images

4. Repeat for each gallery you want to create

### Step 3: Use in Your Content

Place gallery markers anywhere in your blog posts, pages, or product descriptions:

```html
<p>Check out our summer collection: [gallery:summer-collection]</p>
```

The marker `[gallery:summer-collection]` will be automatically replaced with a beautiful gallery grid.

## 📖 Usage

### Basic Usage

Simply add a marker with your gallery ID:

```html
[gallery:your-gallery-id]
```

### Multiple Galleries

You can use multiple different galleries on the same page:

```html
<p>Summer Collection: [gallery:summer-collection]</p>
<p>Winter Collection: [gallery:winter-collection]</p>
<p>Product Gallery: [gallery:product-gallery-1]</p>
```

### Same Gallery Multiple Times

You can use the same gallery ID multiple times - each instance works independently:

```html
<p>First instance: [gallery:my-gallery]</p>
<p>Second instance: [gallery:my-gallery]</p>
```

### In Blog Posts

Add markers directly in your blog post content:

```markdown
# My Blog Post

Here's a gallery of my recent work:

[gallery:portfolio-2024]

And here's another one:

[gallery:behind-the-scenes]
```

### In Product Descriptions

Add product galleries in your product descriptions:

```html
<div class="product-description">
  <h2>Product Gallery</h2>
  [gallery:product-images]
  
  <h2>Lifestyle Images</h2>
  [gallery:lifestyle-shots]
</div>
```

## 🎨 Customization

### Gallery Grid Layout

The gallery uses a responsive grid:
- **Desktop**: 6 columns
- **Tablet**: 3 columns  
- **Mobile**: 3 columns (thumbnails)

To customize, modify the CSS in the `{% stylesheet %}` section:

```css
.metaobject-gallery-grid {
  grid-template-columns: repeat(6, 1fr); /* Desktop */
}

@media (max-width: 768px) {
  .metaobject-gallery-grid {
    grid-template-columns: repeat(3, 1fr); /* Mobile */
  }
}
```

### Thumbnail Sizes

Default thumbnail sizes:
- **Desktop**: 150px × 100px
- **Mobile**: 100px × 70px

Customize in the CSS:

```css
.lightbox-thumbnail {
  width: 150px;
  height: 100px;
}

@media (max-width: 768px) {
  .lightbox-thumbnail {
    width: 100px;
    height: 70px;
  }
}
```

### Image Sizes

Images are automatically optimized:
- **Full size**: 1920px width
- **Thumbnails**: 300px width

To change, modify the Liquid code:

```liquid
"url": "{{ image | image_url: width: 1920 }}",
"thumbnail": "{{ image | image_url: width: 300 }}",
```

## 🎮 Controls

### Mouse/Trackpad
- **Click thumbnail**: Open lightbox
- **Click image**: Navigate to next image
- **Click prev/next buttons**: Navigate images
- **Click close button**: Close lightbox
- **Click fullscreen button**: Enter fullscreen mode
- **Hover in fullscreen**: Show exit fullscreen button

### Keyboard
- **Arrow Left**: Previous image
- **Arrow Right**: Next image
- **Escape**: Close lightbox / Exit fullscreen

### Touch/Mobile
- **Swipe left**: Next image
- **Swipe right**: Previous image
- **Tap thumbnail**: Open lightbox
- **Tap close button**: Close lightbox

## 🔧 Technical Details

### Architecture

- **Custom Lightbox Class**: Vanilla JavaScript ES6 class
- **No Dependencies**: Pure JavaScript, no jQuery or external libraries
- **IIFE Wrapped**: Prevents global namespace pollution
- **MutationObserver**: Handles dynamically loaded content
- **Event Delegation**: Efficient event handling

### Performance Optimizations

- ✅ DOM element caching
- ✅ Lazy image loading
- ✅ Optimized image sizes (1920px main, 300px thumbnails)
- ✅ Smooth CSS transitions (150ms fade)
- ✅ Layout shift prevention (min-width/min-height)
- ✅ Debounced scroll events
- ✅ Removed console.log statements

### Browser Support

- ✅ Chrome/Edge (latest)
- ✅ Firefox (latest)
- ✅ Safari (latest, including iOS)
- ✅ Mobile browsers (iOS Safari, Chrome Mobile)

Vendor prefixes included for:
- `-webkit-transform`
- `-webkit-transition`
- `-webkit-backdrop-filter`
- `-webkit-box` / `-webkit-flex`
- `-o-object-fit`

## 📱 Responsive Design

The lightbox is fully responsive:

- **Desktop**: Full-featured with all controls visible
- **Tablet**: Optimized layout, touch-friendly
- **Mobile**: 
  - 3 thumbnails visible
  - Swipe gestures enabled
  - Larger touch targets
  - Optimized image sizes

## 🐛 Troubleshooting

### Gallery Not Showing

1. **Check metaobject name**: Must be exactly `gallery_group`
2. **Check gallery_id**: Must match exactly (case-insensitive)
3. **Check images**: Gallery must have at least one image
4. **Check snippet**: Ensure `{% render 'lightbox-metaobject-gallery-marker' %}` is included

### Images Not Loading

1. **Check image URLs**: Verify images are uploaded correctly
2. **Check console**: Look for JavaScript errors
3. **Check network**: Verify images are accessible

### Lightbox Not Opening

1. **Check JavaScript**: Ensure no console errors
2. **Check initialization**: Verify snippet is loaded
3. **Check selectors**: Ensure content container exists

### Fullscreen Not Working

1. **Check browser support**: Some browsers have restrictions
2. **Check CSS**: Verify fullscreen styles are loaded
3. **Check z-index**: Ensure no conflicting styles

## 📝 File Structure

```
snippets/
  └── lightbox-metaobject-gallery-marker.liquid
      ├── Liquid Template (metaobject data)
      ├── JavaScript (CustomLightbox class)
      └── CSS (All styles)
```

## 🔄 Updates & Maintenance

### Version History

- **v1.0.0**: Initial release
  - Custom lightbox implementation
  - Metaobject integration
  - Fullscreen mode
  - Mobile optimization
  - Performance optimizations

### Future Enhancements

Potential improvements:
- [ ] Video support
- [ ] Zoom functionality
- [ ] Social sharing
- [ ] Download button
- [ ] Slideshow mode

## 📄 License

This project is provided as-is for use in Shopify themes.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 💡 Tips & Best Practices

1. **Gallery IDs**: Use descriptive, lowercase IDs with hyphens (e.g., `summer-collection`)
2. **Image Optimization**: Upload optimized images to Shopify for best performance
3. **Alt Text**: Always add alt text to images for accessibility
4. **Testing**: Test on multiple devices and browsers
5. **Performance**: Don't use too many galleries on a single page (10+ is fine)

## 📞 Support

For issues, questions, or contributions, please open an issue on GitHub.

## 🎯 Use Cases

Perfect for:
- 📸 Portfolio galleries
- 🛍️ Product image galleries
- 📝 Blog post image collections
- 🎨 Showcase galleries
- 📱 Mobile-optimized image viewing
- 🖼️ Fullscreen image viewing

---

**Made with ❤️ for Shopify merchants**

