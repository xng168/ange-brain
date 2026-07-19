# Expo App Development: Debugging iPhone Connection Issue

- **Problem identified**: Expo Go app on iPhone couldn't connect to the development server running on Windows (error: "Could not connect to the server")
- **Root cause**: Wi-Fi connectivity or firewall blocking the local network connection; SDK version mismatch (57 vs current)
- **Solution proposed**: Switch Expo from LAN mode to **tunnel mode** (`npx expo start --tunnel`) to route traffic through the internet instead of requiring same local network; this bypasses router/firewall issues entirely
- **Next steps**: User needs to stop current server (Ctrl+C), run tunnel mode, allow ngrok installation if prompted, then rescan the new QR code with iPhone Camera and test the connection
- **Note**: Tunnel mode takes longer to start (30–40 seconds) but is more reliable for cross-device testing; SDK version should not prevent scanning if Expo Go is up to date

