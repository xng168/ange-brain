# Expo SDK 54 Downgrade - Compatibility Fix

- **Issue**: Scanning Expo QR code produced "Project is incompatible with this version of Expo Go" error
- **Root cause**: Project created on SDK 57, but only SDK 54 currently available on Apple App Store (App Store approval lag for SDK 55+)
- **Solution**: Downgraded project from SDK 57 (expo ~57.0.7, react-native 0.86.0) to SDK 54—a supported routine operation
- **Key decision**: Use compatible App Store version instead of fighting approval delays
- **Next**: Complete Metro Bundler rebuild, rescan QR code with iPhone camera to test on Expo Go
