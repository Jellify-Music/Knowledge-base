# 🏗️ Jellify Build Guide

A comprehensive guide for building and developing the Jellify React Native app locally.

## 📋 Overview

Jellify is a React Native music player application for Jellyfin Media Server. This guide covers setting up the development environment, building the app for both iOS and Android platforms, and understanding the project structure.

## 🎯 Quick Start

### Prerequisites Check
Before starting, ensure you have:
- **Node.js v22** or higher
- **Ruby** (for Fastlane)
- **Git** for version control
- **Yarn** package manager

### Platform-Specific Requirements

#### For iOS Development
- **macOS** (required for iOS development)
- **Xcode** (latest version recommended)
- **iOS Simulator** or physical iOS device
- **Apple Developer Account** (for device testing/distribution)

#### For Android Development
- **Android Studio**
- **Java Development Kit (JDK)**
- **Android SDK** and build tools
- **Android Emulator** or physical Android device

## 🚀 Initial Setup

### 1. Clone the Repository
```bash
git clone https://github.com/Jellify-Music/App.git
cd App
```

### 2. Install Dependencies

#### For iOS (with New Architecture)
```bash
yarn init-ios:new-arch
```
This command will:
- Install npm packages with network concurrency limit
- Install Bundler and required Ruby gems
- Install CocoaPods with React Native's New Architecture enabled

#### For Android
```bash
yarn init-android
```
This command will:
- Install npm packages with network concurrency limit

### 3. Environment Configuration
The app uses various configuration files:
- `.env` - Environment variables
- `react-native.config.js` - React Native configuration
- `metro.config.js` - Metro bundler configuration
- `tamagui.config.ts` - UI framework configuration

## 🍎 iOS Development

### Setup Process

1. **Install Dependencies**
   ```bash
   yarn init-ios:new-arch
   ```

2. **Configure Signing** (if you have access)
   ```bash
   cd ios
   fastlane match development --readonly
   ```
   > Note: You need access to the "Jellify Signing" private repository

3. **Open Project in Xcode**
   - Open `ios/Jellify.xcodeworkspace` (NOT the .xcodeproject file)
   - Wait for Xcode to finish indexing

### Running on iOS

1. **Start the Development Server**
   ```bash
   yarn start
   ```

2. **Run on Device/Simulator**
   - In Xcode, select your target device/simulator
   - Press the Run button or use `Cmd+R`
   
   Alternatively, use CLI:
   ```bash
   yarn ios
   ```

### Building for iOS

#### Development Build
```bash
yarn fastlane:ios:build
```

#### Create App Bundle (for OTA updates)
```bash
yarn createBundle:ios
```

### iOS-Specific Commands
```bash
# Clean iOS build artifacts
yarn clean:ios

# Reinstall CocoaPods
yarn pod:install:new-arch

# Clean and reinstall pods
yarn pod:clean && yarn pod:install:new-arch
```

## 🤖 Android Development

### Setup Process

1. **Install Dependencies**
   ```bash
   yarn init-android
   ```

2. **Configure Android SDK**
   - Install Android Studio
   - Set up `ANDROID_HOME` environment variable
   - Install required SDK versions and build tools

3. **Open Project in Android Studio**
   - Open the `android` folder in Android Studio
   - Let Android Studio sync Gradle files

### Running on Android

1. **Start the Development Server**
   ```bash
   yarn start
   ```

2. **Run on Device/Emulator**
   - In Android Studio, select your target device/emulator
   - Click the Run button
   
   Alternatively, use CLI:
   ```bash
   yarn android
   ```

### Building for Android

#### Development Build
```bash
yarn fastlane:android:build
```

#### Manual APK Build
```bash
yarn androidBuild
```
The APK will be located at: `android/app/build/outputs/apk/release/`

#### Create App Bundle (for OTA updates)
```bash
yarn createBundle:android
```

### Android-Specific Commands
```bash
# Clean Android build artifacts
yarn clean:android

# Install Fastlane gems for Android
cd android && bundle install
```

## 🛠️ Development Workflow

### Daily Development
```bash
# Start development server
yarn start

# Run linting
yarn lint

# Run type checking
yarn tsc

# Run tests
yarn test

# Format code
yarn format
```

### Code Quality
The project uses several tools for code quality:
- **ESLint** - Code linting
- **Prettier** - Code formatting
- **TypeScript** - Type checking
- **Husky** - Git hooks for pre-commit checks
- **Jest** - Testing framework

### Pre-commit Hooks
The project automatically runs:
- Prettier formatting on JS/TS files
- ESLint fixing on JS/TS files

## 📱 Testing

### Unit Tests
```bash
yarn test
```

### E2E Testing (Maestro)
```bash
# Install Maestro first
# Then run tests (Android example)
maestro test maestro-tests/android/
```

## 🔄 Over-the-Air (OTA) Updates

Jellify supports OTA updates for incremental app updates:

### Create OTA Bundles
```bash
# For Android
yarn sendOTA:android

# For iOS
yarn sendOTA:iOS
```

These commands use scripts in the `scripts/` directory to create and deploy app bundles.

## 🏗️ Project Architecture

### Key Technologies
- **React Native 0.80.0** with New Architecture
- **React 19.1.0**
- **TypeScript 5.8.3**
- **Tamagui** for UI components
- **React Navigation** for navigation
- **Jellyfin SDK** for API communication
- **TanStack Query** for state management
- **React Native Track Player** for audio playback

### Directory Structure
```
├── src/                    # Source code
├── android/               # Android-specific code
├── ios/                   # iOS-specific code
├── assets/                # App assets (icons, images)
├── scripts/               # Build and utility scripts
├── maestro-tests/         # E2E test files
├── patches/               # Package patches
└── screenshots/           # App screenshots
```

### Key Configuration Files
- `package.json` - Dependencies and scripts
- `app.json` - React Native app configuration
- `metro.config.js` - Metro bundler settings
- `babel.config.js` - Babel transpilation settings
- `tamagui.config.ts` - UI framework configuration
- `tsconfig.json` - TypeScript configuration

## 🚨 Troubleshooting

### Common Issues

#### iOS Build Issues
- **"No such file or directory"**: Ensure you opened `.xcodeworkspace` not `.xcodeproject`
- **Signing issues**: Make sure you have proper development certificates
- **Pod install failures**: Try `yarn pod:clean && yarn pod:install:new-arch`

#### Android Build Issues
- **ANDROID_HOME not set**: Configure Android SDK path in environment variables
- **Gradle sync issues**: Clean project and rebuild
- **Out of memory**: Increase Gradle heap size in `gradle.properties`

#### General Issues
- **Metro bundler issues**: Clear cache with `yarn start --reset-cache`
- **Node modules issues**: Run `yarn reinstall`
- **Version conflicts**: Ensure Node.js v22+ is being used

### Debugging Tips
1. Check React Native environment with `npx react-native doctor`
2. Use React Native Debugger for debugging
3. Enable console logging in development builds
4. Use Flipper for advanced debugging (if configured)

## 📚 Additional Resources

### Official Documentation
- [React Native Documentation](https://reactnative.dev/docs/getting-started)
- [Jellyfin API Documentation](https://typescript-sdk.jellyfin.org/)
- [Tamagui Documentation](https://tamagui.dev/docs/intro/introduction)

### Community
- [Jellify Discord Server](https://discord.gg/jellify)

### Development Tools
- [React Native CLI](https://github.com/react-native-community/cli)
- [Fastlane](https://fastlane.tools/)
- [Maestro Testing](https://docs.maestro.dev/)

## 🤝 Contributing

When contributing to Jellify:

1. **Fork the repository**
2. **Follow this build guide** to set up your environment
3. **Make your changes** following the coding standards
4. **Test thoroughly** on both platforms if possible
5. **Submit a Pull Request** with clear description

### Code Standards
- Use TypeScript for type safety
- Follow the existing code style (enforced by Prettier/ESLint)
- Write tests for new features
- Update documentation as needed

---

> This build guide is based on Jellify v0.12.37. For the most up-to-date information, always refer to the official repository README and documentation.
