# Android upgrade guide

#### 1. Remove old SDK

Please delete the following content in the `build.gradle` file at the `project` level:

```groovy
maven { url "https://applovin.bintray.com/Android-Adapter-SDKs" }
maven { url "https://chartboostmobile.bintray.com/Chartboost" }
maven { url "http://dl.appnext.com/" }
maven { url "https://fyber.bintray.com/marketplace" }
maven { url "https://dl.bintray.com/mintegral-official/mintegral_ad_sdk_android_for_oversea" }
```

Please delete the following content in the `build.gradle` file at the `app` level:

```groovy
implementation 'com.google.android.gms:play-services-base:16.+'
implementation 'com.google.android.gms:play-services-ads-identifier:16.+'
implementation 'com.google.android.gms:play-services-basement:16.+'
implementation 'com.yodo1:advert-gp:3.14.0'
```

#### 2. Add new SDK

Modify the `build.gradle` file of `project` level and replace it with the following content:

```groovy
maven { url "https://android-sdk.is.com" }
maven { url 'https://artifact.bytedance.com/repository/pangle'}
maven { url "https://sdk.tapjoy.com/" }
```

Modify the `build.gradle` file at the `app` level and replace it with the following:

```groovy
implementation 'com.yodo1.mas:full:4.2.0'
```

For specific integration steps, please refer to [Document](integration-android.md#the-integration-steps)

#### 3.Method signature change

##### v4 provides a more standardized API, please refer to the following comparison table to modify:


|  v3.13.0/v3.14.0               | v4.+                             |
|  :----------------------------  | :-----------------------------  |
| Yodo1Advert.initSDK(activity, appKey); | **Yodo1Mas.getInstance().init(Activity activity, String appId);** |
|  | **Yodo1Mas.getInstance().init(Activity activity, String appId, InitListener listener);** |
| Yodo1Advert.setUserConsent(consent) | **Yodo1Mas.getInstance().setGDPR(userConsent);** |
||**Yodo1Mas.getInstance().isGDPRUserConsent();**|
| Yodo1Advert.setTagForUnderAgeOfConsent(underAgeOfConsent) | **Yodo1Mas.getInstance().setCOPPA(ageRestricted);** |
||**Yodo1Mas.getInstance().isCOPPAAgeRestricted();**|
| Yodo1Advert.setDoNotSell(doNotSell) | **Yodo1Mas.getInstance().setCCPA(doNotSell);** |
||**Yodo1Mas.getInstance().isCCPADoNotSell();**|
|   | **Yodo1Mas.getInstance().setBannerListener** |
| Yodo1Advert.setBannerAlign(activity, align); | **Yodo1Mas.getInstance().showBannerAd(activity, align);** |
|  Yodo1Advert.bannerIsReady(activity);  | **Yodo1Mas.getInstance().isBannerAdLoaded();** |
|  Yodo1Advert.showBanner(activity, callback);  | **Yodo1Mas.getInstance().showBannerAd(activity);** |
|Yodo1Advert.showBanner(activity, placementId,  callback)|**Yodo1Mas.getInstance().showBannerAd(activity, placement);**|
|Yodo1Advert.hideBanner(activity)|**Yodo1Mas.getInstance().dismissBannerAd();**|
|Yodo1Advert.removeBanner(activity)|**Yodo1Mas.getInstance().dismissBannerAd(true);**|
|    | **Yodo1Mas.getInstance().setInterstitialListener** |
|  Yodo1Advert.interstitialIsReady(activity);  | **Yodo1Mas.getInstance().isInterstitialAdLoaded();** |
|  Yodo1Advert.showInterstitial(activity, callback);  | **Yodo1Mas.getInstance().showInterstitialAd(activity);** |
|Yodo1Advert.showInterstitial(activity, placementId,  callback)|**Yodo1Mas.getInstance().showInterstitialAd(activity, placement);**|
|    | **Yodo1Mas.getInstance().setRewardListener** |
|  Yodo1Advert.videoIsReady(activity);  | **Yodo1Mas.getInstance().isRewardedAdLoaded();** |
|  Yodo1Advert.showVideo(activity, callback);  | **Yodo1Mas.getInstance().showRewardedAd(Activity activity);** |
|Yodo1Advert.showVideo(activity, placementId,  callback)|**Yodo1Mas.getInstance().showRewardedAd(activity, placement);**|
