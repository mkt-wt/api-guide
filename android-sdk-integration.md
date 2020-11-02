# Android SDK Integration

분석 시스템의 핵심 구성요소인 SDK는 앱 인스톨과 인앱 이벤트를 어트리뷰트하고 인앱 애널리틱스에 필요한 데이터 포인트를 확보하는 역할을 수행합니다. 데이터를 측정하기 위해 본 문서의 안내에 따라 Wisetracker SDK를 Android App에 연동하여 주시기 바랍니다.




## 1. 필수 설정

필수 설정이란 SDK가 동작하기 위해서 반드시 앱에 추가되어야 하는 최소한의 설정을 말합니다. 필수 설정을 적용하게 되면 인스톨, 세션, 단말기 정보 등을 측정할 수 있게 됩니다.



### 앱에 SDK 추가

프로젝트의 app/build.gradle 파일에 있는 `dependencies`에 아래와 같이 Wisetracker SDK를 추가해주세요.

``` groovy
dependencies {
	implementation fileTree(dir: 'libs', include: ['*.jar'])
	....
	implementation 'com.sdk.wisetracker.base:base_module:0.0.14' // wisetracker base
	implementation 'com.sdk.wisetracker.new_dot:new_dot_module:0.0.14' // wisetracker core
}
```



### AuthorizationKey 등록

프로젝트의 app/res/values/strings.xml 파일에 아래 코드를 추가합니다.

``` xml
<string-array name="dotAuthorizationKey">
	<item name="useMode">1</item>
	<item name="serviceNumber">XXXXXXXX</item>
	<item name="expireDate">14</item>
	<item name="isDebug">false</item>
	<item name="isInstallRetention">true</item>
	<item name="isFingerPrint">true</item>
	<item name="accessToken"></item>
</string-array>
```

추가한 코드 중 `serviceNumber`의 value를 올바른 값으로 변경해야 합니다. 와이즈트래커에 로그인하여 화면 상단의 **Service** 부분을 선택하면 앱 이름과 함께 올바른 Service Number 가 나타납니다. *Service No.* 옆의 숫자를 복사하여 `serviceNumber`의 value로 입력해주세요.

![authKey](http://www.wisetracker.co.kr/wp-content/uploads/2020/09/authKey.png)



### HTTP 통신 허용

프로젝트의 Target API가 **API Level 28** 이상일 경우에 적용하는 설정입니다. 아래와 같이 HTTP 통신을 허용하는 두 가지 설정을 추가해주세요.

#### AndroidManifest.xml 설정

``` xml
<!-- AndroidManifest.xml -->
<application
	android:icon="@mipmap/ic_launcher"
	android:label="@string/app_name"
	android:networkSecurityConfig="@xml/network_security_config"
	android:theme="@style/AppTheme">
```

#### app/res/xml/network_security_config.xml 설정

``` xml
<!-- app/res/xml/network_security_config.xml -->
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
	<domain-config cleartextTrafficPermitted="true">
		<domain includeSubdomains="true">trk.analytics.wisetracker.co.kr</domain>
	</domain-config>
</network-security-config>
```



### Activity 감지를 위한 설정 추가

화면(Activity) 전환을 분석하기 위한 설정입니다. `onResume`에 `onStartPage`를 추가해주세요.

``` java
@Override
protected void onResume() {
	super.onResume();
	DOT.onStartPage(context);
}
```



### Hybrid App을 위한 설정 추가

Hybrid App인 경우에만 적용하면 되는 설정으로, WebView로 표시한 웹페이지 내에서 발생하는 이벤트를 측정하기 위해 필요합니다. 웹뷰로 불러온 페이지를 감지할 수 있도록 다음과 같이 `setWebView` 함수를 호출해주세요.

``` java
@Override
protected void onCreate(@Nullable Bundle savedInstanceState) {
	super.onCreate(savedInstanceState);
	WebView webView = findViewById(R.id.web_view);
	
	DOT.setWebView(webView);
}
```

그리고 `WebViewClient` 의 `onPageFinished` 콜백에 `injectJavascript`를 추가해주세요.

``` java
webView.setWebViewClient(new WebViewClient() {
	@Override
	public void onPageFinished(WebView view, String url) {
		super.onPageFinished(view, url);
		DOT.injectJavascript(view);
	}
});
````



## 2. 고급 설정

고급 설정이란 반드시 적용할 필요는 없지만 와이즈트래커의 확장된 분석기능을 활용하기 위해 추가해야 하는 설정을 말합니다. 필요에 따라 선택적으로 설정을 추가해주시기 바랍니다.



### Re-engagement 측정

앱을 설치해 놓았거나 과거에 앱을 설치했던 경험이 있는 유저가 앱을 다시 사용하는 것을 리인게이지먼트라고 표현합니다. 리인게이지먼트 캠페인은 앱을 실행시키기 위해 딥 링킹을 활용하며, 와이즈트래커의 `setDeepLink`를 적용하여 리인게이지먼트 성과를 측정할 수 있습니다.

딥 링크로 실행되는 Activity의 `onCreate`와 `onNewIntent`에 아래와 같이 `setDeepLink`를 추가합니다.

```java
public class DeepLinkActivity extends Activity {
	@Override
	protected void onCreate(@Nullable Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		/* 중략.. */
		DOT.setDeepLink(getIntent());
	}
	@Override
	protected void onNewIntent(Intent intent) {
		super.onNewIntent(intent);
		DOT.setDeepLink(getIntent());
	}
}
```



### Facebook 광고 성과 측정

[Facebook App Ads](https://www.facebook.com/business/help/1471413626484885?id=1858550721111595)의 퍼포먼스를 와이즈트래커로 측정하는데 필요한 설정으로, **Facebook SDK가 앱에 추가되어 있는 경우**에만 설정을 적용할 수 있습니다.

#### 설정 적용

`MainActivity`의 `onCreate`에 다음 코드를 추가해 주세요.

```java
// call Facebook API
AppLinkData.fetchDeferredAppLinkData(context, new AppLinkData.CompletionHandler() {
	@Override
	public void onDeferredAppLinkDataFetched(AppLinkData appLinkData) {
		if (appLinkData == null) {
			return ;
		}
		Bundle bundle = appLinkData.getArgumentBundle();
		if (bundle == null) {
			return;
		}
		// call Wisetracker API
		DOT.setFacebookReferrer(bundle);
	}
});
```



#### 데이터 확인

Facebook의 App Ads Helper로 *Deferred Deep Linking* 을 테스트 함으로써 위 설정이 올바르게 적용 되었는지를 확인할 수 있습니다.

**준비사항**

1. Android 테스트 단말기 환경
   * 단말기에 Facebook 앱을 설치하고 Facebook 개발자 계정으로 로그인해주세요.
   * 단말기에 테스트 대상 앱(고객사 앱)이 설치되어 있다면 삭제해주세요.
   * 개발자 모드와 USB 디버깅을 활성화 해주세요.
2. 데스크탑 환경
   * Android Studio를 설치해주세요.
   * USB로 연결된 테스트 단말기의 log를 Android Studio의 logcat으로 확인할 수 있어야 합니다.
3. Facebook 설정
   * 테스트 대상 앱이 Facebook Developer에 등록되어 있어야 합니다.
   * 개발자 계정으로 로그인하여 테스트를 진행합니다.



**앱 설치형 광고 테스트**

1) https://developers.facebook.com -> Tools & Support -> App Ads Helper로 이동합니다.

![fb01](http://www.wisetracker.co.kr/wp-content/uploads/2018/01/fb113.png)

2) 테스트할 앱을 선택한 후 페이지 하단 Developer Tool의 Test Deep Link를 클릭합니다.

![fb02](http://www.wisetracker.co.kr/wp-content/uploads/2018/01/fb115.jpg)

3) PC에서 Android Studio를 실행하고 테스트 단말기를 USB로 연결하여 관련 로그를 logcat으로 확인할 수 있도록 준비합니다. 앱이 수신한 Deep Link를 logcat에서 확인해야 하기 때문입니다.

4) Facebook 테스트 페이지로 돌아갑니다. 앱의 커스텀 스키마를 Send Deep Link에 입력하고 *Send to Android* 를 클릭합니다. 이 때 **Send Deferred는 반드시 체크**되어 있어야 합니다.

![fb03](http://www.wisetracker.co.kr/wp-content/uploads/2018/01/fb116.jpg)

5) 테스트 단말기의 Facebook 앱에 알림이 전송됩니다. 해당 알림를 탭하면 플레이스토어로 진입 할 것입니다. 플레이스토어에서 앱을 다운로드 받지 마시고, 6)번 단계로 진행하십시오.

![fb04](http://www.wisetracker.co.kr/wp-content/uploads/2018/01/fb117.png)

6) 안드로이드 스튜디오를 통해 해당 앱을 실행하고 로그를 확인 합니다. Facebook에 입력한 커스텀 스키마가 아래 그림처럼 logcat에서 보인다면 페이스북 앱 설치 광고에 대한 분석이 가능합니다. 

![fb05](http://www.wisetracker.co.kr/wp-content/uploads/2018/01/fb118.png)





**앱 참여형 광고 테스트**

() 앱 참여 광고를 진행하는 경우 이미 앱을 설치한 사용자가 광고를 클릭하여 앱을 실행하는 시점에 페이스북 광고에 등록한 딥 링크값이 동작하는지 여부를 확인하면 됩니다.

8) 앱 참여 광고 등록 시 사용한 딥 링크를 Send Deep Link 영역에 입력 후 Send to Android 버튼을 클릭합니다. 이 때 Send Deferred는 반드시 체크 해제되어 있어야 합니다.

9) 테스트 단말기의 Facebook 앱에 알림이 전송됩니다. 해당 링크를 클릭하여 앱을 실행합니다.

10) Facebook에 입력한 커스텀 스키마가 아래 그림처럼 logcat에서 보인다면 페이스북 앱  광고에 대한 분석이 가능합니다. 




### Push Notification 발송

Wisetracker SDK를 연동하면 타겟 유저에게 원하는 시간에 푸시 메시지를 발송하여 인게이지먼트를 이끌어 낼 수 있습니다. 이 설정을 적용하기 전에 반드시 아래 전제조건을 확인해주세요.



#### 전제조건

* 앱에 Firebase가 설치되어 있어야 합니다. 와이즈트래커는 Android 환경에서 Firebase Messaging Service를 활용해 푸시 메시지를 발송합니다.
* 와이즈트래커에서 프리미엄 등급 이상의 유료 플랜을 구독해야 합니다. 프리미엄 이하의 플랜은 푸시 메시지 발송 기능을 지원하지 않습니다.



#### 푸시 토큰 수집

푸시 메시지를 보내기 위해서는 우선 푸시 토큰을 수집해야 합니다. 우선 Activity 수준에서 푸시 토큰을 수집할 수 있도록 아래와 같이 설정합니다.

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
	FirebaseInstanceId
		.getInstance()
		.getInstanceId()
		.addOnSuccessListener(context, new OnSuccessListener() {
			@Override
			public void onSuccess(InstanceIdResult instanceIdResult) {
				String newToken = instanceIdResult.getToken();
				// call Wisetracker API
				DOT.setPushToken(newToken);
			}
		});
}
```

그리고 `FirebaseMessagingService`를 상속받은 `Service` 수준에서도 푸시 토큰을 수집하도록 아래와 같이 설정합니다.

```java
public class FcmService extends FirebaseMessagingService {
	@Override
	public void onNewToken(String token) {
		super.onNewToken(token);
		// call Wisetracker API
		DOT.setPushToken(token);
	}
}
```



#### 푸시 메시지 수신 측정

푸시 메시지가 단말기에 수신된 것을 측정하기 위해 `onMessageReceived` 메소드에 `setPushReceiver`를 추가합니다.

```java
public class FcmService extends FirebaseMessagingService {

	@Override
	public void onMessageReceived(RemoteMessage remoteMessage) {
		super.onMessageReceived(remoteMessage);
		// call Wisetracker API
		DOT.setPushReceiver(remoteMessage.toIntent());
	}
}
```



#### 푸시 메시지 클릭 측정

푸시 메시지를 클릭하는 것을 측정하기 위해 푸시 메시지를 통해 진입하는 `Activity`에 `setPushClick`을 추가합니다.

```java
public class PushClickActivity extends AppCompatActivity {

	@Override
	protected void onCreate(@Nullable Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		// call Wisetracker API
		DOT.setPushClick(getIntent());
	}

	@Override
	protected void onNewIntent(Intent intent) {
		super.onNewIntent(intent);
		// call Wisetracker API
		DOT.setPushClick(getIntent());
	}
}
```



#### 푸시 메시지 설정

수신 받은 푸시 메시지를 사용 환경에 맞게 적용해 주세요.


```java
Notification notification = new NotificationCompat.Builder(context, /* YOUR NOTIFICATION CHANNEL ID */"1")
	.setAutoCancel(true)
	.setDefaults(Notification.DEFAULT_ALL)
	.setContentIntent(YOUR PENDING INTENT)
	.setContentTitle("YOUR TITLE")
	.setContentText("YOUR CONTENT")
	.setSmallIcon(R.mipmap.app_icon)
	.setStyle(new NotificationCompat.BigPictureStyle()
				.bigPicture(/* YOUR BITMAP */ bitmap)
				.bigLargeIcon(/* YOUR BITMAP */ bitmap)
				.setBigContentTitle("YOUR BIG IMAGE TITLE")
				.setSummaryText("YOUR BIG IMAGE SUMMARY")
			)
	.build();
NotificationManager notificationManager = (NotificationManager) context.getSystemService(Context.NOTIFICATION_SERVICE);
notificationManager.notify(/* YOUR NOTIFICATION ID */0, notification
```
