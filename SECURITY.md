## 🔐 Security Issue: Insecure Random Number Generator

While performing a security audit on our Android app built with **Expo SDK `~51.0.38`**, our scanner flagged a **Medium severity vulnerability** in the native file:

**File:**
expo.modules.updates.UpdatesUtils.java

css
Copy
Edit

### 🔎 Vulnerable Code:
```java
"asset-" + Date().time + "-" + Random().nextInt() + fileExtension
❌ Problem:
java.util.Random is not cryptographically secure. It produces predictable values and is flagged by security tools like MobSF and SonarQube as an insecure RNG.

This can lead to:

Predictable asset filenames

Cache collision risks

Potential file guessability

✅ Recommended Fix
Replace java.util.Random() with java.security.SecureRandom():

java
Copy
Edit
import java.security.SecureRandom;

"asset-" + Date().time + "-" + new SecureRandom().nextInt() + fileExtension
This ensures strong, unpredictable random values backed by system entropy.

Environment
Expo SDK: ~51.0.38

Platform: Android

Module: expo-updates

File: UpdatesUtils.java

 Why This Matters
While this is only used in filename generation, weak randomness in any asset-related logic can have real-world implications:

Predictable or guessable file names

Vulnerable cache mechanisms

Possible attack vectors in shared storage environments

As a general best practice, all randomness in native modules should use SecureRandom.

🛠️ Temporary Workaround
We’ve applied a temporary fix using patch-package` to override the vulnerable implementation until an official patch is released.

 Request
Please confirm if:

This is already resolved in an upcoming release

A patch can be applied in the next version of expo-updates

Thanks a lot for maintaining such a powerful and developer-friendly ecosystem! 
