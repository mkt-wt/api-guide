# Wisetracker Integration Guide
'코베' 앱에 연동할 와이즈트래커 인앱 이벤트를 안내하는 문서입니다.

# Index
* [회원가입](./cobe.md#회원가입)
* [사전등록 완료](./cobe.md#사전등록-완료)
* [상품조회](./cobe.md#상품조회)
	* [적용예시](./cobe.md#적용예시)
* [구매완료](./cobe.md#구매완료)
	* [적용예시](./cobe.md#적용예시-1)
* [적용 후 데이터 검증](./cobe.md#적용-후-데이터-검증)
	* [AOS](./cobe.md#AOS)
	* [iOS](./cobe.md#iOS)


## 회원가입
유저가 앱에서 회원가입을 마치면 도달하게 되는 '회원가입 완료화면'에 아래 코드를 추가합니다.
``` html
<!-- script type이 wisetracker인 점 유의 -->
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("RGR");
	WiseTracker.setGoal("g1", 1);
	WiseTracker.sendTransaction();
</script>
```

## 사전등록 완료
유저가 앱에서 정상적으로 사전등록을 마치면 나타나는 alert에 아래 코드를 추가합니다.

![사전등록 완료](http://www.wisetracker.co.kr/wp-content/uploads/2020/03/cobe000.jpg)

``` javascript
<script>
	alert('...바코드를 제시한 후 입장해주세요.');
	// 와이즈트래커 분석코드 추가
	WiseTracker.setGoal("g3", 1);
	WiseTracker.sendTransaction();
</script>
```

## 상품조회
코베몰에 있는 상품의 상세화면에 아래 코드를 추가합니다.
``` html
<!-- script type이 wisetracker인 점 유의 -->
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setProduct("상품코드", "상품명")
	WiseTracker.setPageIdentity("PDV");
</script>
```

### 적용예시
유저가 '[상담예약 EVENT] 예약하고 선물받으세요!' 상품 상세화면에 도달한 경우.
``` html
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setProduct("해당상품의 고유한 상품코드", "[상담예약 EVENT] 예약하고 선물받으세요!")
	WiseTracker.setPageIdentity("PDV");
</script>
```

## 구매완료
유저가 코베몰에서 상품을 구매 또는 예약하게되면 도달하는 구매완료화면에 아래 코드를 추가합니다. 
``` html
<!-- script type이 wisetracker인 점 유의 -->
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setOrderProductArray(["A상품코드","B상품코드"]);
	WiseTracker.setOrderQuantityArray([A상품수량, B상품수량]);
	WiseTracker.setOrderAmountArray([A상품결제액, B상품결제액]);
	WiseTracker.setOrderNo("주문번호");
	WiseTracker.setPageIdentity("ODR");
	WiseTracker.sendTransaction();
</script>
```

### 적용예시
유저가 '[상담예약 EVENT] 예약하고 선물받으세요!' 상품 1개를 구매한 경우.
``` html
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setOrderProductArray(["상품코드"]); //[상담예약 EVENT] 예약하고 선물받으세요! 상품의 고유 상품코드 입력
	WiseTracker.setOrderQuantityArray([1]);
	WiseTracker.setOrderAmountArray([1]); //유저가 실제 결제한 금액을 입력
	WiseTracker.setOrderNo("TR9821938");
	WiseTracker.setPageIdentity("ODR");
	WiseTracker.sendTransaction();
</script>
```

유저가 '[상담예약 EVENT] 예약하고 선물받으세요!' 상품 1개와 '[루솔박람회 특가EVENT] 이유식 계약하고 최대 63%할인' 상품 2개를 구매한 경우.
``` html
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setOrderProductArray(["A상품코드","B상품코드"]);
	WiseTracker.setOrderQuantityArray([1, 2]);
	WiseTracker.setOrderAmountArray([1, 2]);
	WiseTracker.setOrderNo("TR9939893");
	WiseTracker.setPageIdentity("ODR");
	WiseTracker.sendTransaction();
</script>
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

![iOS Debug Mode](http://www.wisetracker.co.kr/wp-content/uploads/2019/05/ios-debug.png)

``` swift
<key>WiseTrackerLogState</key>
<string>true</string>
```
