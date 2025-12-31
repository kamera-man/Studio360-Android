# XMP Metadata Specification for Facebook 360°

## Overview

Facebook requires specific XMP metadata in the `GPano` namespace for 360° photos to display correctly with the interactive globe icon.

---

## Required XMP Fields

### Minimal XMP Package

```xml
<?xml version="1.0"?>
<x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="XMP Core 5.1.0">
  <rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
    <rdf:Description rdf:about=""
        xmlns:GPano="http://ns.google.com/photos/1.0/panorama/">
      <GPano:UsePanoramaViewer>True</GPano:UsePanoramaViewer>
      <GPano:ProjectionType>equirectangular</GPano:ProjectionType>
      <GPano:CroppedAreaImageWidthPixels>6080</GPano:CroppedAreaImageWidthPixels>
      <GPano:CroppedAreaImageHeightPixels>3040</GPano:CroppedAreaImageHeightPixels>
      <GPano:FullPanoWidthPixels>6080</GPano:FullPanoWidthPixels>
      <GPano:FullPanoHeightPixels>3040</GPano:FullPanoHeightPixels>
      <GPano:CroppedAreaLeftPixels>0</GPano:CroppedAreaLeftPixels>
      <GPano:CroppedAreaTopPixels>0</GPano:CroppedAreaTopPixels>
    </rdf:Description>
  </rdf:RDF>
</x:xmpmeta>
```

---

## Critical Rules

### 1. Dimension Exactness

**CRITICAL:** XMP dimensions MUST exactly match actual image pixels.

```kotlin
// ❌ WRONG - Causes flat display
GPano:CroppedAreaImageWidthPixels = 6080
GPano:CroppedAreaImageHeightPixels = 3040
// But actual image is 5000x2500

// ✅ CORRECT - Globe icon appears
val actualWidth = bitmap.width  // e.g., 6080
val actualHeight = bitmap.height // e.g., 3040
GPano:CroppedAreaImageWidthPixels = actualWidth
GPano:CroppedAreaImageHeightPixels = actualHeight
```

---

## Android Implementation

### Using ExifInterface

**Facebook360MetadataInjector.kt:**
```kotlin
package com.kameraman.studio360.conversion

import androidx.exifinterface.media.ExifInterface
import android.graphics.Bitmap
import java.io.File

class Facebook360MetadataInjector {
    
    fun injectXMP(imageFile: File, width: Int, height: Int): Boolean {
        return try {
            val exif = ExifInterface(imageFile.absolutePath)
            
            // Generate XMP packet
            val xmpPacket = generateXMP(width, height)
            
            // Inject via UserComment (standard XMP location)
            exif.setAttribute(ExifInterface.TAG_USER_COMMENT, xmpPacket)
            
            // Save changes
            exif.saveAttributes()
            
            true
        } catch (e: Exception) {
            e.printStackTrace()
            false
        }
    }
    
    private fun generateXMP(width: Int, height: Int): String {
        return """<?xml version="1.0"?>
<x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="XMP Core 5.1.0">
  <rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
    <rdf:Description rdf:about=""
        xmlns:GPano="http://ns.google.com/photos/1.0/panorama/">
      <GPano:UsePanoramaViewer>True</GPano:UsePanoramaViewer>
      <GPano:ProjectionType>equirectangular</GPano:ProjectionType>
      <GPano:CroppedAreaImageWidthPixels>$width</GPano:CroppedAreaImageWidthPixels>
      <GPano:CroppedAreaImageHeightPixels>$height</GPano:CroppedAreaImageHeightPixels>
      <GPano:FullPanoWidthPixels>$width</GPano:FullPanoWidthPixels>
      <GPano:FullPanoHeightPixels>$height</GPano:FullPanoHeightPixels>
      <GPano:CroppedAreaLeftPixels>0</GPano:CroppedAreaLeftPixels>
      <GPano:CroppedAreaTopPixels>0</GPano:CroppedAreaTopPixels>
    </rdf:Description>
  </rdf:RDF>
</x:xmpmeta>"""
    }
}
```

---

## Verification

### Verify XMP Exists

```kotlin
fun verifyXMP(file: File): Boolean {
    val exif = ExifInterface(file.absolutePath)
    val userComment = exif.getAttribute(ExifInterface.TAG_USER_COMMENT)
    return userComment?.contains("GPano:UsePanoramaViewer") == true
}
```

---

## Platform Requirements

### Facebook
- Max resolution: 6080×3040 (6K)
- Format: JPEG, quality 90%+
- File size: < 30MB recommended
- XMP: Required for globe icon

### Instagram
- Max resolution: 1080×1080 (square crop)
- No XMP support (flattens to regular photo)
- Little Planet works best

---

**🌍 Precise metadata = Perfect 360° experience!**

*This specification ensures Android and iOS versions produce identical, Facebook-compatible outputs.*