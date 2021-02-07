# Unity Integration

**Important** Update MAS Rivendell SDK

- To upgrade from an older SDK to MAS SDK v2, you must remove all the contents of the old SDK as following:</br>
 - Assets/Plugins/iOS/Yodo1Ads
 - Assets/Plugins/Android/Yodo1Ads
 - Assets/Yodo1Ads
- We have modified the interface of the new SDK, please carefully refer to the following documents to upgrade

## The Integration Steps

### 1. Download [Unity Plugin 4.0.0.3](https://docs.yodo1.com/download/Rivendell-SDKs/Rivendell-4.0.0.3.unitypackage)
> * MAS supports Unity 2017.4.37f1+ LTS version, 2018.4.30f1+ LTS version, 2019.41f18+ LTS version, 2020 all version and above.
> * [Jetifier](https://developer.android.com/jetpack/androidx/releases/jetifier) is required for Android builds and can be enabled by selecting ***Assets > External Dependency Manager > Android Resolver > Settings > Use Jetifier***
> * `CocoaPods` is required for iOS builds and can be installed following the instructions [here](https://guides.cocoapods.org/using/getting-started.html#getting-started), please use version 1.8 and above.
> * `Xcode12+` is required for iOS14, please make sure your xcode is lastest version.
> * The Unity plugin contains Sample code. The path is `/Assets/Yodo1/MAS/Sample`</br>

Please upgrade to Firebase 7.0.0 and above if you are using Firebase, lower Firebase will not be probably compatible with AdMob since we are using the most updated Admob. According to Admob, Firebase needs to be updated to match the Admob version. And this update will also improve your general SDK integration process for long-term

### 2. Integrate the SDK Into Your Project
Open your Unity project and import the Unity package. Double click the compressed package icon. The files will populate automatically as illustrated below.

<center class="half">
    <img src="./../resource/import-package.png" width="400"/> 
</center>

**Important!** The MAS Unity Plugin is built for Android & iOS platforms. Please run your projects on an Android or iOS device to test ads when the integration is completed.

### 3. Enter Application Information
> MAS provides a configuration wizard for Unity to quickly configure application information. You can access it through `Assets/Yodo1/MAS Settings`.

<center class="half">
    <img src="./../resource/settings-mas.png" width="400"/> 
</center>

#### 3.1 Set Android Configuration

<center class="half">
    <img src="./../resource/settings-android.png" width="400"/> 
</center>

**Important!** Invalid AdMob AppID will cause a crash, please make sure to fetch the AdMob App ID from MAS dashboard

#### 3.2 Set iOS Configuration

<center class="half">
    <img src="./../resource/settings-ios.png" width="400"/> 
</center>

**Important!** Invalid AdMob AppID will cause a crash, please make sure to fetch the AdMob App ID from MAS dashboard

### 4. Support AndroidX
#### 4.1 Look for and click on "Settings" under "Assets".

<center class="half">
    <img src="./../resource/settings-resolver-android.png" width="400"/> 
</center>

#### 4.2 Select `Use Jetifier`.

<center class="half">
    <img src="./../resource/use-jetifier.png" width="400"/> 
</center>

### 5. Comply With Necessary Legal Frameworks
Please comply with all legal frameworks that apply to your game and its users. You can find information on compliance through these links:

* [GDPR](privacy-gdpr.md)
* [COPPA](privacy-coppa.md)
* [CCPA](privacy-ccpa.md)

<font color=red>IMPORTANT!</font> Failure to comply with these frameworks can lead the Apple App Store and/or Google Play Store rejecting your game, as well as a negative impact of your game's monetization.

### 6. Initialize the SDK

#### 6.1 Sets the initialization delegate method
```c#
Yodo1U3dMas.SetInitializeDelegate((bool success, Yodo1U3dAdError error) => {
    if (success){// Initialize successful

    } else { // Initialize failure

    }
});
    
```

#### 6.2 SDK initialization is called in the `Start` method

```c#
void Start()  {
	Yodo1U3dMas.InitializeSdk();
}
```

### 7. AdMob Android Manifest Merging Errors
The AdMob SDK use the `<queries>` element in their bundled Android Manifest files. If you are on an incompatible version of the Android Gradle plugin, you will encounter the following build errors, respectively:

```xml
com.android.builder.internal.aapt.v2.Aapt2Exception: Android resource linking failed
error: unexpected element <queries> found in <manifest>.
```

You will need to upgrade to one of the following versions of the Android Gradle plugin that supports it:

| **Current Android Gradle Plugin Version** | **Supported Android Gradle Plugin Version** |
|  :-------------------------------------:  | :-----------------------------------------: | 
|    4.1.*                                  |            Already Supported                | 
|    4.0.*                                  |            4.0.1                            |   
|    3.6.*                                  |            3.6.4                            |   
|    3.5.*                                  |            3.5.4                            |   
|    3.4.*                                  |            3.4.3                            |   
|    3.3.*                                  |            3.3.3                            |  

To update the Gradle Plugin version to a compatible one, please enable the custom base Gradle template by selecting **Edit > Project Settings > Android tab > Publisher Settings > Custom Base Gradle Template**.

The template will be located at `Assets/Plugins/Android/mainTemplate.gradle` for Unity 2019.2 or below and `Assets/Plugins/Android/baseProjectTemplate.gradle` for Unity 2019.3 or above. Then update the below line with the appropriate version:

```java
classpath com.android.tools.build:gradle:x.x.x
```

If you are on Unity 2017.4 or below, please ensure that you are on at least 2017.4.40 which uses a compatible version of the Gradle Plugin by default.

Detailed steps for different versions of Unity can be found [here](android-manifest-merging-errors-queries.md).

## Interstitial Integration
### 1. Set the interstitial ad delegate method
```c#
Yodo1U3dMas.SetInterstitialAdDelegate((Yodo1U3dAdEvent adEvent, Yodo1U3dAdError error) => {
    Debug.Log("[Yodo1 Mas] InterstitialAdDelegate:" + adEvent.ToString() + "\n" + error.ToString());
    switch (adEvent)
    {
        case Yodo1U3dAdEvent.AdClosed:
            Debug.Log("[Yodo1 Mas] Interstital ad has been closed.");
            break;
        case Yodo1U3dAdEvent.AdOpened:
            Debug.Log("[Yodo1 Mas] Interstital ad has been shown.");
            break;
        case Yodo1U3dAdEvent.AdError:
            Debug.Log("[Yodo1 Mas] Interstital ad error, " + error.ToString());
            break;
    }
});
```
### 2. Check Interstitial Ad Loading Status

```c#
bool isLoaded = Yodo1U3dMas.IsInterstitialAdLoaded();
```

### 3. Show Interstitial Ads

```c#
Yodo1U3dMas.ShowInterstitialAd();
```

## Rewarded Video Ad Integration
### 1. Set the rewarded video ad delegate method
```c#
Yodo1U3dMas.SetRewardedAdDelegate((Yodo1U3dAdEvent adEvent, Yodo1U3dAdError error) => {
    Debug.Log("[Yodo1 Mas] RewardVideoDelegate:" + adEvent.ToString() + "\n" + error.ToString());
    switch (adEvent)
    {
        case Yodo1U3dAdEvent.AdClosed:
            Debug.Log("[Yodo1 Mas] Reward video ad has been closed.");
            break;
        case Yodo1U3dAdEvent.AdOpened:
            Debug.Log("[Yodo1 Mas] Reward video ad has shown successful.");
            break;
        case Yodo1U3dAdEvent.AdError:
            Debug.Log("[Yodo1 Mas] Reward video ad error, " + error);
            break;
        case Yodo1U3dAdEvent.AdReward:
            Debug.Log("[Yodo1 Mas] Reward video ad reward, give rewards to the player.");
            break;
    }

});
```
### 2. Check Rewarded Video Ad Loading Status
```c#
bool isLoaded = Yodo1U3dMas.IsRewardedAdLoaded();
```

### 3. Show Rewarded Video Ad
```c#
Yodo1U3dMas.ShowRewardedAd();
```
## Banner Integration
### 1. Set the banner ad delegate method
```c#
Yodo1U3dMas.SetBannerAdDelegate((Yodo1U3dAdEvent adEvent, Yodo1U3dAdError error) => {
    Debug.Log("[Yodo1 Mas] BannerdDelegate:" + adEvent.ToString() + "\n" + error.ToString());
    switch (adEvent)
    {
        case Yodo1U3dAdEvent.AdClosed:
            Debug.Log("[Yodo1 Mas] Banner ad has been closed.");
            break;
        case Yodo1U3dAdEvent.AdOpened:
            Debug.Log("[Yodo1 Mas] Banner ad has been shown.");
            break;
        case Yodo1U3dAdEvent.AdError:
            Debug.Log("[Yodo1 Mas] Banner ad error, " + error.ToString());
            break;
    }
});
```
### 2. Check Banner Ad Loading Status
```c#
bool isLoaded = Yodo1U3dMas.IsBannerAdLoaded();
```

### 3. Show banner ad
```c#
Yodo1U3dMas.ShowBannerAd();
```

## Advanced Settings
### Ad Placements
> MAS SDK gives you the ability to set a placement name(e.g. MainMenu, Upgrade_Level etc)。

Below are code snippets on how to set placements for banners, interstitials, and rewarded ads.

**Interstitial Ads**</br>

```c#
Yodo1U3dMas.ShowRewardedAd("MY_INTERSTITIAL_PLACEMENT");
```

**Rewarded Video Ads**</br>

```c#
Yodo1U3dMas.ShowInterstitialAd("MY_REWARDED_PLACEMENT");
```

**Banner Ads**</br>

```c#
Yodo1U3dMas.ShowBannerAd("MY_BANNER_PLACEMENT");
```

## Changelog
|  Version   | Release Date | Notes |
|  --------  | ------------ | ------------  |
|            |              |               |
|            |              |               |
