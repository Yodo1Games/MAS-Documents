# Unity upgrade guide

#### 1. Remove old SDK

Please delete the following directories:

- Assets/Plugins/iOS/Yodo1Ads
- Assets/Plugins/Android/Yodo1Ads
- Assets/Yodo1Ads

#### 2. Add new SDK

- Download the latest [Unity Plugin](https://docs.yodo1.com/download/Rivendell-SDKs/Rivendell-4.0.0.3.unitypackage)

- Double click to open the plugin and import

For specific integration steps, please refer to [Document](integration-unity.md#the-integration-steps)

#### 3. Method signature change

New namespace,v4 provides a more standardized API,The namespace of the related API is `Yodo1.MAS`,please make sure to introduce this namespace when using v4.+

##### Upgrade from v3.13.0 and below to v4.+Please refer to the following comparison table:

| v3.13.0                                   | v4.+                                                         |
| :---------------------------------------- | :----------------------------------------------------------- |
| Yodo1U3dAds.InitializeSdk();              | **Yodo1U3dMas.InitializeSdk();**                             |
| Yodo1U3dSDK.setBannerdDelegate            | **Yodo1U3dMas.SetBannerAdDelegate**                          |
| Yodo1U3dSDK.setInterstitialAdDelegate     | **Yodo1U3dMas.SetInterstitialAdDelegate**                    |
| Yodo1U3dSDK.setRewardVideoDelegate        | **Yodo1U3dMas.SetRewardedAdDelegate**                        |
| Yodo1U3dAds.BannerIsReady();              | **Yodo1U3dMas.IsBannerAdLoaded();**                          |
| Yodo1U3dAds.InterstitialIsReady();        | **Yodo1U3dMas.IsInterstitialAdLoaded();**                    |
| Yodo1U3dAds.VideoIsReady();               | **Yodo1U3dMas.IsRewardedAdLoaded();**                        |
| Yodo1U3dAds.ShowBanner();                 | **Yodo1U3dMas.ShowBannerAd();**                              |
| Yodo1U3dAds.ShowBanner(placementId)       | **Yodo1U3dMas.ShowBannerAd(placementId)**                    |
| Yodo1U3dAds.SetBannerAlign(align)         | **Yodo1U3dMas.ShowBannerAd(align)**                          |
| Yodo1U3dAds.SetBannerOffset(x, y)         | **Yodo1U3dMas.ShowBannerAd(align, x, y)**                    |
| Yodo1U3dAds.HideBanner()                  | **Yodo1U3dMas.DismissBannerAd()**                            |
| Yodo1U3dAds.RemoveBanner()                | **Yodo1U3dMas.DismissBannerAd(true)**                        |
| Yodo1U3dAds.ShowInterstitial()            | **Yodo1U3dMas.ShowInterstitialAd();**                        |
| Yodo1U3dAds.ShowInterstitial(placementId) | **Yodo1U3dMas.ShowInterstitialAd(placementId)**              |
| Yodo1U3dAds.ShowVideo()                   | **Yodo1U3dMas.ShowRewardedAd();**                            |
| Yodo1U3dAds.ShowVideo(placementId)        | **Yodo1U3dMas.ShowRewardedAd(placementId)**                  |
|                                           | **Yodo1U3dMas.SetInitializeDelegate**//Add initialization callback |




##### From v3.14.0 to v4.+, please refer to the following comparison table:

| v3.14.0                                  | v4.+                                                         |
| :--------------------------------------- | :----------------------------------------------------------- |
| Yodo1U3dAds.InitializeSdk();             | **Yodo1U3dMas.InitializeSdk();**                             |
| Yodo1U3dAdsSDK.setBannerdDelegate        | **Yodo1U3dMas.SetBannerAdDelegate**                          |
| Yodo1U3dAdsSDK.setInterstitialAdDelegate | **Yodo1U3dMas.SetInterstitialAdDelegate**                    |
| Yodo1U3dAdsSDK.setRewardVideoDelegate    | **Yodo1U3dMas.SetRewardedAdDelegate**                        |
| Yodo1U3dAds.BannerIsReady();             | **Yodo1U3dMas.IsBannerAdLoaded();**                          |
| Yodo1U3dAds.InterstitialIsReady();       | **Yodo1U3dMas.IsInterstitialAdLoaded();**                    |
| Yodo1U3dAds.VideoIsReady();              | **Yodo1U3dMas.IsRewardedAdLoaded();**                        |
| Yodo1U3dAds.ShowBanner();                | **Yodo1U3dMas.ShowBannerAd();**                              |
| Yodo1U3dAds.ShowBanner(placementId)      | **Yodo1U3dMas.ShowBannerAd(placementId)**                    |
| Yodo1U3dAds.SetBannerAlign(align)        | **Yodo1U3dMas.ShowBannerAd(align)**                          |
| Yodo1U3dAds.SetBannerOffset(x, y)        | **Yodo1U3dMas.ShowBannerAd(align, x, y)**                    |
| Yodo1U3dAds.HideBanner()                 | **Yodo1U3dMas.DismissBannerAd()**                            |
| Yodo1U3dAds.RemoveBanner()               | **Yodo1U3dMas.DismissBannerAd(true)**                        |
| Yodo1U3dAds.ShowInterstitial()           | **Yodo1U3dMas.ShowInterstitialAd();**                        |
| Yodo1U3dAds.ShowInterstitial(placementId)| **Yodo1U3dMas.ShowInterstitialAd(placementId)**              |
| Yodo1U3dAds.ShowVideo()                  | **Yodo1U3dMas.ShowRewardedAd();**                            |
| Yodo1U3dAds.ShowVideo(placementId)       | **Yodo1U3dMas.ShowRewardedAd(placementId)**                  |
|                                          | **Yodo1U3dMas.SetInitializeDelegate** //Add initialization callback |

##### Unity Ad Event signature change，please refer to the following comparison table：

| v3.13.0/v3.14.0                              | v4.+                                                         |
| -------------------------------------------- | ------------------------------------------------------------ |
| Yodo1U3dConstants.AdEvent.AdEventShowFail    | **Yodo1.MAS.Yodo1U3dAdEvent.AdError**                        |
| Yodo1U3dConstants.AdEvent.AdEventShowSuccess | **Yodo1.MAS.Yodo1U3dAdEvent.AdOpened**                       |
| Yodo1U3dConstants.AdEvent.AdEventClose       | **Yodo1.MAS.Yodo1U3dAdEvent.AdClosed**                       |
| Yodo1U3dConstants.AdEvent.AdEventFinish      | **Yodo1.MAS.Yodo1U3dAdEvent.AdReward**                       |
| Yodo1U3dConstants.AdEvent.AdEventClick       | **important!** The `AdEventClick` event has been removed in 4.0.0.0 and above |
