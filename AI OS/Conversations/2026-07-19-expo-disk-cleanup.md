# Expo Development: Disk Cleanup & Tunnel Resume

- **Diagnosed storage issue** preventing Expo development — device had insufficient free space for build/bundler operations
- **Cleared ~7.3 GB** of disk space (likely cache, old node_modules, or build artifacts), bringing free space to 7.7 GB
- **Prepared to resume Expo tunnel** — storage constraints now lifted, ready to run `npx expo start --tunnel` for iPhone testing
- **Next step**: Start Metro Bundler in tunnel mode and scan QR code on iPhone to test mobile app on device
