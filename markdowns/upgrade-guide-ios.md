# iOS upgrade guide

#### 1. Remove old SDK

Please delete the following directories for v3.13.0 and below:

- Yodo1Ads

> The specific catalogue depends on your actual situation

v3.14.0 Please delete the following content in the `Podfile` file:

- `pod 'MasSdk/MasSdk_iOS', "3.14.0"`

#### 2. Add new SDK

update `Podfile`：

```shell
use_frameworks!
source 'https://github.com/CocoaPods/Specs.git'  # recommend: source 'https://cdn.cocoapods.org/'
source 'https://github.com/Yodo1Games/MAS-Spec.git'
source 'https://github.com/Yodo1Games/Yodo1Spec.git'

pod 'FBSDKCoreKit' # If you have introduced FBSDKCoreKit, please ignore
pod 'Yodo1MasSDK', '~> 4.0.0.3'
```

Execute in the terminal:

```shell
pod update
```

> Please use `Cocoapods 1.8` and above

For specific integration steps, please refer to [Document](integration-ios.md#12-import-the-ios-sdk-into-the -project)

#### 3. Method signature change

##### v4 provides a more standardized API, please refer to the following comparison table to modify:

| v3.13.0/v3.14.0                 |    v4.+                             |
| :----------------------------- | :---------------------- |
| [Yodo1Ads initWithAppKey: appKey];                      | **[[Yodo1Mas sharedInstance] initWithAppId: successful: fail:];** |
| [Yodo1Ads setUserConsent:consent];                      |       **[Yodo1Mas sharedInstance].isGDPRUserConsent**        |
| [Yodo1Ads isUserConsent];                               |       **[Yodo1Mas sharedInstance].isGDPRUserConsent**        |
| [Yodo1Ads setTagForUnderAgeOfConsent:isBelowConsentAge] |      **[Yodo1Mas sharedInstance].isCOPPAAgeRestricted**      |
| [Yodo1Ads isTagForUnderAgeOfConsent];                   |      **[Yodo1Mas sharedInstance].isCOPPAAgeRestricted**      |
| [Yodo1Ads setDoNotSell:doNotSell]                       |        **[Yodo1Mas sharedInstance].isCCPADoNotSell**         |
| [Yodo1Ads isDoNotSell];                                 |        **[Yodo1Mas sharedInstance].isCCPADoNotSell**         |
| [Yodo1Ads setBannerCallback:callback];                  |        **[Yodo1Mas sharedInstance].bannerAdDelegate**        |
| [Yodo1Ads setBannerAlign:align];                        | **[[Yodo1Mas sharedInstance] showBannerAdWithAlign:align];** |
| [Yodo1Ads setBannerOffset:point];                       | **[[Yodo1Mas sharedInstance] showBannerAdWithAlign:align offset:offset];** |
| [Yodo1Ads bannerIsReady];               | **[[Yodo1Mas sharedInstance] isBannerAdLoaded];** |
| [Yodo1Ads showBanner];                                  |        **[[Yodo1Mas sharedInstance] showBannerAd];**         |
| [Yodo1Ads showBanner:placement_id];                     | **[[Yodo1Mas sharedInstance] showBannerAdWithPlacement:placement];** |
| [Yodo1Ads hideBanner];                                  |       **[[Yodo1Mas sharedInstance] dismissBannerAd];**       |
| [Yodo1Ads removeBanner];                                | **[[Yodo1Mas sharedInstance] dismissBannerAdWithDestroy:YES];** |
| [Yodo1Ads setInterstitialCallback:callback];            |     **[Yodo1Mas sharedInstance].interstitialAdDelegate**     |
| [Yodo1Ads interstitialIsReady];         | **[[Yodo1Mas sharedInstance] isInterstitialAdLoaded];** |
| [Yodo1Ads showInterstitial];                            |     **[[Yodo1Mas sharedInstance] showInterstitialAd];**      |
| [Yodo1Ads showInterstitialWithPlacement:placement_id];  | **[[Yodo1Mas sharedInstance] showInterstitialAdWithPlacement:placement];** |
| [Yodo1Ads showInterstitial:viewcontroller]; | **[[Yodo1Mas sharedInstance] showInterstitialAd];** |
| [Yodo1Ads showInterstitial:viewcontroller placement:placement]; | **[[Yodo1Mas sharedInstance] showInterstitialAdWithPlacement:placement];** |
| [Yodo1Ads setVideoCallback:callback];                   |        **[Yodo1Mas sharedInstance].rewardAdDelegate**        |
| [Yodo1Ads videoIsReady];                | **[[Yodo1Mas sharedInstance] isRewardAdLoaded];** |
| [Yodo1Ads showVideo];                                   |        **[[Yodo1Mas sharedInstance] showRewardAd];**         |
| [Yodo1Ads showVideoWithPlacement:placement_id];         | **[[Yodo1Mas sharedInstance] showRewardAdWithPlacement:placement];** |
| [Yodo1Ads showVideo:viewcontroller]; | **[[Yodo1Mas sharedInstance] showRewardAd];** |
| [Yodo1Ads showVideo:viewcontroller placement:placement]; | **[[Yodo1Mas sharedInstance] showRewardAdWithPlacement:placement];** |

