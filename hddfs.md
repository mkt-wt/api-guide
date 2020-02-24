# Wisetracker Integration Guide
'현대백화점면세점 중문' 앱에 와이즈트래커를 연동하는데 필요한 기술문서입니다. 연동 중 발생하는 문의사항은 아래 담당자에게 연락 주시기 바랍니다.

> 정주온, humblejohn@wisetracker.co.kr

# Index
* [SDK 삽입 (AOS & iOS)](./hddfs.md#SDK-삽입)
* [분석 API](./hddfs.md#분석-API)
	* [Hybrid 영역 태깅 참고사항](./hddfs.md#Hybrid-영역-태깅-참고사항)
	* [로그인 분석](./hddfs.md#로그인-분석)
		* [주의사항](./hddfs.md#주의사항)
		* [분석 코드](./hddfs.md#분석-코드)
		* [예시](./hddfs.md#예시)
	* [회원 가입 분석](./hddfs.md#회원-가입-분석)
		* [분석 코드](./hddfs.md#분석-코드-1)
	* [상품 분석](./hddfs.md#상품-분석)
		* [주의사항](./hddfs.md#주의사항-1)
		* [분석 코드](./hddfs.md#분석-코드-2)
		* [예시](./hddfs.md#예시-1)
	* [장바구니 담기 분석](./hddfs.md#장바구니-담기-분석)
		* [주의사항](./hddfs.md#주의사항-2)
		* [분석 코드](./hddfs.md#분석-코드-3)
		* [예시](./hddfs.md#예시-2)
	* [관심 상품 등록 분석](./hddfs.md#관심-상품-등록-분석)
		* [분석 코드](./hddfs.md#분석-코드-4)
		* [예시](./hddfs.md#예시-3)
	* [쿠폰 받기 분석](./hddfs.md#쿠폰-받기-분석)
		* [분석 코드](./hddfs.md#분석-코드-5)
	* [적립금 받기 분석](./hddfs.md#적립금-받기-분석)
		* [분석 코드](./hddfs.md#분석-코드-6)
	* [내부 검색어 분석](./hddfs.md#내부-검색어-분석)
		* [분석 코드](./hddfs.md#분석-코드-7)
		* [예시](./hddfs.md#예시-4)
	* [주문 분석](./hddfs.md#주문-분석)
		* [주의사항](./hddfs.md#주의사항-3)
		* [분석 코드](./hddfs.md#분석-코드-8)
		* [예시 A](./hddfs.md#예시-A)
		* [예시 B](./hddfs.md#예시-B)
* [적용 후 데이터 검증](./hddfs.md#적용-후-데이터-검증)
	* [AOS](./hddfs.md#AOS)
	* [iOS](./hddfs.md#iOS)


# SDK 삽입
각 플랫폼별 온라인 가이드를 참고해서 SDK를 삽입해 주시면 됩니다. 아래 가이드의 3번 '필수 연동 API' 까지는 반드시 적용해 주셔야 하며, 'Facebook 분석을 위한 연동'과 WAFI 는 적용하지 않습니다.

-[AOS](https://bintray.com/beta/#/tracker/maven/SDK_V1?tab=readme)

-[iOS](https://github.com/WisetrackerTechteam/wisetrackerSDK)

## 분석 API
데이터 분석용 API와 태깅 방법을 안내합니다.

### Hybrid 영역 태깅 참고사항
Hybrid 영역에 태깅한 분석 API가 Native에 있는 SDK를 참조할 수 있도록 script의 `type`과 `id`를 설정합니다.
``` html
<!-- refer to Wisetracker SDK -->
<script type="wisetracker/text" id="wiseTracker">
	// APIs
</script>
```

### 로그인 분석
유저가 앱에 로그인 하는 횟수, 로그인 유형, 로그인한 유저의 인구통계 정보를 분석할 수 있게 됩니다.

#### 주의사항
1) 로그인 완료 처리하는 시점에 분석 코드를 추가합니다.
2) 총 7가지 방법으로 로그인 할 수 있습니다. 아래 표를 참고하여 각 로그인 유형에 맞는 코드를 입력해 주시기 바랍니다.

로그인 유형 | 유형 코드
-------- | --------
일반(ID로그인) | A
Weibo | B
QQ | C
Wechat | D
Alipay | E
Baidu | F
H-Point | G

3) 로그인한 유저의 성별 정보는 아래 표를 참고하여 입력해 주시기 바랍니다.

성별 | 성별 코드
-------- | --------
여성 | F
남성 | M
기타 | U

4) 로그인한 유저의 연령대 정보는 아래 표를 참고하여 입력해 주시기 바랍니다.

연령대 | 연령대 코드
-------- | --------
10세 미만 | A
10~19세 | B
20~24세 | C
25~29세 | D
30~34세 | E
35~39세 | F
40~44세 | G
45~49세 | H
50~54세 | I
55~59세 | J
60~64세 | K
65~69세 | L
70세 이상 | M

#### 분석 코드
``` java
WiseTracker.setPageIdentity("LIR");
WiseTracker.setGoal("g2", 1);
WiseTracker.setUserAttribute("uvp1", "로그인 유형 코드");
WiseTracker.setGender("성별코드");
WiseTracker.setAge("연령대 코드");
WiseTracker.sendTransaction();
```

#### 예시
30세 남성이 Weibo 계정으로 로그인 하는 경우, 로그인 완료 시점에 아래 코드 추가
``` html
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("LIR");
	WiseTracker.setGoal("g2", 1);
	WiseTracker.setUserAttribute("uvp1", "B");
	WiseTracker.setGender("M");
	WiseTracker.setAge("E");
	WiseTracker.sendTransaction();
</script>
```

### 회원 가입 분석
앱에서 회원으로 가입하는 횟수를 분석할 수 있게 됩니다. 회원가입 완료 화면에 아래 코드를 추가해 주시기 바랍니다.

#### 분석 코드
``` java
WiseTracker.setPageIdentity("RGR");
WiseTracker.setGoal("g1", 1);
WiseTracker.sendGoalData();
```

### 상품 분석
각 상품의 조회수 등을 분석할 수 있게 됩니다. 상품 상세 화면에 아래 코드를 추가해 주세요.

#### 주의사항
1) BO에서 상품을 생성하면 상품 분석 코드가 상품 상세 화면에 포함되도록 작업해 주시기 바랍니다.
2) 일부 상품(아래에 예시 있음)들은 별도의 UI를 사용하고 있습니다. 현 시점에는 해당 상품들엔 상품 분석 코드가 누락된채 사이트에 올라와 있습니다.
3) 아마 BO를 통해 해당 상품이 생성되는 부분에 상품 분석 코드가 빠져 있는 것 같습니다. BO에서 발행하는 모든 상품에 상품 분석 코드가 들어가도록 작업해 주시기 바랍니다.

![이미지](http://www.wisetracker.co.kr/wp-content/uploads/2019/11/002.jpg)

#### 분석 코드
``` java
WiseTracker.setProduct("상품코드", "상품명");
WiseTracker.setCustomMvtTag("mvt1", "브랜드명");
WiseTracker.setPageIdentity("PDV");
```

#### 예시
유저가 新秀丽 VENON BACKPACK BLACK背包 상품 페이지 조회 시, 해당 페이지에 아래 코드 추가
``` html
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setProduct("10368200000704", "新秀丽 VENON BACKPACK BLACK背包");
	WiseTracker.setCustomMvtTag("mvt1", "新秀丽");
	WiseTracker.setPageIdentity("PDV");
</script>
```

### 장바구니 담기 분석
각 상품이 장바구니에 추가되는 횟수를 분석할 수 있게 됩니다.

#### 주의사항
장바구니 담기 펑션 안에 아래 코드를 추가해 주시기 바랍니다.

#### 분석 코드
``` java
WiseTracker.setProduct("상품코드", "상품명");
WiseTracker.setCustomMvtTag("mvt1", "브랜드명");
WiseTracker.setPageIdentity("OCA");
WiseTracker.sendTransaction();
```

#### 예시
유저가 新秀丽 VENON BACKPACK BLACK背包 상품을 장바구니에 잠은 경우, 해당 펑션에 아래 코드 추가
``` javascript
function addCartExampleFunction (){
	// 장바구니 이벤트 안에서 호출함 
	WiseTracker.setProduct("10368200000704", "新秀丽 VENON BACKPACK BLACK背包");
	WiseTracker.setCustomMvtTag("mvt1", "新秀丽");
	WiseTracker.setPageIdentity("OCA");
	WiseTracker.sendTransaction();
}
```

### 관심 상품 등록 분석
각 상품이 관심 상품으로 등록되는 횟수를 분석할 수 있게 됩니다. 상품이 관심 상품으로 등록되는 시점에 아래 코드를 추가해 주세요.

#### 분석 코드
``` java
WiseTracker.setGoalProduct("상품코드");
WiseTracker.setGoalCustomMvtTag("mvt1", "브랜드명");
WiseTracker.setGoal("g4", 1);
WiseTracker.sendGoalData();
```

#### 예시
유저가 新秀丽 VENON BACKPACK BLACK背包 상품을 관심 상품으로 등록한 경우, 해당 이벤트에 아래 코드 추가
``` javascript
function mergeMyGoosExample (){
	// 정상적으로 상품이 관심 상품으로 추가된 경우 호출
	WiseTracker.setGoalProduct("10368200000704");
	WiseTracker.setGoalCustomMvtTag("mvt1", "新秀丽");
	WiseTracker.setGoal("g4", 1);
	WiseTracker.sendGoalData();
}
```

### 쿠폰 받기 분석
앱에서 쿠폰을 발급 받은 횟수를 분석할 수 있게 됩니다. 쿠폰 발급 시점에 아래 코드를 추가해 주세요.

#### 분석 코드
``` java
WiseTracker.setGoal("g5", 1);
WiseTracker.sendGoalData();
```

### 적립금 받기 분석
앱에서 적립금을 발급 받은 횟수를 분석할 수 있게 됩니다. 적립금 발급 시점에 아래 코드를 추가해 주세요.

#### 분석 코드
``` java
WiseTracker.setGoal("g6", 1);
WiseTracker.sendGoalData();
```

### 내부 검색어 분석
앱 내의 검색기능으로 검색한 키워드와 검색 횟수를 분석할 수 있게 됩니다. 검색 완료 화면에 아래 코드를 추가해 주세요.

#### 분석 코드
``` java
WiseTracker.setSearchKeyword("검색어");
WiseTracker.setSearchKeywordResult(검색결과수);
WiseTracker.setPageIdentity("SEARCH");
```

#### 예시
유저가 앱 내에서 '赫莲娜' 를 검색한 경우, 검색 완료 화면에 아래 코드 추가
```html
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setSearchKeyword("赫莲娜");
	WiseTracker.setSearchKeywordResult(41);
	WiseTracker.setPageIdentity("SEARCH");
</script>
```

### 주문 분석
앱 내에서 구매 완료한 상품, 구매 수량, 결제금액 등을 분석할 수 있게 됩니다.

#### 주의사항
1) 구매 완료 화면에 아래 분석 코드를 추가해 주세요.
2) 결제 금액은 유저가 실제 지불해야 할 금액(쿠폰, 적립금 할인을 차감한 최종금액)을 달러화 단위로 입력해 주세요.
3) 1회 주문에 다수의 상품을 구매하는 경우, 콤마(,)로 value를 구분해서 입력해 주세요.

#### 분석 코드
``` java
WiseTracker.setOrderProductArray(["A상품코드", "B상품코드"]);
WiseTracker.setOrderQuantityArray([A상품수량, B상품수량]);
WiseTracker.setOrderAmountArray([A결제금액, B결제금액]);
WiseTracker.setOrderCustomMvtTagArray(["A브랜드명", "B브랜드명"]);
WiseTracker.setPageIdentity("ODR");
WiseTracker.sendTransaction();
```

#### 예시 A
유저가 新秀丽 VENON BACKPACK BLACK背包 상품을 2개 구매한 경우
``` html
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setOrderProductArray(["10368200000704"]);
	WiseTracker.setOrderQuantityArray([2]);
	WiseTracker.setOrderAmountArray([650]);
	WiseTracker.setOrderCustomMvtTagArray(["新秀丽"]);
	WiseTracker.setOrderNo("O12345678");
	WiseTracker.setPageIdentity("ODR");
	WiseTracker.sendTransaction();
</script>
```

#### 예시 B
유저가 新秀丽 VENON BACKPACK BLACK背包 상품 2개와, M/K PALETTE 眼影盘 #BEACH MUSE 상품 1개를 구매한 경우
``` html
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setOrderProductArray(["10368200000704", "56023270012001"]);
	WiseTracker.setOrderQuantityArray([2, 1]);
	WiseTracker.setOrderAmountArray([650, 27]);
	WiseTracker.setOrderCustomMvtTagArray(["新秀丽", "3CE"]);
	WiseTracker.setOrderNo("O5678901234");
	WiseTracker.setPageIdentity("ODR");
	WiseTracker.sendTransaction();
</script>
```

## 적용 후 데이터 검증
SDK와 API가 올바르게 적용 되었는지 확인하기 위해서는 아래 코드(디버그 모드 활성화)를 적용한 테스트 앱을 저희 쪽으로 보내주시면 됩니다. 보내주신 테스트 앱에서 데이터를 확인한 후 결과에 대해서 회신 드리고 있습니다.

### AOS
AndroidManifest.xml 파일에 아래 메타 데이터 태그를 추가합니다.
``` java
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
