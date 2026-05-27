# Technical Architecture

## Architecture

The private project is structured around four layers:

1. Android module entry and process filtering.
2. Runtime feature registry and overlay controls.
3. Native library discovery, pattern scanning, and hook installation.
4. Target-specific research modules for script, dialogue, achievement, and runtime-state tracing.

## Layer Responsibilities

| Layer | Responsibility | Portfolio Signal |
| --- | --- | --- |
| Android entry | Load only inside intended target processes and keep the module disabled elsewhere. | Production-style scope control and stability thinking. |
| Feature registry | Store booleans/floats, expose runtime controls, and persist settings across launches. | Runtime tooling design instead of one-off scripts. |
| JNI/native bridge | Connect Java controls to C++ status, scanners, and runtime instrumentation. | Android systems integration. |
| Native runtime tools | Discover loaded libraries, inspect memory ranges, resolve symbols, scan patterns, and report counters. | Low-level debugging and engine internals. |
| Script research | Observe script load boundaries and map script helpers to native/UI behavior. | Cocos2d-x/Lua runtime understanding. |

## Engine Detection

The reusable detector looks for engine libraries such as:

- `libil2cpp.so` and `libunity.so` for Unity
- Unreal library names
- Cocos2d-x library names
- Godot Android runtime libraries
- Flutter / React Native / Xamarin runtime markers

That matters because hook strategy differs by engine. Unity IL2CPP favors metadata-driven method
and field resolution. Cocos2d-x/Lua work often starts with script-load boundaries and native C
bindings.

## Lua Runtime Research

The project investigates Lua chunk loading and script execution in a native Android game runtime.
The key idea is to observe decoded script buffers at load time, then map script-level names to native
side effects and UI behavior.

This is useful for understanding:

- dialogue dispatch
- coroutine yield boundaries
- wait/input helpers
- scene transitions
- reward/flag/save side effects

## Native Runtime Workflows

The project uses a layered workflow:

1. Identify active process and ABI.
2. Confirm which engine/runtime libraries are mapped.
3. Choose an engine strategy: IL2CPP metadata, Cocos2d-x/Lua script boundary, exported symbols, or pattern research.
4. Add a narrow observation point.
5. Verify with status counters and logs.
6. Only then add a runtime toggle or patch.

This is intentionally conservative. A runtime tool that cannot be turned off or verified is not a
good research tool.

## Fast-Iteration Design

For dialogue/timer acceleration, the important design point is preserving execution order.

The safe design is not to jump to the end of a script. The safe design is to shorten waits while
still iterating through each script step so state changes, rewards, flags, saves, and transitions
fire in their natural order.

That reasoning maps directly to AI simulation work, where fast iteration is useful only if the
environment state remains valid.

## Relevance To AI-Agent Evaluation

An AI agent interacting with a game needs a bridge between model decisions and environment state.
This project studies the lower-level pieces of that bridge:

- detecting which runtime is present
- locating stable observation points
- reducing idle wait time
- preserving side effects
- producing counters/logs that make runs auditable
- running on Android devices and emulators

## Discussion Topics

- How I identify the process and loaded runtime libraries.
- How I choose a Unity IL2CPP strategy versus a Cocos2d-x/Lua strategy.
- How I verify hooks fail closed instead of corrupting state.
- How I use counters/status files to validate behavior on-device.
- How emulator/root setup supports repeatable runtime experiments.
- How this work connects to AI-agent evaluation, state extraction, and simulation acceleration.
