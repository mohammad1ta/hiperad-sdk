# Hiperad SDK  
You can get started with the following:  
[Initialize the SDK](#initialize-the-sdk)  
[Banner Ads](#banner-ads)  
[Rewarded Video Ads](#rewarded-video-ads)  
[Interstitial Ads](#interstitial-ads)

The latest version of Hiperad SDK supports Android OS versions 4 (API level 14) and later.

![Demo](demo.png)

### Initialize the SDK
1. Download [hiperad-sdk-1.5.aar](https://github.com/mohammad1ta/hiperad-sdk/blob/master/hiperad-sdk-1.5.aar) and copy to the **app/libs** directory within your project.
2. Add the relevant Gradle reference ( **app/build.gradle** )
```gradle
dependencies {
	...
	compile files('libs/hiperad-sdk-1.5.aar')
	...
}
```

3. Within your project’s **AndroidManifest.xml** file, add the following permissions inside the *<manifest>* tag.
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

4. Add the App token to your **AndroidManifest.xml** file (before the closing *</application>* tag):
```xml
<meta-data
    android:name="HIPERAD_APP_TOKEN"
    android:value="Your-Token-Here" />
```
> Your API keys are available in the Hiperad [dashboard](http://dashboard.hiperad.com).  
You will need to [register](https://dashboard.hiperad.com/register) or [login](https://dashboard.hiperad.com/login) in order to view your API keys.
  
___

### Banner Ads
You can add a banner ad in your layout resource file in XML and reference it in your code as you would in a regular view.
The following snippet shows how to add a banner ad in XML. 
```xml
<com.hiperad.sdk.view.HiperadBanner
    xmlns:hiperad="http://schemas.android.com/apk/lib/com.hiperad.sdk"
    hiperad:zone_id="Zone Here"
    hiperad:size="300x250"
    android:id="@+id/myad_1"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_gravity="center"
    android:layout_centerHorizontal="true"/>
```
> Dont forget to fill your Zone place code on **hiperad:zone_id** attibute.

You can use below sample code to show horizontal ad on parent bottom of your current layout:
```xml
<com.hiperad.sdk.view.HiperadBanner
    xmlns:hiperad="http://schemas.android.com/apk/lib/com.hiperad.sdk"
    hiperad:zone_id="Zone Here"
    hiperad:size="300x50"
    android:id="@+id/myad_2"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_gravity="center"
    android:layout_alignParentBottom="true"
    android:layout_centerHorizontal="true"/>
```

___

### Rewarded Video Ads
To create a rewarded video ad, create an instance of an HiperadVideo and set your Zone place.
```java
HiperadVideo videoAd = new HiperadVideo( "ZONE HERE" );
videoAd.createVideo(this);
videoAd.show();
```
You can set Listener interface that allows you to listen to events for an video ad. You should listen to these events to ensure that your application correctly handles the various ads transitions.
```java
videoAd.setVideoAdListener(this);
```
```java
@Override
public void onVideoAdClosed() {

    Log.e( "Video Status", "Closed" );

}

@Override
public void onVideoAdFailedToLoad(int errorCode) {

    Log.e( "Video Status", "Failed: " + errorCode );

}

@Override
public void onVideoAdLoaded() {

    Log.e( "Video Status", "Loaded" );

}

@Override
public void onVideoAdOpened() {

    Log.e( "Video Status", "Opened" );

}

@Override
public void onVideoAdCompleted() {

    Log.e( "Video Status", "Completed" );

}
```

___

### Interstitial Ads
Interstitial Ads are full screen ads that display over any of your application’s content. The best time to use Interstitial Ads is during a natural break in the application’s content, such as after completion of a level in a game. Within interstitial ad placements developers have the option to display interactive video ads.  
Create the interstitial placement instance and set the Zone placement.
```java
final HiperadInterstitial myAd = new HiperadInterstitial( "ZONE HERE" );
myAd.createInterstitial( this );
myAd.show();
```
You can set Listener interface that allows you to listen to events for an interstitial ad. You should listen to these events to ensure that your application correctly handles the various ads transitions.
```java
myAd.setBannerAdListener(this);
```
```java
@Override
public void onBannerAdClosed() {

    Log.e( "Ad Status", "Closed" );

}

@Override
public void onBannerAdFailedToLoad(int errorCode) {

    Log.e( "Ad Status", "Failed: " + errorCode );

}

@Override
public void onBannerAdLoaded() {

    Log.e( "Ad Status", "Loaded" );

}

@Override
public void onBannerAdOpened() {

    Log.e( "Ad Status", "Opened" );

}
```
