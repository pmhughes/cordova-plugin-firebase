[![Build Status](https://travis-ci.org/freefiona85/cordova-plugin-firebase.svg?branch=master)](https://travis-ci.org/freefiona85/cordova-plugin-firebase) [![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/freefiona85/cordova-plugin-firebase/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/freefiona85/cordova-plugin-firebase/?branch=master)

# cordova-plugin-firebase - Fio's fork (Updated 28 October 2019)
This plugin brings push notifications, analytics, event tracking, crash reporting and more from Google Firebase to your Cordova project!  Android and iOS supported. This fork built specifically for Phonegap Build (PGB) Straight (it may have dependency clash with other plugins/incompatibilities, though.).

There's few features that's disabled due to incompatibilities to how Firebase now works :
- getByteArray for remote config on android (they changed the whole process completely on Firebase)
- get and set remote config (same as above - they changed how things works)
- IncrementCounter (we can implement our own version)

## Supported Cordova Versions
- cordova: `>= 8.0.0`
- cordova-android: `>= 7.1.0`
- cordova-ios: `>= 4.5.4`

Suggested to use Adobe Phonegap Build with CLI 9.0.0 as Firebase needs newest dependencies in PGB.

## Installation
Install the plugin by adding it to your project's config.xml:
```
<plugin spec="https://github.com/freefiona85/cordova-plugin-firebase" />

```

or by running 
```
cordova plugin add https://github.com/freefiona85/cordova-plugin-firebase --save
```

### Setup
Download your Firebase configuration files, GoogleService-Info.plist for iOS and google-services.json for android, and place them in the root folder of your cordova project.  Check out this [firebase article](https://support.google.com/firebase/answer/7015592) for details on how to download the files.

```
- My Project/
    platforms/
    plugins/
    www/
    config.xml
    google-services.json       <--
    GoogleService-Info.plist   <--
    ...
```

###### IMPORTANT NOTES
- This plugin uses a hook (after prepare) that copies the configuration files to the right place, namely `platforms/ios/\<My Project\>/Resources` for ios and `platforms/android` for android.
- Firebase SDK requires the configuration files to be present and valid, otherwise your app will crash on boot or Firebase features won't work.

### PhoneGap Build
Hooks do not work with PhoneGap Build. This means you will have to manually make sure the configuration files are included. 

One way to do that is to make a private fork of this plugin and replace the placeholder config files (see `src/ios` and `src/android`) with your actual ones, as well as hard coding your app id and api key in `plugin.xml`.

For newer Cordova version, you can also put google-services.json and GoogleService-Info.plist on the project root, and add this to your config.xml  :

```
<platform name="android">
        <resource-file src="google-services.json" target="app/google-services.json" />
    </platform>
    <platform name="ios">
        <resource-file src="GoogleService-Info.plist" />
    </platform>
```

### Google Play Services
Your build may fail if you are installing multiple plugins that use Google Play Services.  This is caused by the plugins installing different versions of the Google Play Services library.  This can be resolved by installing [cordova-android-play-services-gradle-release](https://github.com/dpa99c/cordova-android-play-services-gradle-release).

If your build is still failing, you can try installing [cordova-android-firebase-gradle-release](https://github.com/dpa99c/cordova-android-firebase-gradle-release).  For more info, read the following [comment](https://github.com/dpa99c/cordova-plugin-request-location-accuracy/issues/50#issuecomment-390025013) about locking down the specific versions for play services and firebase. It is suggested to use `+` instead of `15.+` to ensure the correct versions are used.

## Google Tag Manager

Checkout our [guide](docs/GOOGLE_TAG_MANAGER.md) for info on setting up Google Tag Manager.

## Configuring Notifications

Checkout our [guide](docs/NOTIFICATIONS.md) for info on configuring notification icons and colors.

## API

See the full [API](docs/API.md) available for this plugin.

## Donation

Donation is not needed, but much appreciated so we can focus on making sure it'll be working on latest Phonegap Build and Firebase release. Google changed a lot of Firebase and their dependencies each time.
```
BTC : 3LGdPBrULnVnZzu4GS2fNAwaXX6mPNz8Cv
```
