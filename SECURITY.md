# Security Policy

## Reporting a Vulnerability
Hello Expo team,

While running a security audit on our Expo SDK 51 project, we found that expo.modules.updates.UpdatesUtils.java still uses java.util.Random, which is flagged as a weak random number generator.

This may introduce a security vulnerability if randomness is used for sensitive operations.

📄 Affected File: UpdatesUtils.java
🔍 Expo SDK: 51.0.38
🛡️ Recommendation: Replace java.util.Random with java.security.SecureRandom.

Please confirm if this is on the roadmap or fixed in future releases.

Thank you!
