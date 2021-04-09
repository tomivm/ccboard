# Cboard Cordova - AAC communication board with text-to-speech for mobile devices

[![cboard-org](https://circleci.com/gh/cboard-org/ccboard.svg?style=shield)](https://app.circleci.com/pipelines/github/cboard-org/ccboard)

`git clone --recursive git@github.com:nous-/ccboard.git`

This is a Cordova application that wraps the original [Cboard React application](https://github.com/cboard-org/cboard) to bring native mobile and desktop support. The Cboard react app is maintained to support Cordova detection, setup and bindings.

Text-to-speach (TTS) support is provided via [`phonegap-plugin-speech-synthesis`](https://github.com/macdonst/SpeechSynthesisPlugin). This plugin bridges the native operating system TTS functionality to browser app, in a way that mimics [W3C Web Speech API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API): `SpeechSynthesis`. It uses the `android.speech.tts.TextToSpeech` interface on Android.

## Platforms supported: 

1. Android 
1. Electron - Windows

## One-time setup

1. `git submodule update` - Get Cboard app 
1. `npm i`
1. `mkdir -p www` - Make root cordova app folder 
1. `cordova platform add android` -or `cordova platform add electron` - Add Cordova platforms. *`www` folder must be present.*
1. `cd cboard`
1. `npm i`


## Building 

You need to build the react.js app, and after that copy un cordova project:

1. `cd cboard`
1. Release `npm run build` / Debug `npm run build-cordova-debug`
1. `cp -r ./build/* ../www`
1. `cd ..`

## Building and running 

Android: 
 `cordova run android --emulator`

Electron: 

 `cordova build electron --release` For release
 `cordova build electron --debug ` For enable the dev tools
 
## Android Platform
## Generate Release APK

1. Build `cordova build android --release`
1. Copy `cp platforms/android/app/build/outputs/apk/release/app-release-unsigned.apk ccboard.apk`
1. Sign

    1. Generate self-signed keys `keytool -genkey -v -keystore ccboard.keystore -alias ccboard -keyalg RSA -keysize 2048 -validity 100000`
    1. Sign `jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore ccboard.keystore ccboard.apk ccboard`

## Debugging output

For emulator console.log output, you can either run in the debugging under eg. `Android Studio`, or in Chrome, navigate to `chrome://inspect`, and select the remote target that shows up once the emulator starts.

