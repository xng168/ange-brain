# Mandarin Kids App: Web-First Architecture Decision Locked In

• **Resolved Windows/Mac platform constraint**: Chose PWA (web-first) over SwiftUI because you're on Windows; SwiftUI requires Mac. PWA still opens App Store path via Capacitor wrapper.

• **Architecture decision: static, offline PWA with no backend**. New rule added to Super Prompt (2b) that prevents accidental backend-creep — this keeps the app storable, shareable, and wrappable into native apps later without rewriting.

• **App Store monetization path stays open at zero cost**: Capacitor wraps the PWA into real iOS/Android apps on cloud Mac (Codemagic/Ionic Appflow/GitHub Actions). No hardware purchase needed. Only pay when you ship ($99/yr Apple, $25 one-time Google, cloud-build service). This is a late-stage decision, not a rewrite.

• **Immediate next steps unchanged**: Build the PWA first (start in `C:\Users\Angela\Projects\mandarin-kids-app`), test it in browser. Content (curriculum + native audio) is the real bottleneck—still happens in parallel.

• **Two open product questions**: (1) Simplified + Pinyin as v1 default? (schema holds Traditional + Zhuyin too); (2) Re-index gbrain for this venture searchability?
