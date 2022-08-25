# Android Questions 

## What platform architectures are supported?

MAS supports various platform architectures. Please configure your game's architecture in the project under the label `defaultConfig` in the `build.gradle` file as required by the app. Avoid exceptions caused by using unnecessary platform architectures.

Example:

```groovy
defaultConfig { 
     ndk { 
          abiFilters "x86", "armeabi" 
     } 
}
```

## How can you address the issue of Android DEX 64K Methods Limit?

Android has a 64K method constraint. Since the game will include third-party libraries (including the MAS SDK), the opportunity to add all method sizes will exceed the limit. When your app and the libraries it references exceed 65,536 methods, you can click [here](https://developer.android.com/studio/build/multidex) to see how to enable multidex for apps with over 64K methods.

## What is the minimum Android API version supported by MAS?

MAS SDK supports Android API version 21+.

## What is the cause of the error below during testing with our demo?

```java
 NO FILL received: 
..ID: "3ffe33014bc836be" 
..SDK KEY: "xcGD2fy-GdmiZQapx_kUSy5SMKyLoXBk8RyB5u9MVv34KetGdbl4XrXvAUFy0Qg9scKyVTI0NM4i_yzdXih4XE" 
..PACKAGE NAME: "com.yodo1.ads.demo.gp" ..Reason: [{"code":1008,"msg":"Ad unit info must include the adunit ID - please double-check that your package name \/ bundle id matches the one defined in the MAX Ad Unit ID being used"},{"code":1009,"msg":"Ad unit info must include the ad format - please double-check that your package name / bundle id matches the one defined in the MAX Ad Unit ID being used"}]
Copy
```

This issue is caused by an incorrect package name. MAS includes many networks and most of them have a bundle-id verification mechanism. You have to use the real package name from your app to get live ads.




