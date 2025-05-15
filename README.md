# Crzgames Builder Libraries

## Informations repository
Ce dépôt build les bibliothèques des dépendences de Crzgames_RC2DCore qui sont sois beaucoup trop longue ou sois pas possible dans un CMakeLists.txt. <br />
Les bibliothèques : OpenSSL, ONNX Runtime et SDL3_shadercross. <br /><br />

## 📋 Plateforme supportés - ONNX Runtime :

| Platform | Architectures | System Version | Compatible |
|----------|---------------|----------------|------------|
| **Windows** | x64 / arm64 | Windows 10+  | ✓          |
| **macOS** | Apple Silicon arm64 | macOS 15.0+ | ✓ |
| **iOS/iPadOS** | arm64 (iphoneos) - not iphonesimulator | iOS 18.0+ | ✓ |
| **Android** | arm64-v8a / armeabi-v7a | Android 9.0+ | ✓ |
| **Linux** | x64 / arm64 | glibc 2.35+ | ✓ |
| **Steam Linux** | x64 / arm64 | Steam Linux Runtime 3.0 (Sniper) | ✓ |
| **Steam Deck** | x64 | Steam Linux Runtime 3.0 (Sniper) | ✓ |

## 📋 Plateforme supportés - OpenSSL :

| Platform | Architectures | System Version | Compatible |
|----------|---------------|----------------|------------|
| **Windows** | x64 / arm64 | Windows 10+  | ✓          |
| **macOS** | Intel x64 / Apple Silicon arm64 | macOS ?+ | ✓ |
| **iOS/iPadOS** | arm64 (iphoneos) - not iphonesimulator | iOS ?+ | ✓ |
| **Android** | arm64-v8a / armeabi-v7a | Android 9.0+ | ✓ |
| **Linux** | x64 / arm64 | glibc 2.35+ | ✓ |
| **Steam Linux** | x64 / arm64 | Steam Linux Runtime 3.0 (Sniper) | ✓ |
| **Steam Deck** | x64 | Steam Linux Runtime 3.0 (Sniper) | ✓ |

## 📋 Plateforme supportés - SDL3_shadercross :

| Platform | Architectures | System Version | Compatible |
|----------|---------------|----------------|------------|
| **Windows** | x64 / arm64 | Windows 10+  | ✓           |
| **macOS** | Apple Silicon arm64 | macOS 15.0+ | ✓ |
| **Linux** | x64 / arm64 | glibc 2.35+ | ✓ |
| **Steam Linux** | x64 / arm64 | Steam Linux Runtime 3.0 (Sniper) | ✓ |
| **Steam Deck** | x64 | Steam Linux Runtime 3.0 (Sniper) | ✓ |

<br />

---

<br />

## Notes utile

### ONNX Runtime
#### iOS / macOS :
- macOS 10.12 et ultérieures (c'est écrit sur la doc mais c'est faux) -> Il faut target la version macOS >= 13.4 et avec un sdk >= 14.4, issue concernant concernant cela : https://github.com/microsoft/onnxruntime/issues/21033
- iOS/macOS : Utilise tout les deux CoreML.
- iOS/macOS : Utiliser CMake 3.28 (minimum demandé par ONNX Runtime) à 3.31 (après cette version c'est CMake version 4.x.x, et fait planter avec le flag : --use_coreml)
- iOS 13.0 et ultérieurs (vu que le flag --use_coreml demande iOS 13.0+)
- IMPORTANT iOS/macOS : Pour utilisé CoreML il faut linker "-framework CoreML"
- Ce n'ai pas indiquer sur la doc mais on peux faire ça pour toute les plateformes Apple (au lieu de --build_shared_lib) : --use_xcode, --build_apple_framework puis requis : --ios, --macos, --visionos, ou --tvos, --apple_sysroot <the location or name of the macOS platform SDK> par exemple : <br />
--use_xcode --build_apple_framework --macos MacOSX/Catalyst --apple_sysroot macosx --apple_deploy_target 15.0 --osx_arch arm64
- macOS: Depuis onnxruntime >= 1.22.0, macOS x86_64 ne peux pas être construit depuis un macOS arm64

#### Windows :
- Windows x64/arm64 possible.
- Direct ML compatible que : x64 mais pas arm64 (c'est écrit sur la doc mais c'est faux) j'ai réussi à construire pour Windows arm64.
- Windows x64 : Fallback sur XNN si pas Direct3D12 (Execution Providers)
- Windows arm64 : Fallback sur XNN impossible puisque quand on lui passe l'argument cela plante avec XNN, donc arm64 aura que DirectML.

#### Linux / Steam Linux Runtime 3.0 (Sniper) :
- Linux x64/arm64 possible.
- XNN (Execution Providers)
- GCC >= 11.1

#### Android :
- Android arm64-v8a/armeabi-v7a possible.
- NNAPI (Execution Providers) compatible que à partir de : Android 8.1+ (API 27+), mais recommandé à partir de Android 9.0 (API 28+).

<br />

### OpenSSL
- Rien à signaler de particulier.

<br />

### SDL3_shadercross
- Windows arm64 : l'action "setup-sdl" ne marche pas encore, obliger de construire à partir des sources.
