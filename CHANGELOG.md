### Unreleased

Signing changes:

* Switch from signing new release zips, as well as git commits and tags, with GPG to SSH (PR: #229, @chenxiaolong)
  * The goal is to switch to stronger cryptography and rely on a simpler tool that everybody already has installed (including on Windows). For folks who were previously verifying signatures using GPG, please see the updated documentation for how to verify signatures with SSH.
  * For folks who want to verify that this change is legitimate, see commit 0bc3935fe2a1b6e3d56049503db521877501edc1. That commit, which introduced this change, was signed using the original GPG key.
  * The APK signing key remains unchanged.

### Version 1.30

* Update Slovak translations (PR: #217, @pvagner)
* Update Polish translations (PR: #219, @Twoomatch)
* Improve English description of `initially paused` preference (PR: #220, @Twoomatch)
* Update Spanish translations (PR: #222, @nmayorga092)

Magisk module updater changes:

* Show changelog for the correct version, excluding unreleased changes (PR: #223, @chenxiaolong)

Documentation changes:

* README.md: Fix typos (PR: #221, @Twoomatch)

### Version 1.29

* Add a new option for starting the recording in the paused state (Issue: #198, PR: #211, @chenxiaolong)
  * If enabled, this allows the user to choose whether a call is recorded. If a recording starts in the paused state and is never resumed, then the empty output file is not saved.

Documentation changes:

* README.md: Document hidden/advanced features (Issue: #212, PR: #213, @chenxiaolong)

### Version 1.28

* Inform the user that the device/firmware might not support call recording if an error origates from Android's internal components (PR: #206, @chenxiaolong)
* Fix crash if any filename template value (eg. caller/contact name) contains \ or $ (Issue: #207, PR: #209, @chenxiaolong)
* Add support for pausing/resuming the recording (Issue: #198, PR: #210, @chenxiaolong)
  * The button is in the `Call recording in progress` notification

### Version 1.27

* Update Polish translations (PR: #192, @Twoomatch)
* Update Spanish translations (PR: #201, @nmayorga092)
* Fix silent crash causing recording to not happen when debug mode is enabled (Issue: #195, PR: #203, @chenxiaolong)
  * The bug was introduced in version 1.26
* Add support for changing the filename timestamp format (Issue: #204, PR: #205, @chenxiaolong)
  * Similar to the existing output filename options, this can only be done via the `bcr.properties` config file

Non-user-facing changes:

* Update Kotlin and AndroidX (PR: #196, @PatrykMis)
* Update Build Tools (PR: #199, @PatrykMis)

### Version 1.26

* Update Turkish and Russian translations (PR: #188, @EleoXDA)
* Add hidden feature to customize the output filename (PR: #189, @chenxiaolong)
  * To avoid complicating BCR's code, there is no UI option for this
  * To customize the output filenames, copy [the default template](./app/src/main/res/raw/filename_template.properties) to `bcr.properties` in the output directory and edit the file

### Version 1.25

* Add SIM slot ID to the filename if there are multiple active SIMs (Issue: #177, PR: #178, @chenxiaolong)
* Fix share action in the recording complete notification always referencing an old recording (PR: #181, @chenxiaolong)
* Add a new Delete action alongside Open and Share in the notifications (Issue: #179, PR: #182, @chenxiaolong)
* Allow changing output settings when call recording is disabled (PR: #183, @chenxiaolong)

Documentation changes:

* README.md: Explain what every permission is used for (PR: #180, @chenxiaolong)

Non-user-facing changes:

* Update gradle wrapper to 7.6.0 (PR: #174, @PatrykMis)

### Version 1.24

* Notification improvements (PR: #169, @chenxiaolong)
  * A notification is now shown when a recording completes, with options for opening or sharing the recording in a 3rd party app.
    * **NOTE: Manual action required.** For opening/sharing recordings to work, reset the output directory to the default and then select the output directory again. This is required because BCR previously only requested write access to the output directory, but not read access.
    * These new notifications can be disabled in Android's settings by turning off the `Success alerts` notification channel.
  * The file path in error notifications is now human readable instead of a URL-encoded `content://...`.
* BCR will explicitly vibrate if vibration is enabled for its notification channels (PR: #167, #171, @quyenvsp, @chenxiaolong)
  * This is needed because Android will not respect the notification vibration option during a phone call.

Non-user-facing changes:

* Updated all dependencies (PR: #160, @PatrykMis)
* Fixed Gradle non-laziness, causing the execution of specific tasks to be slower (PR: #168, @chenxiaolong)

### Version 1.23

* Update all dependencies and fix build system lint issues (PR: #155, @PatrykMis)
* Add Slovak translation (PR: #161, @pvagner)

### Version 1.22

* (Direct installs only) Add `/system/addon.d/` script to persist installation across OS updates (Issue: #142, PR: #144, @chenxiaolong)
  * Only applies to LineageOS-based firmware
* Improve logging in debug mode (Issue: #143, PR: #145, #147, #148, @chenxiaolong)
  * Run logcat interactively for the duration of the call to ensure no lost log messages due to logcat overflow
  * Include BCR version number in the logs
* Improve output file writing reliability (Issue: #143, PR: #146, #149, #150, @chenxiaolong)
* Improve call disconnection detection on buggy firmware (Issue: #143, PR: #151, @chenxiaolong)
  * Works around Samsung OneUI's telephony framework bug where Android does not notify apps (including their own) when a call disconnects
* Use non-blocking reads from call audio stream (Issue: #143, PR: #152, @chenxiaolong)
  * Fixes recordings not stopping until another call becomes active on Samsung OneUI because `AudioRecord.read()` blocks forever as soon as a call disconnects

### Version 1.21

* (Direct installs only) Explicitly remount system as writable and ignore `ENOENT` errors during cleanup (Issue: #108, #138, PR: #139, @chenxiaolong)
* Updated all dependencies (PR: #140, @chenxiaolong)

### Version 1.20

* Update dependencies (PR: #121, #132, @PatrykMis)
* Perform a direct install if `/system/bin/recovery` exists in the environment (Issue: #131, PR: #133, @chenxiaolong)
  * Previously, only `/sbin/recovery` was used to detect if booted into recovery

### Version 1.19

* Add support for flashing via recovery (Issue: #128, PR: #130, @chenxiaolong)
  * This is for unrooted (non-Magisk) installs only. BCR will be installed to the system partition directly when flashed via recovery.

### Version 1.18

* Update gradle wrapper to 7.5.1 (PR: #116, @PatrykMis)
* Fix plurals in Russian translations (PR: #117, @EleoXDA)
* Add French translation (PR: #120, @NSO73)

### Version 1.17

* Update dependencies and gradle wrapper (PR: #112, @PatrykMis)
* Update Polish translations (PR: #112, @PatrykMis)
* Fix silent crash when receiving a call from a private number (Issue: #111, PR: #114, @chenxiaolong)

### Version 1.16

* Update Turkish translations (PR: #106, @EleoXDA)
* Update Russian translations (PR: #107, @EleoXDA)

### Version 1.15

* Update Spanish translations (PR: #92, @nmayorga092)
* Update Turkish translations (PR: #97, @EleoXDA)

### Version 1.14

* Add support for a basic file retention policy (Issue: #25 #81 #88, PR: #90, @chenxiaolong)

Non-user-facing changes:

* Improve type-safety when loading and saving preferences (PR: #91, @chenxiaolong)

### Version 1.13

* Add Polish translations (PR: #76, @uvzen)
* Target stable API 33 (Tiramisu) (PR: #82, @chenxiaolong)
* Add optional contacts permission to initial permissions prompt (Issue: #78 #80, PR: #84, @chenxiaolong)
  * If allowed, contact names are added to the output filenames.
  * This feature was implemented in version 1.5, but required the user to manually enable from the system settings.

Non-user-facing changes:

* Update Android gradle plugin to 7.2.1 and Kotlin to 1.7.0 (PR: #83, @chenxiaolong)

### Version 1.12

* Fix potential crash when showing user-friendly output directory path (PR: #74, @chenxiaolong)
  * Fixes regression in version 1.11

### Version 1.11

* Fix persistent notification icon being too small (PR: #67, @chenxiaolong)
* Increase internal buffer sizes to reduce chance of encoding slowdowns causing audible artifacts (Issue: #39 #54, PR: #69 #73, @chenxiaolong)
  * The native sample rate option had to be removed for this change
* Show user-friendly path instead of a raw URI for the output directory (PR: #71, @chenxiaolong)
* Work around SAF slowness by recording to the default directory and then moving to the user directory after recording is completed (Issue: #39 #54, PR: #72, @chenxiaolong)

Non-user-facing changes:

* Change Container abstract class to an interface (PR: #68, @chenxiaolong)
* Update all gradle dependencies (PR: #70, @chenxiaolong)

### Version 1.10

* Update Spanish translations (PR: #64, @nmayorga092)
* Add hidden debug mode, which saves logs for each recording (long press version number to enable) (PR: #65, @chenxiaolong)
* Set recording thread priority to THREAD_PRIORITY_URGENT_AUDIO (Issue: #39 #54, PR: #66, @chenxiaolong)

### Version 1.9

* Improve buffering to reduce chance of audio drops (Issue: #39 #54, PR: #61, @chenxiaolong)

### Version 1.8

* Update Turkish translations (PR: #58, @fnldstntn)
* Fix overlapping audio and other audible artifacts when using an encoded format (OPUS, AAC, or FLAC) (Issue: #39 #54, PR: #59, @chenxiaolong)

### Version 1.7

* Change output format button group to material chips to prevent text from being cut off with narrower screen widths (Issue: #52, PR: #55, @chenxiaolong)
* Add support for configuring the capture sample rate (PR: #56, @chenxiaolong)
* Send notification if an error occurs during call recording (PR: #57, @chenxiaolong)

### Version 1.6

* Enable minification (without obfuscation) to shrink the download size by ~64% (PR: #45, @chenxiaolong)
* Update Turkish translations (PR: #46, @fnldstntn)
* Add support for WAV/PCM output for troubleshooting (bypasses encoding/compression pipeline) (PR: #48, @chenxiaolong)

Non-user-facing changes:

* Improve output format parameter abstraction (PR: #49, @chenxiaolong)
* Use view binding instead of findViewById where possible (PR: #50, @chenxiaolong)

### Version 1.5

* Optionally add contact name to output filename if Contacts permission is granted (Android 11+) (Issue: #28, PR: #42, @chenxiaolong)
* Add Spanish translation (PR: #41, @nmayorga092)
* Redact sensitive information from logcat logs (PR: #43, @chenxiaolong)

### Version 1.4

* Add support for configurable output formats: OGG/Opus (Android 10+), M4A/AAC, FLAC (Issue: #21, PR: #29, #32, #34, #35, #38, @chenxiaolong)
* README.md: Remove mention of cloud storage. Android's Storage Access Framework does not support cloud storage when opening folders (Issue: #30, PR: #31, @chenxiaolong)
* Add full changelog text for updates from Magisk Manager (PR: #36, @chenxiaolong)

Non-user-facing changes:

* Fix minor compiler warnings (PR: #37, @chenxiaolong)

### Version 1.3

* Write audio duration to FLAC metadata after recording is complete (Issue: #19, PR: #20, @chenxiaolong)
* Add Turkish translations (Issue: #18, PR: #22, @fnldstntn)

Non-user-facing changes:

* Don't add irrelevant update metadata to release zips (PR: #23, @chenxiaolong)
* Fix serialization exception when running the `updateJson` gradle tasks (PR: #24, @chenxiaolong)

### Version 1.2

* Fix typo and improve wording of battery optimization preference (PR: #4, @EleoXDA)
* Add Russian translations (PR: #7, @marat2509)
* Add support for API 28 (Android 9) (Issue: #6, PR: #10, @chenxiaolong)
* Add incoming/outgoing tag to filenames (Issue: #3, PR: #11, @chenxiaolong)
* Add caller ID to filenames for incoming calls (Android 10+ only) (Issue: #3, PR: #13, @chenxiaolong)
* Fix filename timestamps to match the call log exactly (Issue: #3, PR: #12, @chenxiaolong)
* The about link in the app now links to the exact commit the version was built from (PR: #15, @chenxiaolong)
* Add support for Magisk's built-in module updater (PR: #16, @chenxiaolong)

Non-user-facing changes:

* Update gradle and Android gradle plugin dependencies (PR: #9, @chenxiaolong)
* Add git commit to version number for debug builds (PR: #14, @chenxiaolong)
* Ensure custom gradle tasks (`moduleProp`, `permissionsXml`, `zip`, and `updateJson`) rebuild when input variables (eg. git commit) change (PR: #17, @chenxiaolong)

### Version 1.1

* Target Android SDK 32. BCR was previously targeting the Tiramisu (33) preview SDK, which made it not installable on stable Android versions. (Issue: #1, PR: #2, @chenxiaolong)

### Version 1.0

* Initial release
