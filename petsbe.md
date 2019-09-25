# Wisetracker Integration Guide
'펫츠비'앱에 와이즈트래커를 연동하는데 필요한 기술문서입니다. 연동 중 발생하는 문의사항은 아래 담당자에게 연락 주시기 바랍니다.

> 정주온, humblejohn@wisetracker.co.kr

# Index
* [SDK 삽입 (AOS & iOS)](./petsbe.md#SDK-삽입)
* [분석 API](./petsbe.md#분석-API)
	* [Hybrid 영역 태깅 참고사항](./petsbe.md#Hybrid-영역-태깅-참고사항)
	* [회원 가입 분석](./petsbe.md#회원-가입-분석)
		* [분석 코드](./petsbe.md#분석-코드)
	* [상품 분석](./petsbe.md#상품-분석)
		* [분석 코드](./petsbe.md#분석-코드-1)
	* [장바구니 담기 분석](./petsbe.md#장바구니-담기-분석)
		* [분석 코드](./petsbe.md#분석-코드-2)
	* [구매 분석](./petsbe.md#구매-분석)
		* [분석 코드](./petsbe.md#분석-코드-3)
		* [예시](./petsbe.md#예시)
	* [엔페이 구매 분석](./petsbe.md#엔페이-구매-분석)
		* [분석 코드](./petsbe.md#분석-코드-4)
* [적용 후 데이터 검증](./petsbe.md#적용-후-데이터-검증)
	* [AOS](./petsbe.md#AOS)
	* [iOS](./petsbe.md#iOS)


# SDK 삽입
각 플랫폼별 온라인 가이드를 참고해서 SDK를 삽입해 주시면 됩니다.

#### -[AOS](https://bintray.com/beta/#/tracker/maven/SDK_V1?tab=readme)
#### -[iOS](https://github.com/WisetrackerTechteam/wisetrackerSDK)

## 분석 API
앱에 SDK를 삽입한 이후 아래 API를 구현합니다.

### Hybrid 영역 태깅 참고사항
Hybrid 영역에 태깅한 분석 API가 Native에 있는 SDK를 참조해서 동작하는 구조입니다. 이렇게 동작할 수 있도록 script의 `type`과 `id`를 아래와 같이 설정합니다.
``` html
<!-- to Wisetracker SDK -->
<script type="wisetracker/text" id="wiseTracker">
	// APIs
</script>
```

### 회원 가입 분석
유저가 앱에서 회원가입을 마치면 도달하게 되는 '회원가입 완료화면'에 아래 코드를 추가합니다.

#### 분석 코드
``` html
<!-- 회원가입 완료 화면에 코드 추가 -->
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("RGR");
	WiseTracker.setGoal("g1", 1);
	WiseTracker.sendGoalData();
</script>
```

### 상품 분석
개별 상품들의 상세 페이지에 아래 코드를 추가합니다.

#### 분석 코드
``` html
<!-- 상품 상세 화면에 코드 추가 -->
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setProduct("상품코드", "상품명");
	WiseTracker.setProductCategoty("카테고리코드", "카테고리명");
	WiseTracker.setPageIdentity("PDV");
</script>
```

### 장바구니 담기 분석
유저가 장바구니에 상품을 담는 펑션에 아래 코드를 추가합니다.

#### 분석 코드
``` javascript
function addCartExampleFunction (){
	// 장바구니 이벤트 안에서 호출함
	WiseTracker.setProduct("상품코드", "상품명");
	WiseTracker.setProductCategory("카테고리코드", "카테고리명");
	WiseTracker.setPageIdentity("OCA");
	WiseTracker.sendTransaction();
)
```

### 구매 분석
구매완료 화면에 아래 코드를 추가합니다.

#### 분석 코드
``` html
<!-- 구매완료 화면에 코드 추가 -->
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setOrderProductArray("상품코드", "상품코드");
	WiseTracker.setOrderProductCategoryArray("카테고리코드", "카테고리코드");
	WiseTracker.setOrderQuantityArray(구매수량, 구매수량);
	WiseTracker.setOrderAmountArray(구매금액, 구매금액);
	WiseTracker.setOrderNo("주문번호");
	WiseTracker.setPageIdentity("ODR");
	WiseTracker.sendTransaction();
</script>
```

#### 예시
25,000원짜리 상품을 2개 구매
``` html
<!-- 구매완료 화면에 코드 추가 -->
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setOrderProductArray("PD001");
	WiseTracker.setOrderProductCategoryArray("CG001");
	WiseTracker.setOrderQuantityArray(2);
	WiseTracker.setOrderAmountArray(50000);
	WiseTracker.setOrderNo("TR1234");
	WiseTracker.setPageIdentity("ODR");
	WiseTracker.sendTransaction();
</script>
```

10,000원짜리 상품 1개와 25,000원짜리 상품 2개 구매
``` html
<!-- 구매완료 화면에 코드 추가 -->
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setOrderProductArray("PD002", "PD001");
	WiseTracker.setOrderProductCategoryArray("CG001", "CG001");
	WiseTracker.setOrderQuantityArray(1, 2);
	WiseTracker.setOrderAmountArray(10000, 50000);
	WiseTracker.setOrderNo("TR2938");
	WiseTracker.setPageIdentity("ODR");
	WiseTracker.sendTransaction();
</script>
```

### 엔페이 구매 분석
'엔페이로 구매하기' 버튼의 클릭 이벤트에 아래 코드를 추가합니다.

#### 분석 코드
``` javascript
onclick = "
	WiseTracker.setOrderNPaymentId("#MALL_MANAGE_CODE#"); //고유 MALL_MANAGE_CODE 입력
	WiseTracker.sendTransaction();
"
```

## 적용 후 데이터 검증
SDK와 API가 올바르게 적용 되었는지 확인하기 위해서는 아래 코드(디버그 모드 활성화)를 적용한 테스트 앱을 저희 쪽으로 보내주시면 됩니다. 보내주신 테스트 앱에서 데이터를 확인한 후 결과에 대해서 회신 드리고 있습니다.

### AOS
AndroidManifest.xml 파일에 아래 메타 데이터 태그를 추가합니다.
``` kotlin
<meta-data android:name="WiseTrackerLogState" android:value="true" />
// 개발용 테스트 앱에는 true로, 배포용 앱에는 false로 설정
```

### iOS
Info.plist 파일에 아래 그림과 같이 값을 추가 합니다.

![iOS Debug Mobe](http://www.wisetracker.co.kr/wp-content/uploads/2019/05/ios-debug.png)

``` swift
<key>WiseTrackerLogState</key>
<string>true</string>
```
