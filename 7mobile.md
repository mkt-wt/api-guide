# Wisetracker Integration Guide
'SK 7mobile' 사이트에 와이즈트래커 분석코드를 삽입하는데 필요한 기술문서입니다. 작업 중 발생하는 문의사항은 아래 담당자에게 연락 주시기 바랍니다.

> 정주온, humblejohn@wisetracker.co.kr

# Index
* [공통 스크립트 삽입](./7mobile.md#공통-스크립트-삽입)
* [분석 코드](./7mobile.md#분석-코드)
	* [로그인 분석](./7mobile.md#로그인-분석)
		* [주의사항](./7mobile.md#주의사항)
		* [코드](./7mobile.md#코드)
		* [태깅 예시](./7mobile.md#태깅-예시)
	* [회원가입 분석](./7mobile.md#회원가입-분석)
		* [코드](./7mobile.md#코드-1)
		* [태깅 예시](./7mobile.md#태깅-예시-1)
	* [상품 분석](./7mobile.md#상품-분석)
		* [주의사항](./7mobile.md#주의사항-1)
		* [코드](./7mobile.md#코드-2)
		* [태깅 예시](./7mobile.md#태깅-예시-2)
	* [요금제 변경 분석](./7mobile.md#요금제-변경-분석)
		* [주의사항](./7mobile.md#주의사항-2)
		* [코드](./7mobile.md#코드-3)
		* [태깅 예시](./7mobile.md#태깅-예시-3)
	* [구매 분석](./7mobile.md#구매-분석)
		* [주의사항](./7mobile.md#주의사항-3)
		* [코드](./7mobile.md#코드-4)
		* [태깅 예시](./7mobile.md#태깅-예시-4)
	* [화면별 페이지뷰 분석](./7mobile.md#화면별-페이지뷰-분석)
		* [코드](./7mobile.md#코드-5)
* [적용 후 데이터 검증](./7mobile.md#적용-후-데이터-검증)


# 공통 스크립트 삽입
이메일을 통해 전달받은 스크립트 파일을 사이트의 Footer에 삽입해야 합니다. 스크립트 파일의 확장자가 txt인 경우 js로 변경해서 적용하면 됩니다.
``` html
<!-- 사이트의 공통 영역에 Wisetracker script 삽입 -->
<script type="text/javascript" src=".../10197_Insight_WebAnalytics.js"></script>
</body>
</html>
```

## 분석 코드
데이터 분석용 코드와 태깅 방법을 안내합니다.

### 로그인 분석
로그인이 완료되는 시점(완료 페이지, 완료 이벤트, 완료 처리 등)에 아래 분석 코드를 설정합니다.

#### 주의사항
1) 로그인하는 사용자의 회원정보 중 성별, 연령, 요금제 정보를 참조해서 값을 입력해야 합니다.
2) `성별코드`, `연령대코드`에는 아래 표에 있는 코드 값을 넣어주시고, `현재요금제명칭`, `기존요금제명칭`에는 텍스트로 표현된 명칭 그대로를 입력해 주세요.

성별 | 성별코드
-------- | --------
여성 | F
남성 | M
기타 | U

연령대 | 연령대코드
-------- | --------
10세 미만 | A
10 - 19세 | B
20 - 29세 | C
30 - 39세 | D
40 - 49세 | E
50 - 59세 | F
60 - 69세 | G
70세 이상 | H

#### 코드
``` javascript
eval('try{_trk_flashEnvView(
\'_TRK_PI=LIR\',
\'_TRK_ISLOGIN=Y\',
\'_TRK_MBR=Y\',
\'_TRK_SX=성별코드\',
\'_TRK_AG=연령대코드\',
\'_TRK_UVP1=현재요금제명칭\',
\'_TRK_UVP2=기존요금제명칭\',
\'_TRK_G2=1\'
);}catch(_e){}');
```

#### 태깅 예시
30대 여성이며 기존에는 일반 요금제를 사용했으나 현재 플러스 요금제를 사용중인 유저가 로그인한 경우.
``` javascript
eval('try{_trk_flashEnvView(
\'_TRK_PI=LIR\',
\'_TRK_ISLOGIN=Y\',
\'_TRK_MBR=Y\',
\'_TRK_SX=F\',
\'_TRK_AG=D\',
\'_TRK_UVP1=플러스\',
\'_TRK_UVP2=일반\',
\'_TRK_G2=1\'
);}catch(_e){}');
```

40대 남성이며 아무런 요금제도 사용하지 않는 유저가 로그인한 경우.
``` javascript
eval('try{_trk_flashEnvView(
\'_TRK_PI=LIR\',
\'_TRK_ISLOGIN=Y\',
\'_TRK_MBR=Y\',
\'_TRK_SX=M\',
\'_TRK_AG=E\',
\'_TRK_UVP1=\',
\'_TRK_UVP2=\',
\'_TRK_G2=1\'
);}catch(_e){}');
```

### 회원가입 분석
회원가입 완료 화면에 아래 분석 코드를 설정합니다.

#### 코드
``` javascript
_TRK_PI = "RGR"; 
_TRK_G1 = "1";
```

#### 태깅 예시
``` html
<script type="text/javascript">
_TRK_PI = "RGR"; 
_TRK_G1 = "1";
</script>
```

### 상품 분석
개별 상품들의 상세 페이지에 아래 코드를 설정합니다.

#### 주의사항
'상품'에는 두가지가 있는 것으로 정의 했습니다. 단말기상품과 유심상품 입니다(즉, 요금제나 부가서비스 등은 상품으로 분석하지 않습니다). 상품에 포함되는 상세 페이지에만 아래 코드들을 적용해 주시기 바랍니다.

#### 코드
``` javascript
_TRK_PNC="상품코드";
_TRK_PNC_NM="상품명";
_TRK_PNG="범주코드"; //단말기 상품일 경우 000, 유심 상품일 경우 001 입력
_TRK_PNG_NM="범주명"; //단말기 상품일 경우 '단말기', 유심 상품일 경우 '유심' 입력
_TRK_PI="PDV";
```

#### 태깅 예시
유저가 유심 상세화면을 조회하는 경우 해당 화면에 아래 코드 태깅.
``` html
<script type="text/javascript">
_TRK_PNC="0000365614"; //back office 상의 실제 상품코드 입력
_TRK_PNC_NM="유심";
_TRK_PNG="001";
_TRK_PNG_NM="유심";
_TRK_PI="PDV";
</script>
```

유저가 갤럭시J4+ 상세화면을 조회하는 경우 해당 화면에 아래 코드 태깅.
``` html
<script type="text/javascript">
_TRK_PNC="0000454713"; //back office 상의 실제 상품코드 입력
_TRK_PNC_NM="갤럭시J4+";
_TRK_PNG="000";
_TRK_PNG_NM="단말기";
_TRK_PI="PDV";
</script>
```

### 요금제 변경 분석
단말기 상세 페이지의 'Step 2. 요금제 선택'에서, 유저가 요금제를 어떻게 변경하는지를 분석하기 위한 코드입니다.

#### 주의사항
1) '다른 요금제 선택' 버튼을 클릭하면 요금제 목록창이 나타납니다. 이 창에서 '선택' 버튼을 클릭하는 시점에 아래 코드를 태깅하면 됩니다.
!(http://www.wisetracker.co.kr/wp-content/uploads/2019/08/005.png)
2) 요금제 목록창에서 몇가지 요금들을 체크박스로 선택하여 '선택한 요금제 비교'로 넘어가는 경우도 있습니다. '선택한 요금제 비교'로 넘어간 화면에 있는 '선택' 버튼을 클릭하는 시점에도 아래 코드를 태깅해야 합니다.
!(http://www.wisetracker.co.kr/wp-content/uploads/2019/08/006.png)

#### 코드
``` javascript
eval('try{_trk_flashEnvView(
\'_TRK_MVT1=기존 요금제 명칭\',
\'_TRK_MVT2=새롭게 선택된 요금제 명칭\'
);}catch(_e){}');
```

#### 태깅 예시
유저가 'LTE온라인6GB' 요금제에서 'LTE 온라인 음성 S5' 요금 옆의 '선택' 버튼을 클릭해 요금제를 변경한 경우, 해당 클릭 이벤트에 아래 코드 태깅.
``` javascript
onclick="
	eval('try{_trk_flashEnvView(
	\'_TRK_MVT1=LTE온라인6GB\',
	\'_TRK_MVT2=LTE 온라인 음성 S5\'
	);}catch(_e){}');
"
```

### 구매 분석
단말기 & 유심 상품이 온라인 또는 전화로 신청 완료되는 경우를 분석하기 위한 코드입니다. 따라서 '온라인신청'이 완료되는 화면과 '전화신청'이 완료되는 화면에 분석 코드가 태깅되어야 합니다.

#### 주의사항
1) 단말기 구매 시 유심 상품도 함께 구매하도록 되어 있습니다. 이런 경우 분석 코드에도 두 상품의 정보가 모두 입력 되어야 합니다.
2) 온라인 신청 완료 화면, 그리고 전화 신청 완료 화면에 분석 코드를 태깅해 주시기 바랍니다.

#### 코드
``` javascript
_TRK_PNC = "상품코드";
_TRK_PNG = "범주코드";
_TRK_EA = "주문수량";
_TRK_AMT = "구매금액";
_TRK_ODNO = "주문번호";
_TRK_MVT3 = "신청방법"; //온라인 신청인 경우 '온라인'을, 전화 신청인 경우 '전화'를 입력
_TRK_PI = "ODR";
```

#### 태깅 예시
유저가 '전화신청'으로 '갤럭시J4+' 단말기와 'NFC 유심'을 신청한 경우 신청 완료 화면에 아래 코드 태깅.
``` html
<script type="text/javascript">
_TRK_PNC = "단말기상품코드;유심상품코드";
_TRK_PNG = "000;001";
_TRK_EA = "1;1";
_TRK_AMT = "단말기구매금액;유심구매금액";
_TRK_ODNO = "주문번호";
_TRK_MVT3 = "전화;전화";
_TRK_PI = "ODR";
</script>
```

유저가 '온라인신청'으로 '일반 유심'을 신청한 경우 신청 완료 화면에 아래 코드 태깅.
``` html
<script type="text/javascript">
_TRK_PNC = "유심상품코드";
_TRK_PNG = "001";
_TRK_EA = "1";
_TRK_AMT = "유심구매금액";
_TRK_ODNO = "주문번호";
_TRK_MVT3 = "온라인";
_TRK_PI = "ODR";
</script>
```

### 화면별 페이지뷰 분석
화면별 페이지뷰를 분석하기 위해서는 화면 식별용 API가 각 화면마다 태깅 되어야 합니다. 그리고 API에 각 화면에 대한 `화면코드`값을 입력해야 합니다. 화면정의 V0.9.3을 기준으로 아래 화면들에 대해 매핑된 `화면코드`를 사용해 주시기 바랍니다.

화면이름 | 화면코드 | 화면이미지
-------- | -------- | --------
로그인 | LIF | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image001.png)
회원가입 | RGF | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image003.png)
월정액상품 | SUBS | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image005.png)
VOD 결제하기 | ODF | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image007.png)
실시간TV | LIVE | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image009.png)
메인 | HOMEMAIN | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image011.png)
인기콘텐츠 | POPULAR | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image013.png)
상품기반 무료 (카테고리 - 나의 무료와 동일한 페이지) | FREE | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image015.png)
매거진 | MGZ | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image017.png)
5G특별관 (카테고리 - 5G 프리미엄과 동일한 페이지) | FIVEG | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image019.png)
오리지널 콘텐츠 | ORIGINAL | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image023.png)
리뷰의 신 | REVIEW | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image025.png)
음악채널(OST) | OST | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image027.png)
카테고리 Tab | CTGMAIN | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image029.png)
추천 카테고리 | RECOCTG | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image015.png)
전체 카테고리 | ALLCTG | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image035.png)
검색결과 | SCH | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image037.png)
콘텐츠 리스트(Scene 검색) | SCENESCH | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image039.png)
안면인식 감정 추론 기반 추천 콘텐츠 | EMOSCH | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image041.png)
마이페이지 | MYPAGE | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image043.png)
캐시 | CASH | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image045.png)
TV쿠폰 | TVCOUP | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image047.png)
콘텐츠 이용권 | VOUCHER | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image049.png)
무료체험권 | TRIAL | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image051.png)
마이스타일 리포트 | MYSTYLE | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image053.png)
구매내역(구매목록) | PAYLIST | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image055.png)
내가 찜한 콘텐츠 | WISHLIST | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image057.png)
좋아요 | LIKE | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image059.png)
다운로드 | DOWNLOAD | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image061.png)
시청내역 | WATCH | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image063.png)
성인 19+ | RATED | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image065.png)
올레TV 목록 | TVLIST | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image067.png)
이벤트 | EVENT | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image069.png)
공지 | NOTICE | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image071.png)
인물 상세정보 | FIGURE | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image073.png)
단편/시리즈/클립 | PDV | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image075.png)
패키지 메인 콘텐츠 | PACKAGE | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image077.png)

#### 분석 코드 - AOS
**[예시]** 사용자가 영상 상세의 단편/시리즈/클립 화면을 조회하는 경우, 해당 화면에 아래 코드 태깅
``` java
WiseTracker.setPageIdentity("PDV");
```

#### 분석 코드 - iOS Objective-C
**[예시]** 사용자가 회원가입에 필요한 정보를 입력하는 화면을 조회하는 경우, 해당 화면에 아래 코드 태깅
``` objc
[WiseTracker setPageIdentity:@"RGF"];
```

#### 분석 코드 - iOS Swift
**[예시]** 사용자가 마이 페이지 화면을 조회하는 경우, 해당 화면에 아래 코드 태깅
``` swift
WiseTracker.setPageIdentity("MYPAGE")
```

#### 분석 코드 - Hybrid
**[예시]** 사용자가 인물 상세정보 화면을 조회하는 경우, 해당 화면에 아래 코드 태깅
``` html
<script type="wisetracker/text" id="wiseTracker">
	WiseTracker.setPageIdentity("FIGURE");
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

![iOS Debug Mobe](http://www.wisetracker.co.kr/wp-content/uploads/2019/05/ios-debug.png)

``` swift
<key>WiseTrackerLogState</key>
<string>true</string>
```
