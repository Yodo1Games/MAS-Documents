# Android升级指引

#### 1. 删除旧SDK

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

##### v4提供了更加规范的的API，请参考以下对照表进行修改:


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
