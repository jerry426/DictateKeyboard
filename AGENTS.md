# AGENTS.md

This repo is a personal fork of
[Dictate Keyboard](https://github.com/DevEmperor/DictateKeyboard), a
FlorisBoard-based Android keyboard. The goal is a voice-first keyboard with
OpenRouter batch models, Azure MAI-Transcribe-2-Streaming, and a typing
layout for corrections. See `PLAN.md` for the architecture and remaining
steps.

## Upstream

- `origin` is `jerry426/DictateKeyboard`. `upstream` is
  `DevEmperor/DictateKeyboard`. Upstream merges must stay cheap.
- Put new features in new files where possible. Keep edits to upstream files
  small, and don't reformat or reorganize upstream code.
- Speech providers live in
  `lib/dictate-core/src/main/kotlin/dev/patrickgold/florisboard/dictate/provider/`.

## Build

- The Android SDK is Homebrew's, at `/opt/homebrew/share/android-commandlinetools`.
  `local.properties` points Gradle to it and is not committed.
- To install packages, run `sdkmanager --sdk_root=/opt/homebrew/share/android-commandlinetools`.
  The SDK, NDK, and build-tools versions are pinned in
  `gradle/tools.versions.toml` and `gradle.properties`.
- To build a debug APK, run `./gradlew :app:assembleDebug`.
- To install on a USB-connected phone, run `./gradlew :app:installDebug`.
- The build fails until two sets of native libraries exist. They are not in
  git. After a fresh clone, run `tools/fetch-sherpa-onnx.sh` and
  `tools/bergamot/build-android.sh`. The Bergamot build needs the SDK's
  CMake package at the pinned version.

## Secrets

- Never commit API keys, keystores, or `keystore.properties`. Keys are entered
  in the app on the phone.

## Workspace

- `tmp/` is Workbench's scratch area for this repo, and git ignores it. Put
  build logs and other temporary files there instead of the system temp
  folder.
- The keyboard only needs English. Don't spend effort on other languages.
