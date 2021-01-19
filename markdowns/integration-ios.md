# iOS Integration
>* iOS14 requires `Xcode 12+`. Please make sure you are using the latest version of Xcode.
>* MAS supports iOS 9.0 and above
>* The easiest way is to use `cocoaPods`, If you are just starting out with 'CocoaPods', please refer to its [official documentation](https://guides.cocoapods.org/using/using-cocoapods) to study how to create and use it `Podfile`

## The Integration Steps
### 1. Add iOS SDK to your project
#### 1.1 Create the `Podfile` file

Create the `Podfile` file in the project root directory

```ruby
touch Podfile
```

#### 1.2 Import the iOS SDK into the project
Please open the project's `Podfile` file and add the following code to the target of the application:

```ruby
source 'https://github.com/Yodo1Games/MAS-Spec.git'

pod 'Yodo1MasSDK', '~> 0.0.0.7-beta'
```

Execute the following command in `Terminal` :

```ruby
pod install --repo-update
```

### 2. Xcode project configuration
#### 2.1 iOS9 `App Transport Security (ATS)` Settings

Apple has added in controls for ATS in iOS9. To ensure uninterrupted ad delivery across all Mediation Networks, it’s important to make these changes to your `info.plist`.

* Add a dictionary and name it `NSAppTransportSecurity`.
* Inside this dictionary, add a Boolean named `NSAllowsArbitraryLoads` and set it to YES.

You may edit the `info.plist` file using the `Open As Source Code` and add the code below to the file. Such as:

``` xml
<key>NSAppTransportSecurity</key> 
<dict> 
    <key>NSAllowsArbitraryLoads</key> 
    <true/> 
</dict>
```

#### 2.2 iOS14 `AppTrackingTransparency(ATT)` Settings

**User tracking instructions**

iOS 14 requires publishers to obtain permission to track user devices across applications. Follow these steps to complete the process.

* Using the Xcode project navigator, select `Info.plist`.
* Click the add button (+) next to any key in the property list editor and create a new property key.
* Enter the key name - `NSUserTrackingUsageDescription`.
* Choose a string value type.
* Enter the app tracking transparency message in the value field.
* Personalized ads are delivered using this identifier. For example:
```xml
<key>NSUserTrackingUsageDescription</key>
<string>This identifier will be used to deliver personalized ads to you.</string>
```

For more information about `NSUserTrackingUsageDescription`, check Apple's developer [documentation](https://developer.apple.com/documentation/bundleresources/information_property_list/nsusertrackingusagedescription). 

For multi-language localizations, check Apple's developer [documentation](https://developer.apple.com/documentation/xcode/localization/adding_support_for_languages_and_regions).

**Advertising Network ID**

Games for users running iOS 14 or later need to include the network ID of each advertising platform in the attribute list file (`Info.plist`):

* Under the Xcode project navigator, select `Info.plist`.
* Click the add button (+) next to any key in the property list editor and create a new property key.
* Enter the key name - `SKAdNetworkItems`.
* For value type, choose `Array`.
* Use the key and each advertising platform network ID string to add the dictionary to the array.

For more information about editing the property list, check Xcode's [documentation](https://help.apple.com/xcode/mac/current/#/dev3f399a2a6%C2%A0).

The following shows the array of dictionaries you need to access the SDK.

```
<key>SKAdNetworkItems</key>
<array>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>cstr6suwn9.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>4DZT52R2T5.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>SU67R6K2V3.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>4PFYVQ9L8R.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>ludvb6z3bs.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>KBD757YWX3.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>F38H382JLK.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>4FZDC2EVR5.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>2U9PT9HC89.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>WZMMZ9FP6W.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>t38b2kh725.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>9T245VHMPL.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>7UG5ZH24HU.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>M8DBW4SV7C.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>mlmmfzh3r3.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>TL55SBB4FM.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>YCLNXRL5PM.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>hs6bdukanm.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>av6w8kgt66.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>8s468mfl3y.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>prcb7njmu6.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>4468km3ulz.skadnetwork</string>
  </dict>
  <dict>
    <key>SKAdNetworkIdentifier</key>
    <string>9RD848Q2BZ.skadnetwork</string>
  </dict>
</array>
```

#### 2.4 Disable `BitCode`
Ensure that all mediation networks work properly by disabling bitcode.

<img src="./../resource/ios-bitcode-disable.png" style="zoom:50%;" />

#### 2.5 Add AdMob App ID
* Add `GADApplicationIdentifier` with `String` type to your project's `info.plist` file.
* You may edit the `info.plist` file and add `GADApplicationIdentifier` to it by using the `Open As Source Code` option.

``` xml
<key>GADApplicationIdentifier</key> 
<string>Your MAS AdMob App ID</string>
```

### 3. Comply With Necessary Legal Framework
Please comply with all legal frameworks that apply to your game and its users. You can find references to the major legal frameworks and details about how to comply with them while using MAS through these links:

* [GDPR](privacy-gdpr.md)
* [COPPA](privacy-coppa.md)
* [CCPA](privacy-ccpa.md)

<font color=red>IMPORTANT!</font> Failure to comply with these frameworks can lead to **Apple App Store and/or Google Play Store rejecting** your game, as well as a negative impact of your game's monetization.

### 4. Initialize the SDK
#### 4.1 Import header file `Yodo1Mas.h`
``` obj-c
#import <Yodo1MasCore/Yodo1Mas.h>
```

#### 4.2 Add the snippet below by using your AppDelegate's `didFinishLaunchingWithOptions` method:

``` obj-c
[[Yodo1Mas sharedInstance] initWithAppId:@"你的AppId" successful:^{
    
} fail:^(NSError * _Nonnull error) {
    
}];
```

## Interstitial Integration
### 1. Set the interstitial ad delegate method
``` obj-c
[Yodo1Mas sharedInstance].bannerAdDelegate = self; 

#pragma mark - Interstitial Delegate
- (void)onAdOpened:(Yodo1MasAdEvent *)event {
    
}

- (void)onAdClosed:(Yodo1MasAdEvent *)event {
    
}

- (void)onAdError:(Yodo1MasAdEvent *)event error:(Yodo1MasError *)error {
    
}       
```

### 2. Check the loading status of interstitials
``` obj-c
BOOL isLoaded = [[Yodo1Mas sharedInstance] isInterstitialAdLoaded];
```

### 3. Show interstitial ad
```obj-c
[[Yodo1Mas sharedInstance] showInterstitialAd];
```

## Rewarded Video Integration
### 1. Set up rewarded video ad delegate methods
``` obj-c
[Yodo1Mas sharedInstance].rewardAdDelegate = self;

#pragma mark - Yodo1MasAdDelegate
- (void)onAdOpened:(Yodo1MasAdEvent *)event {
    
}

- (void)onAdClosed:(Yodo1MasAdEvent *)event {
    
}

- (void)onAdvertError:(Yodo1MasAdEvent *)event error:(Yodo1MasError *)error {
    
}

#pragma mark - Ad Rewarded
- (void)onAdRewardEarned:(Yodo1MasAdEvent *)event {
    
}
```

### 2. Check the loading status of rewarded video ads
``` obj-c
BOOL isLoaded = [[Yodo1Mas sharedInstance] isRewardAdLoaded];
```

### 3. Show rewarded video ads
```obj-c
[[Yodo1Mas sharedInstance] showRewardAd]
```

## Banner Integration
### 1. Set up the banner ad delegate method
``` obj-c
[Yodo1Mas sharedInstance].bannerAdDelegate = self;

#pragma mark - Yodo1MasAdDelegate
- (void)onAdOpened:(Yodo1MasAdEvent *)event {
    
}

- (void)onAdClosed:(Yodo1MasAdEvent *)event {
    
}

- (void)onAdvertError:(Yodo1MasAdEvent *)event error:(Yodo1MasError *)error {
    
}
```

### 2. Check the loading status of banners
```obj-c
BOOL isLoaded = [[Yodo1Mas sharedInstance] isBannerAdLoaded];
```

### 3. Show banner ad
```obj-c
[[Yodo1Mas sharedInstance] showBannerAd];
```

### 4. Dismiss banner ad
```obj-c
[[Yodo1Mas sharedInstance] dismissBannerAd];
```

## Advanced Settings
### Ad Placements
> MAS SDK gives you the ability to set a placement name(e.g. MainMenu, Upgrade_Level etc)。

Below are code snippets on how to set placements for banners, interstitials, and rewarded ads.

**Interstitial Ads**</br>
```obj-c
[[Yodo1Mas sharedInstance] showInterstitialAd:@"MY_INTERSTITIAL_PLACEMENT"]
```

**Rewarded Video Ads**</br>
```obj-c
[[Yodo1Mas sharedInstance] showRewardAd:@"MY_REWARDED_PLACEMENT"]
```

**Banner Ads**</br>
```obj-c
[[Yodo1Mas sharedInstance] showBannerAd:@"MY_BANNER_PLACEMENT"]
```

## Changelog
|  Version   | Release Date | Notes |
|  --------  | ------------ | ------------  |
|            |              |               |
|            |              |               |
