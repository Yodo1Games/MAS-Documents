# Android Integration
> MAS supports Android version 4.4.+ (Android API level: 19+) and above

**Important** Update MAS Rivendell SDK
- To upgrade from an older SDK to MAS SDK v2, you must remove all the contents of the old SDK
- We have modified the interface of the new SDK, please carefully refer to the following documents to upgrade

## The Integration Steps
### 1. Open your project-level `build.gradle` and add the relevant code.

```groovy
maven { url "https://dl.bintray.com/ironsource-mobile/android-sdk" }
maven { url "https://dl.bintray.com/ironsource-mobile/android-adapters" }
maven { url "https://dl.bintray.com/yodo1/MAS-Android" }
maven { url "https://dl.bintray.com/yodo1/android-sdk" }
```

### 2. Open your app-level `build.gradle` and add the relevant code.
#### 2.1 Add a Gradle dependency
```groovy
implementation 'com.yodo1.mas:google:0.0.0.20-beta'
```

#### 2.2 Add the `compileOptions` property to the `Android` section
```ruby
android {
	compileOptions {
		sourceCompatibility = 1.8
		targetCompatibility = 1.8
	} 
}
```

### 3. Add the `MultiDex` property to the `defaultConfig` section

```
defaultConfig {
    ...
    multiDexEnabled true
    ...
}
```

### 4. Support AndroidX
Add the following content to the `gradle.properties` file

```ruby
android.useAndroidX=true
android.enableJetifier=true
```

### 5. Add AdMob App ID
* Add your `AdMob App ID` to your app's AndroidManifest.xml file by adding the `<meta-data>` tag 
* You can find your App ID in the MAS dashboard
* Please replace `android:value` with your own AdMob App ID

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

	
### 7. Android P Adaptation

To be compatible with `Android P (API level 28)`, please do the following:

* Create an XML folder in your resources folder
* Create an XML file named `network_security_configi.xml` in the XML folder. In the `res/xml/network_security_config.xml` file, please add these lines

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
* Next, add these lines to the application element in `AndroidManifest.xml`.

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest ... >
	<application android:networkSecurityConfig="@xml/network_security_config"
	... >
	...
	</application>
</manifest>
```
	
### 8. Comply With Necessary Legal Frameworks
Please comply with all legal frameworks that apply to your game and its users. You can find references to major legal frameworks and details about how to comply with them while using MAS through these links:

* [GDPR](privacy-gdpr.md)
* [COPPA](privacy-coppa.md)
* [CCPA](privacy-ccpa.md)

### 9. Initialize the SDK
Initialize the SDK in the `onCreate` method of `Activity`

```java
protected void onCreate() {
  super.onCreate();
	Yodo1Mas.getInstance().init(this, "Your AppId", new Yodo1Mas.InitListener() {
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

### 10. ProGuard
If you're using ProGuard with the MAS SDK, add the following code to your ProGuard file (Android Studio: `proguard-rules.pro` or Eclipse: `proguard-project.txt`).

```
-ignorewarnings
-keeppackagenames com.yodo1.**
-keep class com.yodo1.** { *; }
-keep class com.yodo1.mas.** { *; }
-keep class com.yodo1.mas.ads.** {*;}
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

## Interstitial Integration

### 1. Set the interstitial ad delegate method

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
    
### 2. Check the loading status of interstitials

```java
boolean isLoaded = Yodo1Mas.getInstance().isInterstitialAdLoaded();
```
    
### 3. Show interstitial ad

```java
Yodo1Mas.getInstance().showInterstitialAd(MyActivity.this);
```
    
## Rewarded Video Integration

### 1. Set up rewarded video ad delegate methods

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
    
### 2. Check the loading status of rewarded video ads

```java
boolean isLoaded = Yodo1Mas.getInstance().isBannerAdLoaded();
```
    
### 3. Show rewarded video ads

```java
Yodo1Mas.getInstance().showRewardedAd(MyActivity.this);
```

## Banner Integration
### 1. Set up the banner ad delegate method
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

### 2. Check the banner ad load status
```java
boolean isLoaded =  Yodo1Mas.getInstance().isBannerAdLoaded();
```
    
### 3. Show banner ad
```java
Yodo1Mas.getInstance().showBannerAd(MyActivity.this);
```
 
### 4. Dismiss banner ad
```java
Yodo1Mas.getInstance().dismissBannerAd(MyActivity.this);
```

## Advanced Settings
### Ad Placements
> MAS SDK gives you the ability to set a placement name(e.g. MainMenu, Upgrade_Level etc)

Below are code snippets on how to set placements for banners, interstitials, and rewarded ads.

**Interstitial Ads**

```java
Yodo1Mas.getInstance().showInterstitialAd(MyActivity.this, "MY_INTERSTITIAL_PLACEMENT");
```

**Rewarded Video Ads**

```java
Yodo1Mas.getInstance().showRewardedAd(MyActivity.this, "MY_REWARDED_PLACEMENT");
```

**Banner Ads**

```java
Yodo1Mas.getInstance(). showBannerAd(MyActivity.this, "MY_BANNER_PLACEMENT");
```

## Changelog
|  Version   | Release Date | Notes |
|  --------  | ------------ | ------------  |
|            |              |               |
|            |              |               |

