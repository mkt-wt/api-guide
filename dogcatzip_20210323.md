# Wisetracker Integration Guide
'개고집' 앱에서 추가 데이터를 측정하는데 필요한 코드를 적용하는 방법을 안내하는 문서입니다. 진행 중에 발생하는 기술적인 이슈는 아래 담당 개발자에게 연락 주시기 바랍니다.

> 허원철 팀장, fornew21c@wisetracker.co.kr, tech@wisetracker.co.kr



# Index

* [와이즈트래커 초기화 시점 변경](./dogcatzip_20210323.md#와이즈트래커-초기화-시점-변경)
* [제품 보러가기 버튼 클릭 측정](./dogcatzip_20210323.md#이벤트-화면-내-제품-보러가기-버튼-클릭-측정)
* [제품 구매하러 가기 버튼 클릭 측정](./dogcatzip_20210323.md#이벤트-화면-내-제품-보러가기-버튼-클릭-측정)
* [적용 후 검증](./dogcatzip_20210323.md#적용-후-검증)



## 와이즈트래커 초기화 시점 변경

최초에는 Flutter의 `initState()`에서 와이즈트래커를 초기화 하도록 안내 드렸으나, 더 정확한 측정을 위해서는 Flutter가 아닌 Native에서 초기화 될 필요가 있습니다. 이에 따라 `DOT.initialization()` 위치를아래 예시와 같이 수정해 주시기 바랍니다.

* 코드 적용 시점 - 본인인증이 완료되는 시점에 적용해 주시기 바랍니다. 총 3곳에서 본인인증이 가능한 것으로 전달 받았으며, 어디에서 인증이 완료되는지에 따라 서로 다른 값이 코드에 추가되어야 합니다.


### 기존 코드

```dart
void initState() {
    super.initState();
    DOT.initialization();
}
```

### Android 수정

Application을 상속받는 클래스가 아닌 `Activity`를 상속받는 기본 화면의 `onCreate()` 함수에 적용해 주세요.

```java
public class MainActivity extends AppCompatActivity {
    @Override
        protected void onCreate(Bundle savedInstanceState) {
            DOT.initialization(this); // 와이즈트래커 초기화
        }
}
```

### iOS 수정

AppDelegate의 `didFinishLaunchingWithOptions` 함수에 다음과 같이 적용합니다.

```swift
import DOT
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    DOT.initialization(launchOptions, application: application) // 와이즈트래커 초기화
}
```


## 이벤트 화면 내 '제품 보러가기' 버튼 클릭 측정

이벤트 화면에 새로 생긴 '제품 보러가기' 버튼의 클릭 횟수를 측정하기 위한 코드로, 버튼이 클릭되는 시점에 코드를 추가해 주시기 바랍니다.

### 분석 코드

```dart
var event = {};
event["event"] = "event_view_product";
event["event_id"] = "이벤트 고유번호";
event["event_name"] = "이벤트 명칭";
event["page_id"] = "event detail";
DOT.logEvent(event);
```

## 이벤트 화면 내 '제품 구매하러 가기' 버튼 클릭 측정

이벤트 화면에 새로 생긴 '제품 구매하러 가기' 버튼의 클릭 횟수를 측정하기 위한 코드로, 버튼이 클릭되는 시점에 코드를 추가해 주시기 바랍니다.

### 분석 코드

```dart
var event = {};
event["event"] = "event_buy_product";
event["event_id"] = "이벤트 고유번호";
event["event_name"] = "이벤트 명칭";
event["page_id"] = "event detail";
DOT.logEvent(event);
```

## 적용 후 검증

상기 내용을 적용한 테스트앱을 아래 내용을 참고하여 저희쪽으로 보내주시기 바랍니다. 앱이 배포되기 이전에 저희가 확인을 해보고 문제가 없는 상태에서 배포될 수 있도록 도와드리기 위해 본 과정을 진행하고 있습니다.

1. APK 파일은 wisetracker@naver.com 으로 보내주시기 바랍니다.
2. iOS 앱은 fornew21c@wisetracker.co.kr, humblejohn@wisetracker.co.kr 계정을 테스트플라이트로 초대하여 공유해 주시기 바랍니다.
3. APK와 테스트플라이트 초대를 해주셨다면, 이렇게 앱을 공유해 주셨다는 것을 저희 담당자에게 메일로 안내해 주시기 바랍니다.
4. 안내해주실때 앱의 메인 액티비티를 호출하는 커스텀 스키마 정보를 함께 알려주시기 바랍니다. (AOS, iOS 모두)

