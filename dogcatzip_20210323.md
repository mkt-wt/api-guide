# Wisetracker Integration Guide
'개고집' 앱에서 추가 데이터를 측정하는데 필요한 코드를 적용하는 방법을 안내하는 문서입니다. 진행 중에 발생하는 기술적인 이슈는 아래 담당 개발자에게 연락 주시기 바랍니다.

> 허원철 팀장, fornew21c@wisetracker.co.kr, tech@wisetracker.co.kr



# Index

* [와이즈트래커 초기화 시점 변경](./dogcatzip_20210323.md#와이즈트래커-초기화-시점-변경)
* [제품 보러가기 버튼 클릭 측정](./dogcatzip_20210323.md#이벤트-화면-내-제품-보러가기-버튼-클릭-측정)
* [제품 구매하러 가기 버튼 클릭 측정](./dogcatzip_20210323.md#이벤트-화면-내-제품-보러가기-버튼-클릭-측정)
* [EWG 등급 버튼 클릭 측정](./dogcatzip_20210323.md#EWG-등급-버튼-클릭-측정)
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

## EWG 등급 버튼 클릭 측정

1. 제품 상세화면에 '식품첨가물'을 표시하는 영역이 있으며, 해당 영역 클릭 시 *이미 와이즈트래커 코드가 적용되어 있습니다.*
2. 특정 카테고리에 속하는 제품들은 해당 영역에 '식품첨가물'이 아닌 'EWG 등급'이 표시되도록 변경되었다고 합니다.
3. 이에 따라 기존의 식품첨가물 버튼과, 새로 생긴 EWG 등급 버튼의 클릭을 구분할 필요가 있으며 아래 내용을 참고하여 코드를 적용해 주시기 바랍니다.

* 코드 적용 시점 - 제품 상세 화면에서 해당 버튼이 클릭되는 시점에 적용해 주세요.

### 분석 코드

```dart
var event = {};
event["event"] = "버튼 종류"; // 여기에 들어갈 값은 아래 '변경사항' 부분을 참고해 주세요
event["page_id"] = "product detail";
var product = {};
product["product_id"] = "제품 고유번호";
product["product_name"] = "제품 명칭";
product["category_name_a"] = "제품이 속한 카테고리 명칭";
product["brand_name"] = "제품의 브랜드 명칭";
event["product"] = product;
DOT.logEvent(event);
```

### 변경사항

기존에 적용되어 있는 코드에는 위의 `버튼 종류` 부분에 `food_additives` 값이 들어가도록 되어 있습니다. 이것을 아래 카테고리에 포함되는 모든 제품들에 한해서만 `ewg_additives` 라는 값으로 변경해 주시기 바랍니다.

* 강아지 > 목욕/미용 > 샴푸/린스
* 강아지 > 목욕/미용 > 에센스/향수
* 강아지 > 목욕/미용 > 그 외
* 강아지> 배변/위생 > 물티슈
* 고양이 > 목욕/미용 > 샴푸/린스
* 고양이 > 목욕/미용 > 에센스/향수
* 고양이 > 목욕/미용 > 그 외
* 고양이> 배변/위생 > 물티슈


## 적용 후 검증

상기 내용을 적용한 테스트앱을 아래 내용을 참고하여 저희쪽으로 보내주시기 바랍니다. 앱이 배포되기 이전에 저희가 확인을 해보고 문제가 없는 상태에서 배포될 수 있도록 도와드리기 위해 본 과정을 진행하고 있습니다.

1. APK 파일은 wisetracker@naver.com 으로 보내주시기 바랍니다.
2. iOS 앱은 fornew21c@wisetracker.co.kr, humblejohn@wisetracker.co.kr 계정을 테스트플라이트로 초대하여 공유해 주시기 바랍니다.
3. APK와 테스트플라이트 초대를 해주셨다면, 이렇게 앱을 공유해 주셨다는 것을 저희 담당자에게 메일로 안내해 주시기 바랍니다.
4. 안내해주실때 앱의 메인 액티비티를 호출하는 커스텀 스키마 정보를 함께 알려주시기 바랍니다. (AOS, iOS 모두)

