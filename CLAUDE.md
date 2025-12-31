# CLAUDE.md - Studio 360° Android Development

## Current Working State (December 31, 2025)

### Project Status

**Phase:** Initial Setup
**Platform:** Android (targeting DJI RC Pro)
**Sister Project:** Studio360 iOS (95% complete)

---

## What's Working

- ✅ Repository created and initialized
- ✅ Documentation framework established
- ✅ Development roadmap defined

---

## What's Pending

**Critical Path:**
1. ⏳ Android Studio project creation
2. ⏳ DJI Mobile SDK integration
3. ⏳ DJI SDK key registration
4. ⏳ Core conversion engine (Kotlin port from iOS Swift)
5. ⏳ XMP metadata injection implementation
6. ⏳ OpenGL ES 360° preview

---

## Known Challenges

### DJI RC Pro Limitations
- Locked Android launcher (requires workarounds)
- Limited internet access during flights
- Custom DJI file management system
- Restricted background processing

### Technical Unknowns
- DJI SDK compatibility with RC Pro (needs testing)
- Performance of 8K image processing on Snapdragon
- OpenGL ES shader complexity for 360° preview
- XMP metadata library availability on Android

---

## Implementation Queue

**Phase 1: Foundation (Weeks 1-2)**
1. Create Android Studio project structure
2. Integrate DJI Mobile SDK
3. Test SDK on actual RC Pro device
4. Implement basic file scanning

**Phase 2: Core Conversion (Weeks 3-6)**
1. Port XMP metadata injection to Kotlin
2. Implement Facebook 360° conversion logic
3. Add basic UI with file list
4. Test conversion accuracy

**Phase 3: Preview System (Weeks 7-10)**
1. OpenGL ES sphere rendering
2. Equirectangular texture mapping
3. Touch controls for rotation
4. Performance optimization

**Phase 4: DJI Integration (Weeks 11-14)**
1. Auto-detect panorama capture completion
2. Access DJI MediaManager files
3. Trigger conversion automatically
4. Handle DJI-specific metadata

**Phase 5: Little Planet (Weeks 15-18)**
1. Port LittlePlanetGenerator to Kotlin
2. Implement Vernon Slider
3. Add preset styles
4. Real-time preview optimization

---

## Technical Specifications

### Target Devices

**Primary:** DJI RC Pro
- Android 10
- Qualcomm Snapdragon
- 4GB RAM
- 5.5" 1080p display
- OpenGL ES 3.0 support

**Secondary:** Android Phones/Tablets
- Android 10+
- 3GB+ RAM
- OpenGL ES 3.0

### Performance Targets

- **8K Conversion:** < 5 seconds on RC Pro
- **Preview Load:** < 1 second
- **Little Planet:** < 10 seconds
- **Memory Usage:** < 500MB peak

### Output Specifications

**Facebook 360°:**
- Max Resolution: 6080×3040 (6K)
- Format: JPEG, quality 95%
- XMP Metadata: GPano namespace
- Dimensions must exactly match pixels

**Little Planet:**
- Square output (Instagram: 1080×1080)
- Stereographic projection
- Customizable radius (Vernon Slider)

---

## Development Best Practices

### Golden Rule: ONE THING AT A TIME
1. Read this CLAUDE.md completely
2. Identify the ONE thing to implement
3. Create feature branch
4. Test thoroughly
5. Document changes
6. Merge to main

### Code Quality Standards
- Kotlin coding conventions
- Comprehensive inline documentation
- Unit tests for conversion logic
- UI tests for critical paths
- Performance profiling for image operations

### Git Workflow
```bash
# Feature branches
git checkout -b feature/dji-sdk-integration

# Commit messages
git commit -m "Add DJI Media Manager integration

- Implement file scanning from DJI storage
- Add panorama detection logic
- Handle DJI-specific EXIF metadata

🤖 Generated with Claude Code"
```

---

## Cross-Platform Coordination

### Shared Concepts (from iOS version)

**The Kamera Man Equation:**
```
K(P,V,C,L) = ∏ Mᵢ(Sᵢ(P, A(V,C), Eᵢ(L)))
```
Must be implemented identically on both platforms.

**Family UI Names:**
- Vernon Slider → Radius control for Little Planet
- Charlyie Test → 30-second intuitive UI requirement
- Bruce Factor → Technical depth toggle

**Output Quality:**
Android and iOS must produce pixel-identical results for same input.

---

## DJI SDK Integration Notes

### Required Permissions
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
```

### SDK Initialization Pattern
```kotlin
DJISDKManager.getInstance().registerApp(
    applicationContext,
    object : DJISDKManager.SDKManagerCallback {
        override fun onRegister(error: DJIError?) {
            if (error == DJISDKError.REGISTRATION_SUCCESS) {
                // Start conversion engine
            }
        }
        // ...
    }
)
```

---

## Success Metrics

### Version 1.0 Goals
- [ ] Convert DJI panorama to Facebook 360° format
- [ ] Successful sideload to RC Pro
- [ ] Conversion completes in < 5 seconds
- [ ] XMP metadata validates in Facebook upload
- [ ] Passes Charlyie Test (30-second usability)

### Version 1.5 Goals
- [ ] Little Planet generation
- [ ] Vernon Slider functional
- [ ] Batch conversion
- [ ] Map view with GPS

### Version 2.0 Goals
- [ ] Auto-convert on capture
- [ ] Claude API integration
- [ ] Voice commands
- [ ] DJI Flight Log integration

---

## Resources & Links

**DJI Development:**
- SDK Docs: https://developer.dji.com/mobile-sdk/documentation
- Sample Code: https://github.com/dji-sdk/Mobile-SDK-Android
- Forum: https://forum.dji.com/forum-139-1.html

**Android Development:**
- ExifInterface: https://developer.android.com/reference/androidx/exifinterface/media/ExifInterface
- OpenGL ES: https://developer.android.com/develop/ui/views/graphics/opengl
- RenderScript: https://developer.android.com/guide/topics/renderscript

**iOS Reference:**
- Studio360 iOS: https://github.com/kamera-man/Studio360
- Working conversion logic: DJI360ConverterViewController.swift

---

## Why This File Exists

- Maintains context across Claude sessions
- Prevents feature regression
- Tracks implementation priorities
- Documents platform-specific challenges
- Coordinates with iOS version
- Preserves family-driven design philosophy

---

**Remember:** This is the Android adventure. The iOS version proves the concept works - now we bring it to the RC Pro! 🚀

---

*Last Updated: December 31, 2025*
*This file documents Android development state and prevents regression*