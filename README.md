
[![](https://jitpack.io/v/com.vuzix/ultralite-sdk-android.svg)](https://jitpack.io/#com.vuzix/ultralite-sdk-android)

![Vuzix Logo](https://apps.vuzix.com/images/vuzix-logo-old.png)
# Ultralite SDK for Android
Use this library to connect your Android app to the Vuzix Z100™ smart glasses. Easily connect, send notifications, send text, or send images to the glasses display.

## Requirements
- Android device running Android 12 or later
- [Vuzix Connect](https://play.google.com/store/apps/details?id=com.vuzix.connect) app installed
- Vuzix Z100™ smart glasses

## Installation
1. Add JitPack as a maven repository in settings.gradle or settings.gradle.kts at the top level of your Android Studio project:
```
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        ...
        maven { url "https://jitpack.io" } // if using settings.gradle
        maven ("https://jitpack.io")       // if using settings.gradle.kts
    }
}
```
2. Add ultralite-sdk-android to your module's build.gradle or build.gradle.kts file. Replace VERSION below with the version of the SDK you wish to use.
```
dependencies {
    ...
    implementation 'com.vuzix:ultralite-sdk-android:VERSION'   // if using build.gradle
    implementation ("com.vuzix:ultralite-sdk-android:VERSION") // if using build.gradle.kts
    ...
}
```
The latest ultralite-sdk-android version on JitPack is [![](https://jitpack.io/v/com.vuzix/ultralite-sdk-android.svg)](https://jitpack.io/#com.vuzix/ultralite-sdk-android).
## Usage
All interaction with a pair of glasses is done through the UltraliteSDK class. You can obtain an instance of this class with the static `get(Context)` method:
```
@Override
protected void onCreate(@Nullable Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    UltraliteSDK sdk = UltraliteSDK.get(this);
    ...
}
```

The UltraliteSDK class has methods for checking various statuses, such as SDK status, link status, and connection status. These methods return booleans or LiveDatas that can be observed.

The SDK may not be available for immediate use. It's also possible the SDK will become unavailable at some point in the future. Use `isAvailable()` or `getAvailable()` to monitor the state of the SDK. SDK methods will have no effect if called when the SDK is unavailable.

An app that wishes to control the glasses must use `requestControl()`. If there are glasses connected, this request should normally be granted. You should also monitor the control status with either `isControlledByMe()` or `getControlledByMe()`. When another app requests control, your app will be notified that control has been lost. You can also lose control if the connection is broken or if the glasses are unlinked. When control is lost, assume all of your configuration such as layout and canvas state is gone. The next time you gain control, you will have to setup this configuration again.

Once control has been successfully requested, you can use methods such as `setLayout()`, `sendText()` or any of the Canvas methods. Other methods can be called without having control. See [javadoc](https://vuzix.github.io/ultralite-sdk-android/javadoc) for more information.

## Documentation
API level documentation is available in [javadoc](https://vuzix.github.io/ultralite-sdk-android/javadoc).

### Sample App
Sample code showing several example use cases is available [here](https://github.com/Vuzix/ultralite-sdk-android-sample).

## Legal
Use of the SDK is available to developers agreeing to the
[VUZIX® SOFTWARE DEVELOPMENT KIT LICENSE AND CONFIDENTIALITY AGREEMENT](https://www.vuzix.com/pages/vuzix%C2%AE-software-development-kit-license-and-confidentiality-agreement)

