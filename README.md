# ae-pcd-stamp-tracer Public Case Study

Public portfolio version of `ae-pcd-stamp-tracer`, my private Android game-runtime instrumentation
research project.

The private repository contains target-specific implementation details, so this public repo focuses
on the architecture, systems problems, and interview-relevant engineering without publishing raw
target-specific code.

## What This Project Demonstrates

- Android LSPosed module architecture with Java, C++, JNI, CMake, Gradle, and the Android NDK
- Engine detection for Unity, Unreal, Cocos2d-x, Godot, Flutter, React Native, and Xamarin
- Native library discovery using `/proc/self/maps`
- IDA-style byte-pattern scanning and symbol-oriented native research
- Lua script-load inspection for Cocos2d-x/Lua runtimes
- Runtime feature toggles, overlay controls, and native status reporting
- Fast-iteration research for dialogue/timer flows while preserving script side effects
- Runtime state tracing patterns relevant to AI-agent game evaluation and automated testing

## Why It Is Relevant

Game-oriented AI research often needs infrastructure below normal editor scripting:

- state extraction from real game/runtime environments
- repeatable automation across device and emulator setups
- controlled simulation speedups
- verification that side effects still occur in the intended order
- instrumentation that works in native-heavy Android apps

`ae-pcd-stamp-tracer` is the project where I explored those problems most deeply.

## Public Companion Repositories

- Android game runtime portfolio: https://github.com/Jordan231111/android-game-runtime-portfolio
- Unity IL2CPP public sample: https://github.com/Jordan231111/Archero-LSPOSED-Mod
- ARM64 Houdini framework: https://github.com/Jordan231111/arm64-houdini-lsposed-framework
- Universal LSPosed template: https://github.com/Jordan231111/lsposed-universal-template

## Interview Walkthrough

See [docs/interview-walkthrough.md](docs/interview-walkthrough.md).

