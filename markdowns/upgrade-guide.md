# Upgrade Guide

## Method Updates

### Unity Method Updates

|  v3.13.0                        | v3.14.0                           | v4.+                             |
|  -----------------------------  | --------------------------------- | ------------------------------  |
|  Yodo1U3dAds.InitializeSdk();   | Yodo1U3dAds.InitializeSdk();      | **Yodo1U3dMas.InitializeSdk();** |
|  |  | **Yodo1U3dMas.SetInitializeDelegate** |
|  Yodo1U3dSDK.setBannerdDelegate | **Yodo1U3dAdsSDK.setBannerdDelegate** | **Yodo1U3dMas.SetBannerAdDelegate** |
|  bool isReady = Yodo1U3dAds.BannerIsReady();  | bool isReady = Yodo1U3dAds.BannerIsReady(); | bool isLoaded = **Yodo1U3dMas.IsBannerAdLoaded();** |
|  Yodo1U3dAds.ShowBanner();  | Yodo1U3dAds.ShowBanner();  | **Yodo1U3dMas.ShowBannerAd();** |
|  Yodo1U3dSDK.setInterstitialAdDelegate  |  **Yodo1U3dAdsSDK.setInterstitialAdDelegate** | **Yodo1U3dMas.SetInterstitialAdDelegate** |
|  bool isReady = Yodo1U3dAds.InterstitialIsReady();  | bool isReady = Yodo1U3dAds.InterstitialIsReady(); | bool isLoaded = **Yodo1U3dMas.IsInterstitialAdLoaded();** |
|  Yodo1U3dAds.ShowInterstitial()  |  Yodo1U3dAds.ShowInterstitial(); | **Yodo1U3dMas.ShowInterstitialAd();** |
|  Yodo1U3dSDK.setRewardVideoDelegate  |   **Yodo1U3dAdsSDK.setRewardVideoDelegate** | **Yodo1U3dMas.SetRewardedAdDelegate** |
|  bool isReady = Yodo1U3dAds.VideoIsReady();  |  bool isReady = Yodo1U3dAds.VideoIsReady(); | bool isLoaded = **Yodo1U3dMas.IsRewardedAdLoaded();** |
|  Yodo1U3dAds.ShowVideo()  |  Yodo1U3dAds.ShowVideo();  | **Yodo1U3dMas.ShowRewardedAd();** |

### Android Method Updates


|  v3.13.0                        | v3.14.0                           | v4.+                             |
|  -----------------------------  | --------------------------------- | ------------------------------  |
| Yodo1Advert.initSDK(activity, appKey); | Yodo1Advert.initSDK(activity, appKey); | **Yodo1Mas.getInstance().init(Activity activity, String appId);** |
|  |  | **Yodo1Mas.getInstance().init(Activity activity, String appId, InitListener listener);** |
| Yodo1Advert.setUserConsent(consent) |Yodo1Advert.setUserConsent(consent) | **Yodo1Mas.getInstance().setGDPR(userConsent);** |
|||**Yodo1Mas.getInstance().isGDPRUserConsent();**|
| Yodo1Advert.setTagForUnderAgeOfConsent(underAgeOfConsent) |Yodo1Advert.setTagForUnderAgeOfConsent(underAgeOfConsent) | **Yodo1Mas.getInstance().setCOPPA(ageRestricted);** |
|||**Yodo1Mas.getInstance().isCOPPAAgeRestricted();**|
| Yodo1Advert.setDoNotSell(doNotSell) |Yodo1Advert.setDoNotSell(consdoNotSellent) | **Yodo1Mas.getInstance().setCCPA(doNotSell);** |
|||**Yodo1Mas.getInstance().isCCPADoNotSell();**|
|   |  | **Yodo1Mas.getInstance().setBannerListener** |
| Yodo1Advert.setBannerAlign(activity, align); | Yodo1Advert.setBannerAlign(activity, align); | **Yodo1Mas.getInstance().showBannerAd(activity, align);** |
|  boolean isReady = Yodo1Advert.bannerIsReady(activity);  | boolean isReady = Yodo1Advert.bannerIsReady(activity); | boolean isLoaded = **Yodo1Mas.getInstance().isBannerAdLoaded();** |
|  Yodo1Advert.showBanner(activity, callback);  | Yodo1Advert.showBanner(activity, callback); | **Yodo1Mas.getInstance().showBannerAd(activity);** |
|Yodo1Advert.showBanner(activity, placementId,  callback)|Yodo1Advert.showBanner(activity, placementId,  callback)|**Yodo1Mas.getInstance().showBannerAd(activity, placement);**|
|Yodo1Advert.hideBanner(activity)|Yodo1Advert.hideBanner(activity)|**Yodo1Mas.getInstance().dismissBannerAd();**|
|Yodo1Advert.removeBanner(activity)|Yodo1Advert.removeBanner(activity)|**Yodo1Mas.getInstance().dismissBannerAd(true);**|
|    |   | **Yodo1Mas.getInstance().setInterstitialListener** |
|  boolean isReady = Yodo1Advert.interstitialIsReady(activity);  | boolean isReady = Yodo1Advert.interstitialIsReady(activity); | boolean isLoaded = **Yodo1Mas.getInstance().isInterstitialAdLoaded();** |
|  Yodo1Advert.showInterstitial(activity, callback);  | Yodo1Advert.showInterstitial(activity, callback); | **Yodo1Mas.getInstance().showInterstitialAd(activity);** |
|Yodo1Advert.showInterstitial(activity, placementId,  callback)|Yodo1Advert.showInterstitial(activity, placementId,  callback)|**Yodo1Mas.getInstance().showInterstitialAd(activity, placement);**|
|    |    | **Yodo1Mas.getInstance().setRewardListener** |
|  boolean isReady = Yodo1Advert.videoIsReady(activity);  | boolean isReady = Yodo1Advert.videoIsReady(activity); | boolean isLoaded = **Yodo1Mas.getInstance().isRewardedAdLoaded();** |
|  Yodo1Advert.showVideo(activity, callback);  |  Yodo1Advert.showVideo(activity, callback);  | **Yodo1Mas.getInstance().showRewardedAd(Activity activity);** |
|Yodo1Advert.showVideo(activity, placementId,  callback)|Yodo1Advert.showVideo(activity, placementId,  callback)|**Yodo1Mas.getInstance().showRewardedAd(activity, placement);**|

### iOS Method Upates

| v3.13.0                                                 | v3.14.0                                                 |                             V4.+                             |
| ------------------------------------------------------- | ------------------------------------------------------- | :----------------------------------------------------------: |
| [Yodo1Ads initWithAppKey: appKey];                      | [Yodo1Advert initWithAppKey: appKey];                   | **[[Yodo1Mas sharedInstance] initWithAppId: successful: fail:];** |
| [Yodo1Ads setUserConsent:consent];                      | [Yodo1Ads setUserConsent:consent];                      |       **[Yodo1Mas sharedInstance].isGDPRUserConsent**        |
| [Yodo1Ads isUserConsent];                               | [Yodo1Ads isUserConsent];                               |       **[Yodo1Mas sharedInstance].isGDPRUserConsent**        |
| [Yodo1Ads setTagForUnderAgeOfConsent:isBelowConsentAge] | [Yodo1Ads setTagForUnderAgeOfConsent:isBelowConsentAge] |      **[Yodo1Mas sharedInstance].isCOPPAAgeRestricted**      |
| [Yodo1Ads isTagForUnderAgeOfConsent];                   | [Yodo1Ads isTagForUnderAgeOfConsent];                   |      **[Yodo1Mas sharedInstance].isCOPPAAgeRestricted**      |
| [Yodo1Ads setDoNotSell:doNotSell]                       | [Yodo1Ads setDoNotSell:doNotSell]                       |        **[Yodo1Mas sharedInstance].isCCPADoNotSell**         |
| [Yodo1Ads isDoNotSell];                                 | [Yodo1Ads isDoNotSell];                                 |        **[Yodo1Mas sharedInstance].isCCPADoNotSell**         |
| [Yodo1Ads setBannerCallback:callback];                  | [Yodo1Ads setBannerCallback:callback];                  |        **[Yodo1Mas sharedInstance].bannerAdDelegate**        |
| [Yodo1Ads setBannerAlign:align];                        | [Yodo1Ads setBannerAlign:align];                        | **[[Yodo1Mas sharedInstance] showBannerAdWithAlign:align];** |
| [Yodo1Ads setBannerOffset:point];                       | [Yodo1Ads setBannerOffset:point];                       | **[[Yodo1Mas sharedInstance] showBannerAdWithAlign:align offset:offset];** |
| BOOL isLoaded = [Yodo1Ads bannerIsReady];               | BOOL isLoaded = [Yodo1Ads bannerIsReady];               | BOOL isLoaded = **[[Yodo1Mas sharedInstance] isBannerAdLoaded];** |
| [Yodo1Ads showBanner];                                  | [Yodo1Ads showBanner];                                  |        **[[Yodo1Mas sharedInstance] showBannerAd];**         |
| [Yodo1Ads showBanner:placement_id];                     | [Yodo1Ads showBanner:placement_id];                     | **[[Yodo1Mas sharedInstance] showBannerAdWithPlacement:placement];** |
| [Yodo1Ads hideBanner];                                  | [Yodo1Ads hideBanner];                                  |       **[[Yodo1Mas sharedInstance] dismissBannerAd];**       |
| [Yodo1Ads removeBanner];                                | [Yodo1Ads removeBanner];                                | **[[Yodo1Mas sharedInstance] dismissBannerAdWithDestroy:YES];** |
| [Yodo1Ads setInterstitialCallback:callback];            | [Yodo1Ads setInterstitialCallback:callback];            |     **[Yodo1Mas sharedInstance].interstitialAdDelegate**     |
| BOOL isLoaded = [Yodo1Ads interstitialIsReady];         | BOOL isLoaded = [Yodo1Ads interstitialIsReady];         | BOOL isLoaded =**[[Yodo1Mas sharedInstance] isInterstitialAdLoaded];** |
| [Yodo1Ads showInterstitial];                            | [Yodo1Ads showInterstitial];                            |     **[[Yodo1Mas sharedInstance] showInterstitialAd];**      |
| [Yodo1Ads showInterstitialWithPlacement:placement_id];  | [Yodo1Ads showInterstitialWithPlacement:placement_id];  | **[[Yodo1Mas sharedInstance] showInterstitialAdWithPlacement:placement];** |
| [Yodo1Ads setVideoCallback:callback];                   | [Yodo1Ads setVideoCallback:callback];                   |        **[Yodo1Mas sharedInstance].rewardAdDelegate**        |
| BOOL isLoaded = [Yodo1Ads videoIsReady];                | BOOL isLoaded = [Yodo1Ads videoIsReady];                | BOOL isLoaded =**[[Yodo1Mas sharedInstance] isRewardAdLoaded];** |
| [Yodo1Ads showVideo];                                   | [Yodo1Ads showVideo];                                   |        **[[Yodo1Mas sharedInstance] showRewardAd];**         |
| [Yodo1Ads showVideoWithPlacement:placement_id];         | [Yodo1Ads showVideoWithPlacement:placement_id];         | **[[Yodo1Mas sharedInstance] showRewardAdWithPlacement:placement];** |



## Ad Event Updates

**Important!**`AdEventClick` event has been deprecated in the version 4.0.0.0 and above

| v3.13.0v3.13.0 | v3.14.0 | v4.+                                   |
| -------------- | ------- | -------------------------------------- |
|                |         | **Yodo1.MAS.Yodo1U3dAdEvent.AdError**  |
|                |         | **Yodo1.MAS.Yodo1U3dAdEvent.AdOpened** |
|                |         | **Yodo1.MAS.Yodo1U3dAdEvent.AdClosed** |
|                |         | **Yodo1.MAS.Yodo1U3dAdEvent.AdReward** |
|                |         |                                        |

