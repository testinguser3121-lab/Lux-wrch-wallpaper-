# Luxury Watch — Live Wallpaper

An Android live wallpaper that renders an elegant animated analog "luxury watch"
face (gold bezel, gold hour markers, sweeping hands, gradient dial) directly
onto the home/lock screen using `Canvas`.

## Structure

- `MainActivity.kt` — simple launcher screen with a button that opens the
  system live-wallpaper picker pre-selected to this wallpaper.
- `WatchWallpaperService.kt` — the `WallpaperService`/`Engine` that owns the
  surface, redraws once a second, and pauses drawing when not visible.
- `WatchCanvas.kt` — all the actual drawing logic (background gradient,
  bezel, dial, tick marks, brand text, hour/minute/second hands). Kept
  separate from the service so it's easy to test or reuse elsewhere.
- `res/xml/wallpaper.xml` — the required live wallpaper metadata, referenced
  from the `<service>` entry in `AndroidManifest.xml`.

## Opening the project

1. Open this folder (`LuxuryWatch/`) in Android Studio (Koala or newer).
2. Let Gradle sync — it uses AGP 8.5.2 / Kotlin 1.9.24 / compileSdk 34,
   minSdk 24.
3. Run the `app` module on a device or emulator (API 24+).

## Trying the wallpaper

- Launch the app and tap **"Set as Live Wallpaper"** — this opens Android's
  live wallpaper picker with Luxury Watch pre-selected.
- Alternatively: long-press the home screen → **Wallpapers** →
  **Live Wallpapers** → **Luxury Watch**.

## Customizing the look

All visual tuning lives in `WatchCanvas.kt`:
- Colors: `gold`, `goldLight`, `dialColor`, `charcoal` at the top of the class.
- Tick/hand proportions: the `r * 0.xx` multipliers in `drawTicks`/`drawHands`.
- Brand text: `drawBrand()` (currently "LUXURY" / "AUTOMATIC").

## Notes

- The launcher/wallpaper icon is a simple vector adaptive icon
  (`ic_launcher_foreground.xml` / `ic_launcher_background.xml`) — swap in a
  real PNG/vector logo if you have branded artwork.
- The engine redraws every second, which is enough for a visibly sweeping
  second hand without burning battery; lower the interval in
  `WatchWallpaperService.kt` if you want smoother sub-second motion.
