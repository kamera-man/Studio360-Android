# Android Project Structure

## Overview

This document outlines the planned Android Studio project structure for Studio 360°.

---

## Directory Layout

```
Studio360-Android/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/kameraman/studio360/
│   │   │   │   ├── ui/                    # Activities & Fragments
│   │   │   │   │   ├── MainActivity.kt
│   │   │   │   │   ├── PreviewActivity.kt
│   │   │   │   │   └── LittlePlanetEditorActivity.kt
│   │   │   │   │
│   │   │   │   ├── conversion/            # Core conversion logic
│   │   │   │   │   ├── Facebook360Converter.kt
│   │   │   │   │   ├── XMPMetadataInjector.kt
│   │   │   │   │   └── LittlePlanetGenerator.kt
│   │   │   │   │
│   │   │   │   ├── dji/                   # DJI SDK integration
│   │   │   │   │   ├── DJIPanoramaDetector.kt
│   │   │   │   │   ├── DJIMediaManager.kt
│   │   │   │   │   └── DJIConnectionManager.kt
│   │   │   │   │
│   │   │   │   ├── preview/               # 360° OpenGL preview
│   │   │   │   │   ├── SphereRenderer.kt
│   │   │   │   │   ├── EquirectangularShader.kt
│   │   │   │   │   └── TouchController.kt
│   │   │   │   │
│   │   │   │   ├── models/                # Data models
│   │   │   │   │   ├── PanoramaFile.kt
│   │   │   │   │   ├── ExportOptions.kt
│   │   │   │   │   └── LittlePlanetSettings.kt
│   │   │   │   │
│   │   │   │   ├── utils/                 # Utilities
│   │   │   │   │   ├── ImageProcessor.kt
│   │   │   │   │   ├── FileScanner.kt
│   │   │   │   │   └── KameraManEquation.kt
│   │   │   │   │
│   │   │   │   └── Studio360Application.kt
│   │   │   │
│   │   │   ├── res/                    # Resources
│   │   │   │   ├── layout/
│   │   │   │   ├── values/
│   │   │   │   ├── drawable/
│   │   │   │   └── raw/              # GLSL shaders
│   │   │   │
│   │   │   └── AndroidManifest.xml
│   │   │
│   │   └── test/                   # Unit tests
│   │
│   └── build.gradle.kts
│
├── gradle/
├── build.gradle.kts
├── settings.gradle.kts
├── local.properties           # DJI API key goes here (not committed)
│
├── README.md
├── CLAUDE.md
├── DJI_SDK_INTEGRATION.md
├── XMP_METADATA_SPEC.md
└── PROJECT_STRUCTURE.md
```

---

## Key Components

### UI Layer
- **MainActivity**: File list, conversion controls, batch operations
- **PreviewActivity**: Full-screen 360° preview with touch controls
- **LittlePlanetEditorActivity**: Vernon Slider and real-time Little Planet editing

### Conversion Layer
- **Facebook360Converter**: Main conversion engine
- **XMPMetadataInjector**: Injects GPano metadata
- **LittlePlanetGenerator**: Stereographic projection implementation

### DJI Layer
- **DJIPanoramaDetector**: Monitors for panorama capture completion
- **DJIMediaManager**: Access drone SD card files
- **DJIConnectionManager**: Handle SDK initialization and product connection

### Preview Layer
- **SphereRenderer**: OpenGL ES sphere with equirectangular texture
- **EquirectangularShader**: Custom GLSL shaders for 360° mapping
- **TouchController**: Gesture handling for rotation/zoom

---

## Next Steps

1. Create Android Studio project with this structure
2. Setup DJI SDK dependencies
3. Implement stub classes for each component
4. Port iOS conversion logic to Kotlin
5. Test on RC Pro hardware

---

**🛠️ Architecture designed for RC Pro excellence!**