# 升级指引

#### 1. 删除旧SDK

##### Unity

请删除以下目录:

- Assets/Plugins/iOS/Yodo1Ads
- Assets/Plugins/Android/Yodo1Ads
- Assets/Yodo1Ads

#### iOS

v3.13.0及以下请删除以下目录:

- Yodo1Ads

> 具体目录请根据自己的实际情况而定

v3.14.0请删除`Podfile`文件中的以下内容:

- `pod 'MasSdk/MasSdk_iOS', "3.14.0"`

#### Android

请删除`project`级别`build.gradle`文件中的以下内容:

```groovy
maven { url "https://applovin.bintray.com/Android-Adapter-SDKs" }
maven { url "https://chartboostmobile.bintray.com/Chartboost" }
maven { url "http://dl.appnext.com/" }
maven { url "https://fyber.bintray.com/marketplace" }
maven { url "https://dl.bintray.com/mintegral-official/mintegral_ad_sdk_android_for_oversea" }
```

请删除`app`级别`build.gradle`文件中的以下内容：

```groovy
implementation 'com.google.android.gms:play-services-base:16.+'
implementation 'com.google.android.gms:play-services-ads-identifier:16.+'
implementation 'com.google.android.gms:play-services-basement:16.+'
implementation 'com.yodo1:advert-gp:3.14.0'
```

#### 2. 添加新SDK

#### Unity

- 下载最新的[Unity Plugin](https://docs.yodo1.com/download/Rivendell-SDKs/Rivendell-4.0.0.3.unitypackage)

- 双击打开插件并导入

具体集成步骤请参考[文档](https://github.com/Yodo1Games/MAS-Documents/blob/main/markdowns/integration-unity.md#the-integration-steps)

#### iOS

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

具体集成步骤请参考[文档](https://github.com/Yodo1Games/MAS-Documents/blob/upgrade-guide/markdowns/integration-ios.md#12-import-the-ios-sdk-into-the-project)

#### Android

修改`project`级别`build.gradle`文件，替换成以下内容:

```groovy
maven { url "https://dl.bintray.com/ironsource-mobile/android-sdk" }
maven { url "https://dl.bintray.com/ironsource-mobile/android-adapters" }
maven { url "https://dl.bintray.com/yodo1/MAS-Android" }
maven { url "https://dl.bintray.com/yodo1/android-sdk" }
```

修改`app`级别`build.gradle`文件，替换成以下内容：

```groovy
implementation 'com.yodo1.mas:google:4.0.0.3'
```

具体集成步骤请参考[文档](https://github.com/Yodo1Games/MAS-Documents/blob/upgrade-guide/markdowns/integration-android.md#the-integration-steps)

#### 3.方法修改

目前我们提供两种方案:过渡，完整

过渡：尽可能的保留之前的方法，改动量少，提供最基本的功能

完整：改动大，提供完整的功能

##### Unity

v3.13.0及以下到v4.+

v3.14.0到v4.+，修改内容如下：

将所有的`Yodo1U3dAdsSDK`替换为`Yodo1U3dSDK`，例如:

```objc
// Yodo1U3dAdsSDK.setBannerdDelegate((Yodo1U3dAdsConstants.AdEvent adEvent, string error) 替换为
Yodo1U3dSDK.setBannerdDelegate((Yodo1U3dAdsConstants.AdEvent adEvent, string error)
                               
// Yodo1U3dAdsSDK.setInterstitialAdDelegate((Yodo1U3dAdsConstants.AdEvent adEvent, string error) 替换为
Yodo1U3dSDK.setInterstitialAdDelegate((Yodo1U3dAdsConstants.AdEvent adEvent, string error)
                               
// Yodo1U3dAdsSDK.setRewardVideoDelegate((Yodo1U3dAdsConstants.AdEvent adEvent, string error) 替换为
Yodo1U3dSDK.setRewardVideoDelegate((Yodo1U3dAdsConstants.AdEvent adEvent, string error)
```

>  `Yodo1U3dAds` 及 `Yodo1U3dSDK` 所有方法已被废弃，请开发者参考最新的[集成文档]( https://github.com/Yodo1Games/MAS-Documents/blob/main/markdowns/integration-unity.md)进行修改

**重要**:

- Yodo1U3dAdsConstants.AdEvent.AdEventClick 事件已被废弃，在v4.+版本不再被回调

##### iOS

```objc
// #import "Yodo1Ads.h" 替换为
#import <Yodo1MasCore/Yodo1Ads.h>
```

**重要**：

- Yodo1AdsEventClick 事件已被废弃，在v4.+版本不再被回调

##### Android

```java
// import com.yodo1.advert.open.Yodo1Advert; 替换为
import com.yodo1.mas.ads.Yodo1Advert;
```

**重要**：

以下方法已被废弃, 在v4.+版本不再被回调

- `BannerCallback.onBannerClicked()`
- `InterstitialCallback.onInterstitialClicked()`
- `VideoCallback.onVideoClicked()`



### Unity方法更新

| v4.+                             |  v3.13.0                        | v3.14.0                           |
|:------------------------------  |  :--------------------------  | :------------------------------|
| **Yodo1U3dMas.InitializeSdk();** |  Yodo1U3dAds.InitializeSdk();   | Yodo1U3dAds.InitializeSdk();      |
| **Yodo1U3dMas.SetInitializeDelegate** |  |  |
| **Yodo1U3dMas.SetBannerAdDelegate** |  Yodo1U3dSDK.setBannerdDelegate | **Yodo1U3dAdsSDK.setBannerdDelegate** |
| bool isLoaded = **Yodo1U3dMas.IsBannerAdLoaded();** |  bool isReady = Yodo1U3dAds.BannerIsReady();  | bool isReady = Yodo1U3dAds.BannerIsReady(); |
| **Yodo1U3dMas.ShowBannerAd();** |  Yodo1U3dAds.ShowBanner();  | Yodo1U3dAds.ShowBanner();  |
| **Yodo1U3dMas.SetInterstitialAdDelegate** |  Yodo1U3dSDK.setInterstitialAdDelegate  |  **Yodo1U3dAdsSDK.setInterstitialAdDelegate** |
| bool isLoaded = **Yodo1U3dMas.IsInterstitialAdLoaded();** |  bool isReady = Yodo1U3dAds.InterstitialIsReady();  | bool isReady = Yodo1U3dAds.InterstitialIsReady(); |
| **Yodo1U3dMas.ShowInterstitialAd();** |  Yodo1U3dAds.ShowInterstitial()  |  Yodo1U3dAds.ShowInterstitial(); |
| **Yodo1U3dMas.SetRewardedAdDelegate** |  Yodo1U3dSDK.setRewardVideoDelegate  |   **Yodo1U3dAdsSDK.setRewardVideoDelegate** |
| bool isLoaded = **Yodo1U3dMas.IsRewardedAdLoaded();** |  bool isReady = Yodo1U3dAds.VideoIsReady();  |  bool isReady = Yodo1U3dAds.VideoIsReady(); |
| **Yodo1U3dMas.ShowRewardedAd();** |  Yodo1U3dAds.ShowVideo()  |  Yodo1U3dAds.ShowVideo();  |

### Android方法更新


| v4.+                             |  v3.13.0/v3.14.0               |
| :-----------------------------  |  :----------------------------  |
| **Yodo1Mas.getInstance().init(Activity activity, String appId);** | Yodo1Advert.initSDK(activity, appKey); |
| **Yodo1Mas.getInstance().init(Activity activity, String appId, InitListener listener);** |  |
| **Yodo1Mas.getInstance().setGDPR(userConsent);** | Yodo1Advert.setUserConsent(consent) |
|**Yodo1Mas.getInstance().isGDPRUserConsent();**||
| **Yodo1Mas.getInstance().setCOPPA(ageRestricted);** | Yodo1Advert.setTagForUnderAgeOfConsent(underAgeOfConsent) |
|**Yodo1Mas.getInstance().isCOPPAAgeRestricted();**||
| **Yodo1Mas.getInstance().setCCPA(doNotSell);** | Yodo1Advert.setDoNotSell(doNotSell) |
|**Yodo1Mas.getInstance().isCCPADoNotSell();**||
| **Yodo1Mas.getInstance().setBannerListener** |   |
| **Yodo1Mas.getInstance().showBannerAd(activity, align);** | Yodo1Advert.setBannerAlign(activity, align); |
| boolean isLoaded = **Yodo1Mas.getInstance().isBannerAdLoaded();** |  boolean isReady = Yodo1Advert.bannerIsReady(activity);  |
| **Yodo1Mas.getInstance().showBannerAd(activity);** |  Yodo1Advert.showBanner(activity, callback);  |
|**Yodo1Mas.getInstance().showBannerAd(activity, placement);**|Yodo1Advert.showBanner(activity, placementId,  callback)|
|**Yodo1Mas.getInstance().dismissBannerAd();**|Yodo1Advert.hideBanner(activity)|
|**Yodo1Mas.getInstance().dismissBannerAd(true);**|Yodo1Advert.removeBanner(activity)|
| **Yodo1Mas.getInstance().setInterstitialListener** |    |
| boolean isLoaded = **Yodo1Mas.getInstance().isInterstitialAdLoaded();** |  boolean isReady = Yodo1Advert.interstitialIsReady(activity);  |
| **Yodo1Mas.getInstance().showInterstitialAd(activity);** |  Yodo1Advert.showInterstitial(activity, callback);  |
|**Yodo1Mas.getInstance().showInterstitialAd(activity, placement);**|Yodo1Advert.showInterstitial(activity, placementId,  callback)|
| **Yodo1Mas.getInstance().setRewardListener** |    |
| boolean isLoaded = **Yodo1Mas.getInstance().isRewardedAdLoaded();** |  boolean isReady = Yodo1Advert.videoIsReady(activity);  |
| **Yodo1Mas.getInstance().showRewardedAd(Activity activity);** |  Yodo1Advert.showVideo(activity, callback);  |
|**Yodo1Mas.getInstance().showRewardedAd(activity, placement);**|Yodo1Advert.showVideo(activity, placementId,  callback)|

### iOS方法更新

|    v4.+                             | v3.13.0/v3.14.0                 |
| :---------------------- | :----------------------------- |
| **[[Yodo1Mas sharedInstance] initWithAppId: successful: fail:];** | [Yodo1Ads initWithAppKey: appKey];                      |
|       **[Yodo1Mas sharedInstance].isGDPRUserConsent**        | [Yodo1Ads setUserConsent:consent];                      |
|       **[Yodo1Mas sharedInstance].isGDPRUserConsent**        | [Yodo1Ads isUserConsent];                               |
|      **[Yodo1Mas sharedInstance].isCOPPAAgeRestricted**      | [Yodo1Ads setTagForUnderAgeOfConsent:isBelowConsentAge] |
|      **[Yodo1Mas sharedInstance].isCOPPAAgeRestricted**      | [Yodo1Ads isTagForUnderAgeOfConsent];                   |
|        **[Yodo1Mas sharedInstance].isCCPADoNotSell**         | [Yodo1Ads setDoNotSell:doNotSell]                       |
|        **[Yodo1Mas sharedInstance].isCCPADoNotSell**         | [Yodo1Ads isDoNotSell];                                 |
|        **[Yodo1Mas sharedInstance].bannerAdDelegate**        | [Yodo1Ads setBannerCallback:callback];                  |
| **[[Yodo1Mas sharedInstance] showBannerAdWithAlign:align];** | [Yodo1Ads setBannerAlign:align];                        |
| **[[Yodo1Mas sharedInstance] showBannerAdWithAlign:align offset:offset];** | [Yodo1Ads setBannerOffset:point];                       |
| BOOL isLoaded = **[[Yodo1Mas sharedInstance] isBannerAdLoaded];** | BOOL isLoaded = [Yodo1Ads bannerIsReady];               |
|        **[[Yodo1Mas sharedInstance] showBannerAd];**         | [Yodo1Ads showBanner];                                  |
| **[[Yodo1Mas sharedInstance] showBannerAdWithPlacement:placement];** | [Yodo1Ads showBanner:placement_id];                     |
|       **[[Yodo1Mas sharedInstance] dismissBannerAd];**       | [Yodo1Ads hideBanner];                                  |
| **[[Yodo1Mas sharedInstance] dismissBannerAdWithDestroy:YES];** | [Yodo1Ads removeBanner];                                |
|     **[Yodo1Mas sharedInstance].interstitialAdDelegate**     | [Yodo1Ads setInterstitialCallback:callback];            |
| BOOL isLoaded =**[[Yodo1Mas sharedInstance] isInterstitialAdLoaded];** | BOOL isLoaded = [Yodo1Ads interstitialIsReady];         |
|     **[[Yodo1Mas sharedInstance] showInterstitialAd];**      | [Yodo1Ads showInterstitial];                            |
| **[[Yodo1Mas sharedInstance] showInterstitialAdWithPlacement:placement];** | [Yodo1Ads showInterstitialWithPlacement:placement_id];  |
| **[[Yodo1Mas sharedInstance] showInterstitialAd];** | [Yodo1Ads showInterstitial:viewcontroller]; |
| **[[Yodo1Mas sharedInstance] showInterstitialAdWithPlacement:placement];** | [Yodo1Ads showInterstitial:viewcontroller placement:placement]; |
|        **[Yodo1Mas sharedInstance].rewardAdDelegate**        | [Yodo1Ads setVideoCallback:callback];                   |
| BOOL isLoaded =**[[Yodo1Mas sharedInstance] isRewardAdLoaded];** | BOOL isLoaded = [Yodo1Ads videoIsReady];                |
|        **[[Yodo1Mas sharedInstance] showRewardAd];**         | [Yodo1Ads showVideo];                                   |
| **[[Yodo1Mas sharedInstance] showRewardAdWithPlacement:placement];** | [Yodo1Ads showVideoWithPlacement:placement_id];         |
| **[[Yodo1Mas sharedInstance] showRewardAd];** | [Yodo1Ads showVideo:viewcontroller]; |
| **[[Yodo1Mas sharedInstance] showRewardAdWithPlacement:placement];** | [Yodo1Ads showVideo:viewcontroller placement:placement]; |



## Ad Event更新

#### Unity Ad Event更新

**重要!**`AdEventClick` 事件已在4.0.0.0及以上版本废弃

| v3.13.0/v3.14.0                              | v4.+                                   |
| -------------------------------------------- | -------------------------------------- |
| Yodo1U3dConstants.AdEvent.AdEventShowFail    | **Yodo1.MAS.Yodo1U3dAdEvent.AdError**  |
| Yodo1U3dConstants.AdEvent.AdEventShowSuccess | **Yodo1.MAS.Yodo1U3dAdEvent.AdOpened** |
| Yodo1U3dConstants.AdEvent.AdEventClose       | **Yodo1.MAS.Yodo1U3dAdEvent.AdClosed** |
| Yodo1U3dConstants.AdEvent.AdEventFinish      | **Yodo1.MAS.Yodo1U3dAdEvent.AdReward** |
| Yodo1U3dConstants.AdEvent.AdEventClick       |                                        |
