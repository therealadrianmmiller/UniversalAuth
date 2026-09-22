# UniversalAuth
This project aims to bring a variety of custom authentication options to various Android ROMs.

**Your phone needs to have Xposed (or EdXposed/Lsposed).**

***Please read next section carefully***

- **This project was originally created by **@null-dev** for use on Android 11/12. It may work in Android 10 though.**

- **This project was then forked by **@cubewhy** who added hooks, recievers & patches for Android 14/15 and Lineage**

- **In September 2026, Google changed a biometric class in Android 17 (when the same class was unchanged in previous ROM in July) and broke it, which is when i forked it and stumbled my way through fixing it as a newb to coding, compiling and building APK's (with some help from AI). I contacted @cubewhy with updates, but he was no longer using it and unable to test so i can only confirm this works for post-September stock Android 17, which i used and tested it on.**

- **My version adds logging (via XposedBridge) and is visible via Lspoded Manager if theres issues OR another change by Google to the biometric class**

-  **An alternate fork, which is patched as far as Android 16, and combines the 2 separate APKS (app and lsposed module) into one is available here: https://github.com/Aba114514/UniversalAuth  - I had no way to contact the user and notify of the changes id made, so hopefully he updates his version for Android 17.**

- **This continues to work in Legacy mode in LSposed at time of writing, when running LSposed 2.x builds.**

- **Note: When i forked @cubewhy's repo i made all the external dependencies local, and gradle/etc changes reflect this. The project will build as at time of writing, and i built and created APK the EASY way by forking and using the method in this repo https://github.com/ni554n/apk-builder-action - thanks @ni554n**



**You currently cannot use this project to authenticate in apps. It can only unlock your lockscreen.** Support for using this project to authenticate in apps is under development/investigation.

![Face unlock demo](https://github.com/therealadrianmmiller/UniversalAuth/blob/master/branding/face-unlock.gif)

## Authentication modules
Currently available authentication modules:
- [Face unlock](#face-unlock)

### Face unlock
Face unlock allows you to unlock your phone with your face.

The face unlock module depends on closed source, proprietary libraries developed by Megvii (APK linked below in steps - do NOT install separately)

#### Installation
1. Install and enable the UniversalAuth Xposed module, and install the Face Unlock APK. You can download them from [the releases page](https://github.com/therealadrianmmiller/UniversalAuth/releases).
2. Download the required Motorola Face Unlock APK (01.03.0312) [here](https://www.apkmirror.com/apk/motorola-mobility-llc/motorola-face-unlock-6/motorola-face-unlock-6-01-03-0312-release/motorola-face-unlock-6-01-03-0312-android-apk-download/) 
3. Reboot to make sure the Xposed module is enabled.
4. Launch "Face unlock"
5. Manually install the **com.motorola.faceunlock_01.03.0312** APK downloaded previously in Step 2
6. Grant the app permission to unlock your phone when asked.
7. Enable the accessibility service when asked.
8. Press the "START SETUP" button to enroll your face. The app will ask you to grant it camera permissions, make sure to select "allow while using the app" if that option is available.
9. Lock your phone and test that you are able to use face unlock!

#### In use notes

There may be delays before face scan starts, these are the most common reasons, in order, and not something attributable to code:
- Camera warm-up. The face app's camera has to initialize from cold each time; this varies run to run and isn't something the module controls.
- The trigger method itself firing late. KeyguardUpdateMonitor calls updateFaceListeningState from several places (screen on, keyguard visibility change, doze changes), and on some builds it's debounced or delayed slightly by the system.
- Thermal or Doze throttling, especially if the lag is worse after the phone's been idle for a while.

# Credits
Thanks to:

- the PixelExperience devs for writing the core UI and face unlock logic code.
- The LsPosed/EdXposed devs and rovo89 for Xposed.
- topjohnwu for Magisk.
- Google for AOSP.
