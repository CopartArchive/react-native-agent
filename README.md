# Instana React Native Agent <a href="https://www.npmjs.com/package/@instana/react-native-agent"><img alt="npm (scoped)" src="https://img.shields.io/npm/v/@instana/react-native-agent?color=0db4b33"></a>

**[Changelog](CHANGELOG.md)** |
**[Contributing](CONTRIBUTING.md)**

---

## Installation

### Node.js Dependency

```
npm install --save @instana/react-native-agent 
```

### Android

Android will require you to take 2 extra steps in order to support automatic tracking of network requests:

Add the Instana Android agent plugin to your dependencies via `android/build.gradle`:

```groovy
buildscript {
    dependencies {
        classpath 'com.instana:android-agent-plugin:1.4.0'
    }
}
```

Apply the Instana Android agent plugin via `android/app/build.gradle` file (at the top):

```groovy
apply plugin: 'com.android.application'
apply plugin: 'com.instana.android-agent-plugin'
```

### iOS

Your project needs to contains at least one Swift file (it can be empty). If you don't have any, please open your Xcode Project in `<YourReactNativeProject>/ios` and add an empty Swift file. Please also let Xcode create the Bridging Header for you.

## Usage

Please refer to our [React Native API documentation](https://docs.instana.io/products/mobile_app_monitoring/react_native_api/).

## Recommendation

We recommend adding `http://localhost:8081` to the ignored URLs list to prevent the Agent from tracing communication with the Metro bundler:

```javascript
Instana.setIgnoreURLsByRegex(["http:\/\/localhost:8081.*"]);
```

## Known Issues

### Android: fetch(url)

If your app uses `fetch` to complete network requests, you might find your app crashing on runtime whenever `fetch` is used after linking Instana React Native Agent : `No virtual method toString(Z)Ljava/lang/String;`  

If you encounter this issue before [the upstream issue is solved](https://github.com/facebook/react-native/issues/28425), please apply the following [workaround](https://github.com/facebook/react-native/issues/27250#issuecomment-573111088). Add the following to your Android module-level gradle file (usually `app/gradle.build`):

```groovy
dependencies {
    implementation "com.squareup.okhttp3:okhttp:4.3.1"
    implementation "com.squareup.okhttp3:okhttp-urlconnection:4.3.1"
}
```
