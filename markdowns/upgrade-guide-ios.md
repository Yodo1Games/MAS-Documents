# iOS升级指引

#### 1. 删除旧SDK

v3.13.0及以下请删除以下目录:

- Yodo1Ads

> 具体目录请根据自己的实际情况而定

v3.14.0请删除`Podfile`文件中的以下内容:

- `pod 'MasSdk/MasSdk_iOS', "3.14.0"`

#### 2. 添加新SDK

修改`Podfile`文件：

```shell
use_frameworks!
source 'https://github.com/CocoaPods/Specs.git'  # recommend: source 'https://cdn.cocoapods.org/'
source 'https://github.com/Yodo1Games/MAS-Spec.git'
source 'https://github.com/Yodo1Games/Yodo1Spec.git'

pod 'FBSDKCoreKit' # If you have introduced FBSDKCoreKit, please ignore
pod 'Yodo1MasSDK', '~> 4.0.0.3'
```

终端内执行:

```shell
pod update
```

> 请使用`Cocoapods 1.8`及以上版本

具体集成步骤请参考[文档](https://github.com/Yodo1Games/MAS-Documents/blob/upgrade-guide/markdowns/integration-ios.md#12-import-the-ios-sdk-into-the-project)

#### 3.方法修改

##### v4提供了更加规范的的API，请参考以下对照表进行修改:

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

