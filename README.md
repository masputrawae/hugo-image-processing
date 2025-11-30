# Hugo Image Processing Template - Cheatsheet

## 📋 Basic Usage

### Minimal Usage

```go-html-template
{{ partial "images/Image" (dict "src" "images/photo.jpg") }}
```

### With Alt Text

```go-html-template
{{ partial "images/Image" (dict
  "src" "images/photo.jpg"
  "alt" "Description of image"
) }}
```

## 🎯 All Parameters

| Parameter | Type   | Default                    | Description                                                   |
| --------- | ------ | -------------------------- | ------------------------------------------------------------- |
| `src`     | string | **required**               | Path to local image or remote URL                             |
| `alt`     | string | `"Image"`                  | Alt text for accessibility                                    |
| `title`   | string | `""`                       | Title attribute (tooltip)                                     |
| `loading` | string | `"lazy"`                   | `"lazy"` or `"eager"`                                         |
| `class`   | string | `""`                       | CSS classes for styling                                       |
| `mode`    | string | `""`                       | Crop mode: `"square"`, `"portrait"`, `"landscape"`, `"smart"` |
| `base`    | number | `300`                      | Base width for responsive images                              |
| `sizes`   | slice  | `[320,768,1024,1280,1536]` | Custom width breakpoints                                      |

## 🌟 Use Cases & Examples

### 1. Local Images

```go-html-template
{{ partial "images/Image" (dict
  "src" "images/my-photo.jpg"
  "alt" "My beautiful photo"
  "class" "rounded-lg shadow-md"
) }}
```

### 2. Remote Images

```go-html-template
{{ partial "images/Image" (dict
  "src" "https://picsum.photos/1200/800"
  "alt" "Random placeholder image"
  "loading" "lazy"
) }}
```

### 3. Square Cropped Images

```go-html-template
{{ partial "images/Image" (dict
  "src" "images/portrait.jpg"
  "mode" "square"
  "base" 400
  "alt" "Square cropped profile picture"
  "class" "rounded-full"
) }}
```

### 4. Portrait Orientation

```go-html-template
{{ partial "images/Image" (dict
  "src" "images/vertical.jpg"
  "mode" "portrait"
  "base" 300
  "alt" "Vertical image optimized"
) }}
```

### 5. Landscape Orientation

```go-html-template
{{ partial "images/Image" (dict
  "src" "images/horizontal.jpg"
  "mode" "landscape"
  "base" 500
  "alt" "Wide landscape image"
) }}
```

### 6. Smart Cropping

```go-html-template
{{ partial "images/Image" (dict
  "src" "images/important-content.jpg"
  "mode" "smart"
  "base" 400
  "alt" "Smart cropped to focus on important areas"
) }}
```

### 7. Custom Width Breakpoints

```go-html-template
{{ partial "images/Image" (dict
  "src" "images/artwork.jpg"
  "sizes" (slice 400 800 1200 1600)
  "alt" "High resolution artwork"
) }}
```

### 8. Above-the-Fold Images (Eager Loading)

```go-html-template
{{ partial "images/Image" (dict
  "src" "images/hero-banner.jpg"
  "loading" "eager"
  "alt" "Important hero image"
  "class" "w-full h-64 object-cover"
) }}
```

### 9. With Title & Advanced Styling

```go-html-template
{{ partial "images/Image" (dict
  "src" "images/product.jpg"
  "alt" "Amazing product"
  "title" "Click to view product details"
  "class" "border-4 border-blue-500 hover:shadow-xl transition-shadow"
  "loading" "lazy"
) }}
```

### 10. Small Thumbnails

```go-html-template
{{ partial "images/Image" (dict
  "src" "images/thumbnail.jpg"
  "base" 150
  "mode" "square"
  "alt" "Small thumbnail"
  "class" "thumbnail"
) }}
```

## 🎨 Crop Modes Quick Reference

| Mode            | Description           | Best For                         |
| --------------- | --------------------- | -------------------------------- |
| **Default**     | Responsive resize     | General images, photos           |
| **`square`**    | Square crop (1:1)     | Profile pics, product thumbnails |
| **`portrait`**  | Vertical crop (1:4)   | Mobile screens, stories          |
| **`landscape`** | Horizontal crop (4:1) | Banners, hero images             |
| **`smart`**     | Focus-aware crop      | Faces, important content         |

## ⚡ Performance Tips

### For Critical Images

```go-html-template
{{ partial "images/Image" (dict
  "src" "images/above-fold.jpg"
  "loading" "eager"  <!-- Load immediately -->
  "sizes" (slice 320 640 960)  <!-- Fewer sizes for faster processing -->
) }}
```

### For Gallery Images

```go-html-template
{{ partial "images/Image" (dict
  "src" "images/gallery-item.jpg"
  "loading" "lazy"  <!-- Load when needed -->
  "mode" "square"   <!-- Consistent aspect ratio -->
  "base" 250        <!-- Smaller base for thumbnails -->
) }}
```

### For High-Resolution Images

```go-html-template
{{ partial "images/Image" (dict
  "src" "images/high-res.jpg"
  "sizes" (slice 800 1200 1600 2000)  <!-- Larger breakpoints -->
  "base" 500                          <!-- Higher base size -->
) }}
```

## 🚨 Error Handling

The template automatically handles:

- Missing local images (falls back to original src)
- Failed remote image loading
- Invalid processing parameters

Check Hugo console for warnings like:

```
WARN: Image not found: images/missing-photo.jpg
WARN: Failed to load remote image: https://invalid-url.com/image.jpg
```

## 📱 Responsive Behavior

**Default sizes attribute:** `(max-width: 320px) 320px, (max-width: 768px) 768px, (max-width: 1024px) 1024px, (max-width: 1280px) 1280px, (max-width: 1536px) 1536px`

**Outputs:**

- WebP format (modern browsers)
- JPEG fallback (compatibility)
- Proper width/height attributes
- Lazy loading by default

## 💡 Pro Tips

1. **Always include alt text** for accessibility
2. **Use `loading="eager"`** only for above-the-fold images
3. **Choose appropriate crop mode** for your layout
4. **Customize sizes** for specific breakpoint needs
5. **Monitor console warnings** for missing images
6. **Combine with CSS** for additional styling needs

---

**Template Location:** `layouts/partials/images/Image.html`

Copy this cheatsheet to your project documentation for quick reference! 🚀
