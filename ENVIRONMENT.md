# Termux / PRoot ARM64 Android Build Environment Rules

- Host Environment: Termux / PRoot ARM64 (Ubuntu container)
- Target Java: OpenJDK 17
- Scope Guardrail: Work EXCLUSIVELY inside current project workspace. DO NOT inspect `/tmp` or system recovery directories.
- Gradle Configurations:
  * Always enforce AAPT2 override in `gradle.properties`:
    android.aapt2FromMavenOverride=/data/data/com.termux/files/usr/bin/aapt2
  * Always enforce JVM limits in `gradle.properties`:
    org.gradle.jvmargs=-Xmx2048m -XX:MaxMetaspaceSize=512m
- Build Command: `./gradlew assembleDebug`
- Deployment Git Credentials:
  * Name: highsockscapital
  * Email: highsockscapital@gmail.com
