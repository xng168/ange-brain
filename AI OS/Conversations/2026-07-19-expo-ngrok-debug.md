# Expo Tunnel/ngrok Installation Issue Debugging

- **Problem identified**: `npx expo start --tunnel` was failing due to missing ngrok; root cause was silent installation failure from insufficient disk space despite npm reporting success
- **Root cause analysis**: npm marked ngrok.exe (30 MB binary) as optional in the package, so the install succeeded at the npm level even though the actual executable was never downloaded
- **Solution verified**: Disk space cleared, ngrok reinstalled correctly with the actual executable now present
- **Next action**: User to retry `npx expo start --tunnel` command — should proceed straight to Metro Bundler startup and display QR code, then scan with iPhone Camera app to connect device
- **Key lesson**: When installations report success but tools don't work, check for silent partial failures (especially large optional binaries) and disk space constraints
