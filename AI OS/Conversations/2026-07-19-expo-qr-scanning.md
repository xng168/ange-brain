# Expo Go QR Scanning & Live Reload Setup

- **Problem solved:** Expo Go app was connecting to stale cached tunneled connections (`.exp.direct`) instead of fresh local development servers, causing outdated code to load
- **Key insight:** Camera app fresh scans are always correct (no caching), while tapping Expo Go's "Recently Opened" can persist old addresses; never rely on the app's memory for connections
- **Decision:** Established simple scanning habit—always use iPhone Camera pointed at the **current** terminal QR code, verify the address shows local IP (e.g. `exp://192.168.x.x:8081`) not `.exp.direct`, then tap the banner
- **Verification trick:** Scan the plain-text address printed above the QR in terminal as backup (should not contain `.exp.direct` if running fresh `npm start`)
- **Next:** Test this approach live in the current dev session to confirm the app now loads correct hot-reload code
