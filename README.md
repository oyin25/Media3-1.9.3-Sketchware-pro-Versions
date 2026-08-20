# Media3 1.9.3 — Sketchware Pro / Android TV Fixed

A prebuilt **AndroidX Media3 1.9.3** local-library project prepared for Sketchware Pro, with Media3 UI, HLS, DASH, Session, cache support, and cumulative Android TV compatibility patches.

This repository stores the library as normal project files and folders. It is **not a ZIP-only repository**.

## Included

- Media3 / ExoPlayer **1.9.3**
- Media3 common, container, database, datasource, decoder and extractor
- ExoPlayer core
- HLS
- DASH
- RTSP
- SmoothStreaming
- Media3 Session
- Media3 UI / `PlayerView`
- Media3 datasource cache (`SimpleCache`, `CacheDataSource`, etc.)
- Guava runtime classes required by the merged build
- Sketchware local-library metadata/resources

## Streamix / Sketchware patches retained

- AVI sync-sample compatibility backport
- TV MediaCodec PerformancePoint safe fallback
- Custom streaming/local `DefaultLoadControl` methods used by Streamix
- MediaSession Android TV `AudioAttributes` compatibility patch
- API-29 direct-playback capability probe fallback
- API-29 audio-offload capability fallback
- Removal of fragile `AudioTrack.Builder.setOffloadedPlayback(...)` use on affected TV firmware
- `AudioTrack.isOffloadedPlayback()` query fallback for affected TV firmware
- Session notification resource-link compatibility fix

The TV audio patches intentionally prefer stable decoded PCM playback over optional vendor offload/passthrough APIs on broken Android TV firmware.

## Sketchware Pro local-library structure

The published project includes the normal local-library files such as:

- `classes.jar`
- `classes.dex`
- `AndroidManifest.xml`
- `config`
- `R.txt`
- `proguard.txt`
- `res/`
- build / patch documentation

## Important

Do not enable this library alongside another Media3/ExoPlayer build containing the same `androidx.media3.*` classes. Remove the older local library first to avoid duplicate classes/resources.

The build is intentionally kept on **Media3 1.9.3** because the Streamix player code and custom patches were developed and verified against that version.

## Android TV compatibility

Several Android TV firmwares report API 29+ but crash when Media3 probes optional platform audio APIs. This build keeps normal MediaCodec → PCM → AudioTrack playback while bypassing those unreliable optional probes.

See the patch notes in the repository for the individual compatibility changes.

## Project status

This repository represents the latest cumulative build used during the Streamix Media3 migration and Android TV compatibility testing.
