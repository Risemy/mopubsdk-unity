# unity集成Android aar

## 系统要求
android 4.1 或更高版本

## 集成
 
``` 
<dependencies>
  <androidPackages>
      <androidPackage spec="com.google.android.gms:play-services-games:9.8.0">
      <androidSdkPackageIds>
        <androidSdkPackageId>extra-google-m2repository</androidSdkPackageId>
      </androidSdkPackageIds>
    </androidPackage>

	 <androidPackage spec="com.wnl:mopub_ad_sdk_unity:1.0.5">
	  <repositories>
	 <repository>https://s3.amazonaws.com/moat-sdk-builds</repository>
     <repository>https://maven.google.com</repository>
	 <repository>https://dl.bintray.com/ironsource-mobile/android-sdk</repository>
	 <repository>https://raw.githubusercontent.com/Risemy/mopubsdk-unity/master</repository>
	 <repository>https://dl.bintray.com/umsdk/release</repository>
	 </repositories>
    </androidPackage>

  </androidPackages>
</dependencies>
 ```
 

## 使用案例

### 初始化SDK
* 包名  com.youloft.mopubsdkunity.core
* 类名  UnityAdManager
* 方法名  initUnityAdSdk（Activity context, String jsonAds, String app_flyers_id, String umengId）
* 参数依次为 activity，广告ID的json字符串,appflyer ID，友盟统计ID

### 加载广告

#### 1.1 加载一个Banner

* 包名  com.youloft.mopubsdkunity.core
* 类名  UnityAdManager
* 方法名  loadAndShowBannerAd（Activity context, boolean isTop）
* 参数依次为 activity，显示在手机屏幕的顶部（true）还是底部(false)
* 回调

```java
  public interface BannerAdListener {
    void onBannerLoaded();  //加载成功

    void onBannerFailed(String errorMsg);  //加载失败

    void onBannerClicked();  //点击了广告
}
```
#### 1.2 隐藏一个Banner 

*  包名  com.youloft.mopubsdkunity.core
*  类名  UnityAdManager
*  方法名  hideBannerAd（）
*  无参数
*  无回调

#### 1.3 加载插屏广告
*  包名  com.youloft.mopubsdkunity.core
*  类名  UnityAdManager
*  方法名  loadInterstitialAd（Activity activity）
*  参数 activity
*  回调 


```java
{
    void onInterstitialLoaded();  //加载成功

    void onInterstitialFailed(String errorMsg);  //加载失败

    void onInterstitialShown();  //已经显示

    void onInterstitialClicked(); //点击插屏广告

    void onInterstitialDismissed();  //已经关闭
}
```


#### 1.4 展示插屏广告
*  包名  com.youloft.mopubsdkunity.core
*  类名  UnityAdManager
*  方法名  showInterstitialAd（Activity activity）
*  参数 activity
*  回调

```java
{
    void onInterstitialLoaded();  //加载成功

    void onInterstitialFailed(String errorMsg);  //加载失败

    void onInterstitialShown();  //已经显示

    void onInterstitialClicked(); //点击插屏广告

    void onInterstitialDismissed();  //已经关闭
}
```


#### 1.5 缓存视频广告
*  包名  com.youloft.mopubsdkunity.core
*  类名  UnityAdManager
*  方法名  loadRewardedVideoAd（Activity activity）
*  参数 activity
*  回调 

```java
    void onRewardedVideoLoadSuccess();  //激励视频加载成功

    void onRewardedVideoLoadFailure(String errorMsg);  //激励视频加载失败

    void onRewardedVideoClicked();  //点击激励视频
 
    void onRewardedVideoClosed();   //关闭激励视频

    void onRewardedVideoCompleted();  //激励视频播放完毕

    void onRewardedVideoStarted();  // //激励视频开始播放

```

#### 1.6 展示视频广告
*  包名  com.youloft.mopubsdkunity.core
*  类名  UnityAdManager
*  方法名  showRewardedVideoAd（Activity activity）
*  参数 activity
*  回调 

```java
    void onRewardedVideoLoadSuccess();  //激励视频加载成功

    void onRewardedVideoLoadFailure(String errorMsg);  //激励视频加载失败

    void onRewardedVideoClicked();  //点击激励视频
 
    void onRewardedVideoClosed();   //关闭激励视频

    void onRewardedVideoCompleted();  //激励视频播放完毕

    void onRewardedVideoStarted();  // //激励视频开始播放

```

#### 1.7 是否存在已经缓存好的视频广告
*  包名  com.youloft.mopubsdkunity.core
*  类名  UnityAdManager
*  方法名  hasRewardedVideo（）
*  无参数 
*  无回调 
*  返回Boolean值


#### 二.统计分析

**2.1 Appsflyer**

* 须在初始化SDK时 AdConfig.Builder 里面 setAppFlyerKey(你的appsflyer ID) 默认为发行商的ID

**2.2 FaceBook**
***注意：必填项，如不填写，将无法初始化FaceBook 数据统计。***

在项目里面 AndroidManifest 的 Application 里面配置 facebook_app_id 是facebook开发者后台申请的 app_id

```java
   <meta-data android:name="com.facebook.sdk.ApplicationId" android:value="@string/facebook_app_id"/>
```
官方文档 https://developers.facebook.com/docs/android/getting-started/

#### 三.协议回调一览
**3.1 banner广告相关回调**
```java
  public interface BannerAdListener {
    void onBannerLoaded();  //加载成功

    void onBannerFailed(String errorMsg);  //加载失败

    void onBannerClicked();  //点击了广告
}
```

**3.2 插屏广告相关回调**
```java
public interface InterstitialAdListener {
    void onInterstitialLoaded();  //加载成功

    void onInterstitialFailed(String errorMsg);  //加载失败

    void onInterstitialShown();  //已经显示

    void onInterstitialClicked(); //点击插屏广告

    void onInterstitialDismissed();  //已经关闭
}
```

**3.3 激励视频相关回调**
```java
public interface RewardedAdListener {
    void onRewardedVideoLoadSuccess();  //激励视频加载成功

    void onRewardedVideoLoadFailure(String errorMsg);  //激励视频加载失败

    void onRewardedVideoClicked();  //点击激励视频
 
    void onRewardedVideoClosed();   //关闭激励视频

    void onRewardedVideoCompleted();  //激励视频播放完毕

    void onRewardedVideoStarted();  // //激励视频开始播放

}
```
