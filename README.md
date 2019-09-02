# unity集成Android aar

## 系统要求
android 4.1 或更高版本
Android Studio 3.4

## 集成

unity开发工具安装Google的unity-jar-resolver插件，拉取库,插件地址：https://github.com/googlesamples/unity-jar-resolver


拉取需要如下配置 
``` 
<dependencies>
  <androidPackages>
     
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
 

## 广告使用案例

###  一、初始化SDK
* 包名  com.youloft.mopubsdkunity.core
* 类名  UnityAdManager
* 方法名  initUnityAdSdk（Activity context, String jsonAds, String app_flyers_id, String umengId）
* 参数依次为 activity，广告ID的json字符串,appflyer ID，友盟统计ID

### 二、加载广告

#### 1.1 加载一个Banner

* 包名  com.youloft.mopubsdkunity.core
* 类名  UnityAdManager
* 方法名  loadAndShowBannerAd（Activity context, boolean isTop）
* 参数依次为 activity，显示在手机屏幕的顶部（true）还是底部(false)
* 回调

```java
{
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

### 三、生命周期相关

#### onCreate
*  包名  com.youloft.mopubsdkunity.core
*  类名  UnityAdManager
*  方法名  onMopubCreate（）
*  无参数 
*  无回调 


#### onResume
*  包名  com.youloft.mopubsdkunity.core
*  类名  UnityAdManager
*  方法名  onMopubResume（）
*  无参数 
*  无回调 

#### onPause

*  包名  com.youloft.mopubsdkunity.core
*  类名  UnityAdManager
*  方法名  onMopubPause（）
*  无参数 
*  无回调 

#### onDestory
*  包名  com.youloft.mopubsdkunity.core
*  类名  UnityAdManager
*  方法名  onMopubDestroy（）
*  无参数 
*  无回调 

## 统计分析使用案例

***注意：必填项，如不填写，将无法初始化FaceBook 数据统计。***

在项目里面 AndroidManifest 的 Application 里面配置 facebook_app_id 是facebook开发者后台申请的 app_id

```java
   <meta-data android:name="com.facebook.sdk.ApplicationId" android:value="@string/facebook_app_id"/>
```

官方文档 https://developers.facebook.com/docs/android/getting-started/

### 统计方法（以下方法暂时仅支持友盟和firebase统计）

#### 关卡统计
***注意：目前每个游戏最多支持500个关卡。***

* 包名 com.youloft.mopubsdkunity.core
* 类名 StatisticsManager
* 方法 在游戏开启新的关卡时调用 startLevel(String level) 方法，在关卡失败时调用failLevel(String level) 方法，在成功过关时调用 finishLevel(String level) 方法。

```java
  	public static void startLevel(String level) {
        UMGameAgent.startLevel(level);
        setFireBaseLevelStart(level);
    }

    public static void finishLevel(String level) {
        UMGameAgent.finishLevel(level);
        setFireBaseLevelEnd(level, 1);
    }

    public static void failLevel(String level) {
        UMGameAgent.failLevel(level);
        setFireBaseLevelEnd(level, 0);
    }
```

####虚拟消费统计

* 包名 com.youloft.mopubsdkunity.core
* 类名 StatisticsManager
* 方法 buy(String item, int number, double price)

```java
/**
     * 比如在游戏中使用金币购买了1个头盔，一个头盔价值 1000 金币，可以这样统计：
     *
     * @param item   购买物品的ID。
     * @param number 购买物品数量。
     * @param price  购买物品的单价(虚拟币)。
     */
	public static void buy(String item, int number, double price)
```

####现金消费统计
* 包名 com.youloft.mopubsdkunity.core
* 类名 StatisticsManager
* 方法 pay(String item, int number, double price)，pay(double money, String item, int number, double price, int source)

```java
/**
     * 在游戏中充值或者购买虚拟币的时候调用此方法，比如通过支付宝用 10元钱 购买了 1000 个金币，可以这样调用
     *
     * @param money  本次消费金额(非负数)。
     * @param coin   本次消费的等值虚拟币(非负数)。
     * @param source 支付渠道, 1 ~ 99 之间的整数， 1-8 已经被预先定义, 9~99之间需要在网站设置。
     */
    public static void pay(double money, double coin, int source) {
        UMGameAgent.pay(money, coin, source);
    }

    /**
     * 有些时候在游戏中会直接购买某个道具，比如10元购买 2个魔法药水,每个药水50个金币，可以调用下面的方法在付费的同时购买道具。
     *
     * @param money  本次消费的金额(非负数)。
     * @param item   购买物品的ID(不能为空)。
     * @param number 购买物品数量(非负数)。
     * @param price  每个物品等值虚拟币的价格(非负数)。
     * @param source 支付渠道 (见上表)。
     */
    public static void pay(double money, String item, int number, double price, int source) {
        UMGameAgent.pay(money, item, number, price, source);
    }
```

####物品消耗统计

***注意: 目前每个游戏最多支持1000个道具的统计***

* 包名 com.youloft.mopubsdkunity.core
* 类名 StatisticsManager
* 方法 use(String item, int number, double price)

```java
    /**
     * 游戏中的物品损耗，比如使用了2瓶魔法药水，每个需要50个虚拟币，可以这样统计：
     *
     * @param item   消耗的物品ID。
     * @param number 消耗物品数量。
     * @param price  物品单价（虚拟币）。
     */
    public static void use(String item, int number, double price) {
        UMGameAgent.use(item, number, price);
        fireBaseUse(item, number, price);
    }

```

####额外奖励

***所有的浮点类型，只精确到百分位； 所有的数值类型不能为负数，否则不予处理。tigger的取值在1~10之间，“1”已经被预先定义为“系统奖励”，超过这个范围将不予处理。***

* 包名 com.youloft.mopubsdkunity.core
* 类名 StatisticsManager
* 方法 bonus(double coin, int trigger), bonus(String item, int num, double price, int trigger)

```java
 /**
     * 针对游戏中额外获得的虚拟币进行统计，比如系统赠送，节日奖励，打怪掉落。 比如连续5天登陆游戏奖励1000金币。
     *
     * @param coin    赠送的虚拟币数额。
     * @param trigger 触发奖励的事件, 取值在 1~10 之间，“1”已经被预先定义为“系统奖励”， 2~10 需要在网站设置含义。
     */
    public static void bonus(double coin, int trigger) {
        UMGameAgent.bonus(coin, trigger);
        setFireBaseEarnVirtualMoney(coin, trigger);
    }

    /**
     * 如果是掉落道具，比如掉落一把价值100金币的宝剑可以这样调用：
     *
     * @param item    奖励物品ID。
     * @param num     奖励物品数量。
     * @param price   物品的虚拟币单价。
     * @param trigger 触发奖励的事件, 取值在 1~10 之间，“1”已经被预先定义为“系统奖励”， 2~10需要在网站设置含义。
     */
    public static void bonus(String item, int num, double price, int trigger) {
        UMGameAgent.bonus(item, num, price, trigger);
        setFireBaseEarnVirtualProduct(item, num, price, trigger);
    }
```
####玩家信息

* 包名 com.youloft.mopubsdkunity.core
* 类名 StatisticsManager
* 方法 onProfileSignIn(String ID),onProfileSignIn(String provider, String ID),setPlayerLevel(int level)，onProfileSignOff()

```java
   /**
     * 玩家信息
     *
     * @param ID 玩家账号ID，长度小于64字节。
     */
    public static void onProfileSignIn(String ID) {
        UMGameAgent.onProfileSignIn(ID);
        onFireBasePlayerSignIn("FromMyself", ID);
    }

    /**
     * 玩家信息
     *
     * @param provider 账号来源。如果玩家通过第三方账号登陆，可以调用此接口进行统计。
     *                 不能以下划线”_”开头，使用大写字母和数字标识，长度小于32字节;
     *                 如果是上市公司，建议使用股票代码。
     * @param ID       玩家账号ID，长度小于64字节。
     */
    public static void onProfileSignIn(String provider, String ID) {
        UMGameAgent.onProfileSignIn(provider, ID);
        onFireBasePlayerSignIn(provider, ID);
    }

    /**
     * 当玩家账号退出登录时需调用如下接口，调用之后不再发送账号相关内容。
     */
    public static void onProfileSignOff() {
        UMGameAgent.onProfileSignOff();
    }

    /**
     * 当玩家建立角色或者升级时  等级统计
     *
     * @param level 大于1的整数，最多统计1000个等级，
     */
    public static void setPlayerLevel(int level) {
        UMGameAgent.setPlayerLevel(level);
        setFireBasePlayerLevel(level);
    }
```

