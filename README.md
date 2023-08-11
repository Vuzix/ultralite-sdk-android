[![](https://jitpack.io/v/com.vuzix/ultralite-sdk-android.svg)](https://jitpack.io/#com.vuzix/ultralite-sdk-android)

# Ultralite SDK for Android
Use this library to send content from your app to any pair of smart glasses made via the Vuzix Ultralite OEM Platform<sup>SM</sup>.

## Requirements
- Android device running Andorid 12 or later
- [Vuzix OEM Platform](https://play.google.com/store/apps/details?id=com.vuzix.ultralite.app) app installed
## Getting Started
1. Add JitPack as a maven repository in settings.gradle or settings.gradle.kts at the top level of your Android Studio project:
```
repositories {
    ...
    maven { url "https://jitpack.io" } // if using build.gradle
    maven ("https://jitpack.io") // if using build.gradle.kts
}
```
2. Add ultralite-sdk-android to your module's build.gradle or build.gradle.kts file. Replace VERSION below with the version of the SDK you wish to use. The latest version is [![](https://jitpack.io/v/com.vuzix/ultralite-sdk-android.svg)](https://jitpack.io/#com.vuzix/ultralite-sdk-android).
```
dependencies {
    ...
    implementation 'com.vuzix:ultralite-sdk-android:VERSION' // if using build.gradle
    implementation ("com.vuzix:ultralite-sdk-android:VERSION") // if using build.gradle.kts
    ...
}
```

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
