# Android集成
> `SDK`要求`Android OS`的最低版本为`Android 4.4`及以上版本</br>
> 重要: 确保你使用的是`Gradle 3.3.0+`版本。

**重要** 更新MAS Rivendell SDK
- 从较旧的SDK升级到MAS SDK v2，您必须移除所有旧SDK的内容
- 我们对新SDK的接口做出了修改，请仔细参照以下文档进行升级

## 集成步骤
### 1. 项目级别`build.gradle`添加 
```groovy
maven { url "https://dl.bintray.com/ironsource-mobile/android-sdk" }
maven { url "https://dl.bintray.com/ironsource-mobile/android-adapters" }
maven { url "https://dl.bintray.com/yodo1/MAS-Android" }
maven { url "https://dl.bintray.com/yodo1/android-sdk" }
```

### 2. app级别`build.gradle`添加
#### 2.1 添加MAS SDK依赖
```groovy
implementation 'com.yodo1.mas:google:0.0.0.14-beta'
```

#### 2.2 添加`compileOptions`属性到 `android` 部分
```ruby
android {
	compileOptions {
		sourceCompatibility = 1.8
		targetCompatibility = 1.8
	} 
}
```

### 3. 开启`MultiDex`，app级别`build.gradle`添加
```
defaultConfig {
    ...
    multiDexEnabled true
    ...
}
```

### 4. 支持AndroidX
添加下面内容到 `gradle.properties` 文件

```ruby
android.useAndroidX=true
android.enableJetifier=true
```

### 5. 添加AdMob应用ID
* 通过添加`<meta-data>`标签，将AdMob应用ID添加到你的应用的`AndroidManifest.xml`文件中
* 你可以在MAS后台中找到你的应用的AdMob应用ID。
* 将`android:value`替换为您自己的AdMob应用ID，示例如下：

```xml
<manifest>
	<application>
	<!-- Sample AdMob App ID: ca-app-pub-3940256099942544~3347511713 -->
	<meta-data
		android:name="com.google.android.gms.ads.APPLICATION_ID"
		android:value="YOUR_ADMOB_APP_ID"/>
	</application>
</manifest>
```

### 6. AdMob Android Manifest Merging Errors
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

	
### 7. Android P 适配
为了兼容`Android P(API level 28)`，请完成以下步骤:

* 在res文件夹下创建一个`xml`文件夹
* 然后创建一个`xml`文件(`res/xml/network_security_config.xml`)并在文件中添加如下内容：

```xml
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
	...
	<base-config cleartextTrafficPermitted="true" />
	<domain-config cleartextTrafficPermitted="true">
	<domain includeSubdomains="true">127.0.0.1</domain>
	</domain-config>
	...
</network-security-config>  
```
* 在你的应用的`AndroidManifest.xml`文件中添加下面的配置，应用属性如下:

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest ... >
	<application android:networkSecurityConfig="@xml/network_security_config"
	... >
	...
	</application>
</manifest>
```
	
### 8. 遵守必要的法律框架(Privacy)
请遵守适用于您的游戏及其用户的所有法律框架。您可以通过这些链接找到相关的法规信息:

* [GDPR](privacy-gdpr.md)
* [COPPA](privacy-coppa.md)
* [CCPA](privacy-ccpa.md)

### 9. 初始化SDK
在`Activity`的`onCreate`方法中初始化SDK

```java
protected void onCreate() {
  super.onCreate();
	Yodo1Mas.getInstance().init(this, "你的AppId", new Yodo1Mas.InitListener() {
	    @Override
	    public void onMasInitSuccessful() {
	        // 初始化成功
	    }
	
	    @Override
	    public void onMasInitFailed(@NonNull Yodo1MasError error) {
	        // 初始化失败
	    }
	});
}
```

### 10. 混淆
如果您的应用需要混淆，必须将以下代码添加到您的ProGuard文件中(Android Studio: `ProGuard-rules.pro`或Eclipse: `proguard-project.txt`):

```
-ignorewarnings
-keeppackagenames com.yodo1.**
-keep class com.yodo1.** { *; }
-keep class com.yodo1.mas.** { *; }
-keep class com.yodo1.mas.error.** { *; }
-keep class com.yodo1.mas.event.** { *; }
-keep public class * extends com.yodo1.mas.mediation.Yodo1MasAdapterBase

-keep class com.google.ads.** { *; }

-keepclassmembers class com.ironsource.sdk.controller.IronSourceWebView$JSInterface {
public *;
}
-keepclassmembers class * implements android.os.Parcelable {
public static final android.os.Parcelable$Creator *;
}
-keep public class com.google.android.gms.ads.** {
public *;
}
-keep class com.ironsource.adapters.** {
*;
}
-dontwarn com.ironsource.mediationsdk.**
-dontwarn com.ironsource.adapters.**
-dontwarn com.moat.**
-keep class com.moat.** { public protected private *; }

-keepattributes SourceFile,LineNumberTable
-keepattributes JavascriptInterface
-keep class android.webkit.JavascriptInterface {
*;
}
-keep class com.unity3d.ads.** {
*;
}
-keep class com.unity3d.services.** {
*;
}
-dontwarn com.google.ar.core.**
-dontwarn com.unity3d.services.**
-dontwarn com.ironsource.adapters.unityads.**
-keepattributes Signature,InnerClasses,Exceptions,Annotation
-keep public class com.applovin.sdk.AppLovinSdk{
*;
}
-keep public class com.applovin.sdk.AppLovin* {
public protected *;
}
-keep public class com.applovin.nativeAds.AppLovin* {
public protected *;
}
-keep public class com.applovin.adview.* {
public protected *;
}
-keep public class com.applovin.mediation.* {
public protected *;
}
-keep public class com.applovin.mediation.ads.* {
public protected *;
}
-keep public class com.applovin.impl.*.AppLovin {
public protected *;
}
-keep public class com.applovin.impl.**.*Impl {
public protected *;
}
-keepclassmembers class com.applovin.sdk.AppLovinSdkSettings {
private java.util.Map localSettings;
}
-keep class com.applovin.mediation.adapters.** {
*;
}
-keep class com.applovin.mediation.adapter.**{
*;
}
-keep class com.chartboost.** {
*;
}
-dontwarn com.facebook.ads.internal.**
-keeppackagenames com.facebook.*
-keep public class com.facebook.ads.** {public protected *;}
-keep class com.tapjoy.** { *;}
-keep class com.moat.** { *;}
-keepattributes JavascriptInterface
-keepattributes *Annotation*
-keep class * extends java.util.ListResourceBundle {
protected Object[][] getContents();
}
-keep public class com.google.android.gms.common.internal.safeparcel.SafeParcelable {
public static final *** NULL;
}
-keepnames @com.google.android.gms.common.annotation.KeepName class * -keepclassmembernames class * {
@com.google.android.gms.common.annotation.KeepName *;
}
-keepnames class * implements android.os.Parcelable {
public static final ** CREATOR;
}
-keep class com.google.android.gms.ads.identifier.** { *;}
-dontwarn com.tapjoy.**

-keep class com.vungle.warren.** { *;}
-dontwarn com.vungle.warren.error.VungleError$ErrorCode
-keep class com.moat.** { *;}
-dontwarn com.moat.**
-dontwarn org.codehaus.mojo.animal_sniffer.IgnoreJRERequirement
-dontwarn okio.**
-dontwarn retrofit2.Platform$Java8
-keepattributes Signature
-keepattributes *Annotation*
-dontwarn sun.misc.**
-keep class com.google.gson.examples.android.model.** { *;}
-keep class * implements com.google.gson.TypeAdapterFactory
-keep class * implements com.google.gson.JsonSerializer
-keep class * implements com.google.gson.JsonDeserializer
-keep class com.google.android.gms.internal.** { *;}
-dontwarn com.google.android.gms.ads.identifier.**

-keepattributes SourceFile,LineNumberTable

-keep class com.my.target.** {*;}

-keep class com.yandex.mobile.ads.** {*;}
-dontwarn com.yandex.mobile.ads.**

-keepattributes *Annotation*

-keep public class com.bytedance.sdk.openadsdk.*{ public *;}

-dontwarn com.tencent.bugly.**
-keep public class com.tencent.bugly.**{*;}

-dontwarn com.sensorsdata.analytics.android.**
-keep class com.sensorsdata.analytics.android.** {
*;
}

-keep class com.yodo1.sensor.** {
*;
}

-keep class **.R$* {
<fields>;
}
-keep public class * extends android.content.ContentProvider
-keepnames class * extends android.view.View

-keep class * extends android.app.Fragment {
public void setUserVisibleHint(boolean);
public void onHiddenChanged(boolean);
public void onResume();
public void onPause();
}
-keep class android.support.v4.app.Fragment {
public void setUserVisibleHint(boolean);
public void onHiddenChanged(boolean);
public void onResume();
public void onPause();
}
-keep class * extends android.support.v4.app.Fragment {
public void setUserVisibleHint(boolean);
public void onHiddenChanged(boolean);
public void onResume();
public void onPause();
}

-dontwarn org.json.**
-keep class org.json.**{*;}

-keep public class com.bytedance.sdk.openadsdk.*{
public *;
}
-keepattributes SourceFile,LineNumberTable
-keep class com.inmobi.** {
*;
}
-keep public class com.google.android.gms.**
-dontwarn com.google.android.gms.**
-dontwarn com.squareup.picasso.**
-keep class com.google.android.gms.ads.identifier.AdvertisingIdClient{
public *;
}
-keep class com.google.android.gms.ads.identifier.AdvertisingIdClient$Info{
public *;
}
# skip the Picasso library classes
-keep class com.squareup.picasso.** {*;}
-dontwarn com.squareup.okhttp.**
# skip Moat classes
-keep class com.moat.** {*;}
-dontwarn com.moat.**
# skip IAB classes
-keep class com.iab.** {*;}
-dontwarn com.iab.**

-keep class com.umeng.** {*;}

-keep class com.uc.** {*;}

-keepclassmembers class * {
public <init> (org.json.JSONObject);
}
-keepclassmembers enum * {
public static **[] values();
public static ** valueOf(java.lang.String);
}
-keep class com.zui.** {*;}
-keep class com.miui.** {*;}
-keep class com.heytap.** {*;}
-keep class a.** {*;}
-keep class com.vivo.** {*;}

-keep class com.uc.crashsdk.** { *; }
-keep interface com.uc.crashsdk.** { *; }
```

## 插屏广告集成

### 1. 设置插屏广告代理方法

```java
Yodo1Mas.getInstance().setInterstitialListener(new Yodo1Mas.InterstitialListener() {
    @Override
    public void onAdOpened(@NonNull Yodo1MasAdEvent event) {
    }

    @Override
    public void onAdError(@NonNull Yodo1MasAdEvent event, @NonNull Yodo1MasError error) {
        
    }

    @Override
    public void onAdClosed(@NonNull Yodo1MasAdEvent event) {
    
    }
});      
```
    
### 2. 检查插屏广告加载状态

```java
boolean isLoaded = Yodo1Mas.getInstance().isInterstitialAdLoaded();
```
    
### 3. 展示插屏广告

```java
Yodo1Mas.getInstance().showInterstitialAd(MyActivity.this);
```
    
## 激励视频广告

### 1. 设置激励视频广告代理方法

```java
Yodo1Mas.getInstance().setRewardListener(new Yodo1Mas.RewardListener() {
    @Override
    public void onAdOpened(@NonNull Yodo1MasAdEvent event) {

    }

    @Override
    public void onAdvertRewardEarned(@NonNull Yodo1MasAdEvent event) {

    }

    @Override
    public void onAdError(@NonNull Yodo1MasAdEvent event, @NonNull Yodo1MasError error) {
    
    }
    
    @Override
    public void onAdClosed(@NonNull Yodo1MasAdEvent event) {
        
    }
});
```
    
### 2. 检查激励视频广告加载状态

```java
boolean isLoaded = Yodo1Mas.getInstance().isBannerAdLoaded();
```
    
### 3. 展示激励视频广告

```java
Yodo1Mas.getInstance().showRewardedAd(MyActivity.this);
```

## 横幅广告集成
### 1. 设置横幅广告代理方法
```java
Yodo1Mas.getInstance().setBannerListener(new Yodo1Mas.BannerListener() {
    @Override
    public void onAdOpened(@NonNull Yodo1MasAdEvent event) {
    
    }

    @Override
    public void onAdError(@NonNull Yodo1MasAdEvent event, @NonNull Yodo1MasError error) {
    
    }

    @Override
    public void onAdClosed(@NonNull Yodo1MasAdEvent event) {
    
    }
});
```

### 2. 检查横幅广告加载状态
```java
boolean isLoaded =  Yodo1Mas.getInstance().isBannerAdLoaded();
```
    
### 3. 展示横幅广告
```java
Yodo1Mas.getInstance().showBannerAd(MyActivity.this);
```
 
### 4. 关闭横幅广告
```java
Yodo1Mas.getInstance().dismissBannerAd(MyActivity.this);
```

## 高级设置
### 广告位
> MAS SDK让你能够设置每个广告单元的放置名称(例如: MainMenu, Upgrade_Level等)。

以下是如何设置插屏广告、奖励广告和横幅广告的示例代码：

**插屏广告**

```java
Yodo1Mas.getInstance().showInterstitialAd(MyActivity.this, "MY_INTERSTITIAL_PLACEMENT");
```

**激励视频广告**

```java
Yodo1Mas.getInstance().showRewardedAd(MyActivity.this, "MY_REWARDED_PLACEMENT");
```

**横幅广告**

```java
Yodo1Mas.getInstance(). showBannerAd(MyActivity.this, "MY_BANNER_PLACEMENT");
```

## 更新日志
|  版本   | 发布日期  | 更新内容 |
|  ----  | ------- | ------  |
|           |              |               |
|           |              |               |

