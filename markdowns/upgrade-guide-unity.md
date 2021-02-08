# Unity升级指引

#### 1. 删除旧SDK

请删除以下目录:

- Assets/Plugins/iOS/Yodo1Ads
- Assets/Plugins/Android/Yodo1Ads
- Assets/Yodo1Ads

#### 2. 添加新SDK

- 下载最新的[Unity Plugin](https://docs.yodo1.com/download/Rivendell-SDKs/Rivendell-4.0.0.3.unitypackage)

- 双击打开插件并导入

具体集成步骤请参考[文档](https://github.com/Yodo1Games/MAS-Documents/blob/main/markdowns/integration-unity.md#the-integration-steps)

#### 3.方法修改

v3.13.0及以下到v4.+:

| v3.13.0                                           | v4.+                                                      |
| :------------------------------------------------ | :-------------------------------------------------------- |
| Yodo1U3dAds.InitializeSdk();                      | **Yodo1U3dMas.InitializeSdk();**                          |
|                                                   | **Yodo1U3dMas.SetInitializeDelegate**                     |
| Yodo1U3dSDK.setBannerdDelegate                    | **Yodo1U3dMas.SetBannerAdDelegate**                       |
| bool isReady = Yodo1U3dAds.BannerIsReady();       | bool isLoaded = **Yodo1U3dMas.IsBannerAdLoaded();**       |
| Yodo1U3dAds.ShowBanner();                         | **Yodo1U3dMas.ShowBannerAd();**                           |
| Yodo1U3dSDK.setInterstitialAdDelegate             | **Yodo1U3dMas.SetInterstitialAdDelegate**                 |
| bool isReady = Yodo1U3dAds.InterstitialIsReady(); | bool isLoaded = **Yodo1U3dMas.IsInterstitialAdLoaded();** |
| Yodo1U3dAds.ShowInterstitial()                    | **Yodo1U3dMas.ShowInterstitialAd();**                     |
| Yodo1U3dSDK.setRewardVideoDelegate                | **Yodo1U3dMas.SetRewardedAdDelegate**                     |
| bool isReady = Yodo1U3dAds.VideoIsReady();        | bool isLoaded = **Yodo1U3dMas.IsRewardedAdLoaded();**     |
| Yodo1U3dAds.ShowVideo()                           | **Yodo1U3dMas.ShowRewardedAd();**                         |

v3.14.0到v4.+：

| v3.13.0                                           | v4.+                                                      |
| :------------------------------------------------ | :-------------------------------------------------------- |
| Yodo1U3dAds.InitializeSdk();                      | **Yodo1U3dMas.InitializeSdk();**                          |
|                                                   | **Yodo1U3dMas.SetInitializeDelegate**                     |
| Yodo1U3dSDK.setBannerdDelegate                    | **Yodo1U3dMas.SetBannerAdDelegate**                       |
| bool isReady = Yodo1U3dAds.BannerIsReady();       | bool isLoaded = **Yodo1U3dMas.IsBannerAdLoaded();**       |
| Yodo1U3dAds.ShowBanner();                         | **Yodo1U3dMas.ShowBannerAd();**                           |
| Yodo1U3dSDK.setInterstitialAdDelegate             | **Yodo1U3dMas.SetInterstitialAdDelegate**                 |
| bool isReady = Yodo1U3dAds.InterstitialIsReady(); | bool isLoaded = **Yodo1U3dMas.IsInterstitialAdLoaded();** |
| Yodo1U3dAds.ShowInterstitial()                    | **Yodo1U3dMas.ShowInterstitialAd();**                     |
| Yodo1U3dSDK.setRewardVideoDelegate                | **Yodo1U3dMas.SetRewardedAdDelegate**                     |
| bool isReady = Yodo1U3dAds.VideoIsReady();        | bool isLoaded = **Yodo1U3dMas.IsRewardedAdLoaded();**     |
| Yodo1U3dAds.ShowVideo()                           | **Yodo1U3dMas.ShowRewardedAd();**                         |

#### Unity Ad Event更新

**重要!**`AdEventClick` 事件已在4.0.0.0及以上版本废弃

| v3.13.0/v3.14.0                              | v4.+                                   |
| -------------------------------------------- | -------------------------------------- |
| Yodo1U3dConstants.AdEvent.AdEventShowFail    | **Yodo1.MAS.Yodo1U3dAdEvent.AdError**  |
| Yodo1U3dConstants.AdEvent.AdEventShowSuccess | **Yodo1.MAS.Yodo1U3dAdEvent.AdOpened** |
| Yodo1U3dConstants.AdEvent.AdEventClose       | **Yodo1.MAS.Yodo1U3dAdEvent.AdClosed** |
| Yodo1U3dConstants.AdEvent.AdEventFinish      | **Yodo1.MAS.Yodo1U3dAdEvent.AdReward** |
| Yodo1U3dConstants.AdEvent.AdEventClick       |                                        |
