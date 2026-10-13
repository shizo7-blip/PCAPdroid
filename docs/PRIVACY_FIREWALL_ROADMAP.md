# Privacy Firewall – implementation and verification plan

This fork is based on PCAPdroid and remains subject to its GPL-3.0 license.

## Already available in upstream code

- Android VPN-based traffic monitoring
- Firewall blocklist and whitelist mode
- Per-app matching and rule import/export (verify individual formats in UI)
- Existing German localization

## Intended security modes

**Normal mode (default):** Existing firewall with user-configured block rules. Do not silently block all traffic.

**High-security mode (opt-in):** Use the existing firewall whitelist mode with explicit allow rules. Before enabling, show a warning about loss of connectivity for messaging, push notifications, updates, and emergency-relevant apps. Keep a clear disable control and a recoverable configuration.

Do not label this as anti-spyware detection. A VPN firewall cannot guarantee detection of privileged malware or bypasses, and encrypted traffic can conceal destinations or payloads.

## Proposed future features (not yet implemented)

1. Locally stored security event history with retention and export controls.
2. Suspicious network behavior heuristics with conservative thresholds and false-positive indicators.
3. Optional offline GeoIP/ASN lookup, including clear uncertainty labels.
4. Inbound port-scan detection only where packets are actually visible to Android's VPN service.
5. Local-only privacy defaults: no additional telemetry or remote reputation lookup without opt-in.
6. Review and localize all new user-facing strings in German.

## Verification gates

- Gradle unit tests and debug APK build in GitHub Actions.
- Inspect resulting APK and test VPN permission, startup, blocking, whitelist mode, DNS handling, and disable/recovery on an Android 15 device.
- Verify IPv4/IPv6, Wi-Fi and mobile data, background execution, and battery use.
- Verify that only the intended GPL-licensed components are distributed.
- Never advertise protection against all government spyware or all external scans.

## Separate future project: encrypted image messaging

A separate Android app can encrypt plaintext using an audited authenticated-encryption library and encode the ciphertext in an image container. Key exchange, metadata exposure, image recompression, and tamper detection require dedicated threat modeling and tests. Do not implement custom cryptographic primitives.
