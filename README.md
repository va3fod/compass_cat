# Compass Cat for Wear OS

**Navigate with Precision: A Feature-Rich Compass for Your Pixel Watch**

**Version 2.0** (`versionCode` 20) · package `com.compass_cat` · Wear OS 5 and later, including the Pixel Watch 3

![PXL_20250406_182111445](https://github.com/user-attachments/assets/a3d6b1aa-3940-434d-b3b9-5f9453deb1e4)
![PXL_20250406_124152110](https://github.com/user-attachments/assets/a20b2a29-474e-4036-bc27-ce80ed535ecd)

Compass Cat transforms your Google Pixel Watch (and other compatible Wear OS devices) into an advanced navigation tool. Designed for outdoor enthusiasts, hikers, and anyone needing reliable orientation, this app combines classic compass functionality with modern GPS data and intuitive controls.

## Support the Developer ☕

If Compass Cat brings value to your adventures, please consider making a small contribution to help keep development going. Every little bit helps and means the world to me!

**Send support via PayPal, Zelle, or Interac to:**
`aschiuta@gmail.com`

## Install

Download [CompassCat-2.0.apk](https://github.com/va3fod/compass_cat/releases/download/v2.0/CompassCat-2.0.apk) from the [v2.0 release](https://github.com/va3fod/compass_cat/releases/tag/v2.0).

Connect the watch with wireless debugging, then install or replace the current app:

    adb install -r CompassCat-2.0.apk

The package id is `com.compass_cat`. If a copy from before the rename is still on the watch, remove that old app:

    adb uninstall com.compass_gpt

## Key Features

*   **Compass rose:** N, E, S, and W with degree ticks. The crown rotates the bezel, and **BRG** is that bezel bearing.
*   **Both norths at once:** A **red triangle** marks Magnetic North. A **blue triangle** marks True North, offset by the local declination. Neither marker is hidden.
*   **Reference toggle:** Tap the cat icon to switch the bearing reference. **🐈** means headings are magnetic (`°M`). **🐾** means headings are true (`°T`). The BRG color follows that choice.
*   **Waypoint needle:** After you save a waypoint, the **yellow needle** points along the true bearing to it. With no waypoint saved, that needle is hidden. The fixed marker at 12 o'clock is the bezel bearing index, not a waypoint.
*   **Themes:** Long-press the center to cycle **Normal** (white and black), **Tactical Red**, and **NVG Green**.
*   **GPS readouts:** Speed (km/h), altitude (m), local time, magnetic declination, and latitude / longitude.
*   **Level bubble:** A clinometer on the right side of the face.
*   **Calibration warning:** A figure-8 and **CALIBRATE (8)** appear when the rotation sensor is unreliable.
*   **Ambient mode:** Always-on display uses a grayscale face with simplified ticks and the text readouts. Live north markers stay hidden in ambient mode so a stale heading is not shown.
*   **Battery use:** The rotation sensor runs at the UI sampling rate, GPS updates every 15 seconds while the app is active, and GPS slows to once a minute in ambient mode.
*   **Callsign screen:** Long-press the cat icon for 2 seconds to show **VA3FOD**, the app version (read from the build, currently **v2.0**), and support details. Double-tap to return to the compass.
*   **Squirrel Chase:** Double-tap the cat icon on the compass to start the easter egg.

## How to Use

1.  **Main compass:**
    *   **Red triangle** = Magnetic North.
    *   **Blue triangle** = True North.
    *   **Yellow needle** = saved waypoint. It is drawn only after a waypoint is set.

2.  **Two-second long presses:**
    *   **Center:** cycle themes (Normal, then Red, then Green).
    *   **Edge / bezel:** save a waypoint at your current location.
    *   **Cat icon:** open the callsign screen. It stays up until you double-tap.

3.  **Cat icon taps, on the compass:**
    *   **Single tap:** toggle magnetic (`°M`, 🐈) and true (`°T`, 🐾) reference.
    *   **Double tap:** start **Squirrel Chase**.

4.  **Calibration:**
    *   If you see the figure-8 or **CALIBRATE (8)**, move the watch through a large figure-8 until the warning clears.

## Technology Stack

*   **Language:** Kotlin
*   **Platform:** Wear OS (Optimized for Google Pixel Watch 3)
*   **Sensors:** `TYPE_ROTATION_VECTOR`, GPS
*   **UI:** Custom `View` drawing on `Canvas`

## Changelog

### v2.0
*   **Version 2.0**: The on-watch callsign screen, Gradle `versionName`, and this README all report 2.0 (`versionCode` 20). The displayed version is read from the build.
*   **North markers**: Magnetic North is the red triangle and True North is the blue triangle. Both stay visible. The cat icon only changes which one the BRG readout uses.
*   **Waypoint needle**: The yellow needle is shown only after a waypoint is saved, and it uses true bearing against the true heading.
*   **Callsign screen**: Long-press the cat icon to open it. It stays until a double-tap.
*   **Ambient and lifecycle**: Always-on display keeps the grayscale readouts and hides live north markers while the rotation sensor is paused.
*   **Package**: `com.compass_cat`. The installable APK is on the GitHub release.

### v1.8
*   **Restored UI Rendering**: Fixed a logic error in `onDraw` that caused readouts and triangles to disappear in v1.7.
*   **Stability**: Verified all primary compass elements are correctly layered and visible.

### v1.7
*   **Drift Mitigation**: Enhanced sensor stability by ensuring strict adherence to filtered rotation data.
*   **Robustness Improvements**: Optimized internal math to prevent orientation jumps during magnetic interference.

### v1.6
*   **Fixed Declination Orientation**: Corrected the visual relationship between Magnetic and True North (Magnetic is CCW of True North for negative/West declination).
*   **Restored Smoothness**: Re-synchronized the canvas rotation with the original filtering logic to ensure perfectly stable movement.

### v1.5
*   **Corrected Declination Logic**: Fixed the orientation of True North relative to Magnetic North.
*   **New North Indicators**: Replaced traditional needles with intuitive triangle markers on the inner compass ring.
*   **Dual North Display**: Both True (Blue Triangle) and Magnetic (Red Triangle) North are now visible at all times.
*   **Reference Toggle**: Clicking the cat icon now switches the bearing reference and readouts between Magnetic and True North without hiding the other.

### v1.4
*   **Persistent Secret Screen**: The "Support the Developer" screen now stays visible until you **double-tap** to return to the compass view.

### v1.3
*   **Support the Developer**: Added donation information to the README and the "Secret" screen on the watch.
*   **Battery Optimizations**: Reduced sensor sampling rate (15Hz vs 50Hz+) to save power.
*   **Adaptive GPS**: Smarter location update frequency to preserve battery during long trips.
*   **Ambient Mode**: Added a low-power grayscale UI for always-on display support.
*   **Version Info**: Added app version display to the "Secret" callsign screen.

### v1.1
*   Added **Night Mode** (Tactical Red) and **NVG Green** themes.
*   Added **Waypoint / Return to Start** functionality with yellow needle.
*   Added **Live GPS Coordinates** (Lat/Lon) to readouts.
*   Improved **Calibration Warning** with figure-8 visual.
*   Standardized all long-presses to 2 seconds.
*   Callsign persistence (stays 2s after release).
*   Fixed fireworks animation speed and sparkle effect.
