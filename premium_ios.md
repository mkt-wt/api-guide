## <a id="WISETRACKER_PREMIUM"></a> Premium 연동 API	
Wisetracker의 모든 고급기능을 사용할 수 있는 Premium Plan을 도입했다면 아래 Premium 연동 API를 적용하여 고급기능에 필요한 데이터들을 앱에서 수집할 수 있게 됩니다.	

### 1. 사용자 분석	
사용자의 성별, 연령대, 회원등급 등을 분석하기 위해 해당 정보를 수집하는 코드를 삽입합니다.	

- 적용위치 : 회원가입 완료화면 및 로그인 완료화면	

#### 1) Objective-C	
```Objective-C	
남성 : [WiseTracker setGender:[WiseTrackerGENDER_MALE]];	
여성 : [WiseTracker setGender:[WiseTrackerGENDER_FEMALE]];	
기타 : [WiseTracker setGender:[WiseTrackerGENDER_ETC]];	
10대 이하 : [WiseTracker setAge:[WiseTrackerAGE_0_TO_9]];	
10대 : [WiseTracker setAge:[WiseTrackerAGE_10_TO_19]];	
20대 : [WiseTracker setAge:[WiseTrackerAGE_20_TO_29]];	
30대 : [WiseTracker setAge:[WiseTrackerAGE_30_TO_39]];	
40대 : [WiseTracker setAge:[WiseTrackerAGE_40_TO_49]];	
50대 : [WiseTracker setAge:[WiseTrackerAGE_50_TO_59]];	
60대이상 : [WiseTracker setAge:[WiseTrackerAGE_60_OVER]];	
회원속성 : [WiseTracker setUserAttribute:[WiseTrackerUSER_ATTRIBUTE_1,"custom value"];	
 * USER_ATTRIBUTE는 회원의 다양한 속성(회원등급, 직업, 외국인 여부 등)을 분류할 필요가 있을때 사용합니다.	
//적용예시	
 [WiseTracker setGender:[WiseTrackerGENDER_MALE]]; // 성별 	
 [WiseTracker setAge:[WiseTrackerAGE_20_TO_29]]; // 연령	
 [WiseTracker setUserAttribute:[WiseTrackerUSER_ATTRIBUTE_1,"VIP"]]; // 회원 분류	
```	

#### 2) Swift	
```Swift	
남성 : WiseTracker.setGender(WiseTracker.GENDER_MALE())	
여성 : WiseTracker.setGender(WiseTracker.GENDER_FEMALE())	
기타 : WiseTracker.setGender(WiseTracker.GENDER_ETC())	
10대 이하 : WiseTracker.setAge(WiseTracker.AGE_0_TO_9())	
10대 : WiseTracker.setAge(WiseTracker.AGE_10_TO_19())	
20대 : WiseTracker.setAge(WiseTracker.AGE_20_TO_29())	
30대 : WiseTracker.setAge(WiseTracker.AGE_30_TO_39())	
40대 : WiseTracker.setAge(WiseTracker.AGE_40_TO_49())	
50대 : WiseTracker.setAge(WiseTracker.AGE_50_TO_59())	
60대이상 : WiseTracker.setAge(WiseTracker.AGE_60_OVER())	
회원속성 : WiseTracker.setUserAttribute(WiseTracker.USER_ATTRIBUTE_1,"custom value"())	
 * USER_ATTRIBUTE는 회원의 다양한 속성(회원등급, 직업, 외국인 여부 등)을 분류할 필요가 있을때 사용합니다.	
//적용예시	
 WiseTracker.setGender(WiseTracker.GENDER_MALE()) // 성별 	
 WiseTracker.setAge(WiseTracker.AGE_20_TO_29()) // 연령	
 WiseTracker.setUserAttribute(WiseTracker.USER_ATTRIBUTE_1,"VIP"()) // 회원 분류	
```	

#### 3) WebView	
```Java script	
남성 : WiseTracker.setGender(WiseTracker.GENDER_MALE);	
여성 : WiseTracker.setGender(WiseTracker.GENDER_FEMALE);	
기타 : WiseTracker.setGender(WiseTracker.GENDER_ETC);	
10대 이하 : WiseTracker.setAge(WiseTracker.AGE_0_TO_9);	
10대 : WiseTracker.setAge(WiseTracker.AGE_10_TO_19);	
20대 : WiseTracker.setAge(WiseTracker.AGE_20_TO_29);	
30대 : WiseTracker.setAge(WiseTracker.AGE_30_TO_39);	
40대 : WiseTracker.setAge(WiseTracker.AGE_40_TO_49);	
50대 : WiseTracker.setAge(WiseTracker.AGE_50_TO_59);	
60대이상 : WiseTracker.setAge(WiseTracker.AGE_60_OVER);	
회원속성 : WiseTracker.setUserAttribute(WiseTracker.USER_ATTRIBUTE_1,"custom value");	
 * USER_ATTRIBUTE는 회원의 다양한 속성(회원등급, 직업, 외국인 여부 등)을 분류할 필요가 있을때 사용합니다.	
//적용예시	
 <script type="wisetracker/text" id="wiseTracker">	
 WiseTracker.setGender(WiseTracker.GENDER_MALE); // 성별 	
 WiseTracker.setAge(WiseTracker.AGE_20_TO_29); // 연령	
 WiseTracker.setUserAttribute(WiseTracker.USER_ATTRIBUTE_1,"VIP"); // 회원 분류 	
 </script>	
```	

### 2. 화면 분석	
화면별 페이지뷰를 분석하기 위해 사용자가 방문하는 주요 화면에 분석 코드를 삽입합니다.	

- 적용위치 : 분석 대상으로 지정한 주요 페이지	


#### 1) Objective-C	
```Objective-C	
로그인 입력 화면 : [WiseTracker setPageIdentity:@"LIF"];	
로그인 완료 화면 : [WiseTracker setPageIdentity:@"LIR"];	
회원가입 신청 화면 : [WiseTracker setPageIdentity:@"RGI"];	
회원가입 입력 화면 : [WiseTracker setPageIdentity:@"RGF"];	
회원가입 완료 화면 : [WiseTracker setPageIdentity:@"RGR"];	
상품 리스트 화면 : [WiseTracker setPageIdentity:@"PLV"];	
상품 상세 화면 : [WiseTracker setPageIdentity:@"PDV"];	
장바구니 화면 : [WiseTracker setPageIdentity:@"OCV"];	
주문정보 입력 화면 : [WiseTracker setPageIdentity:@"ODF"];	
주문 완료 화면 : [WiseTracker setPageIdentity:@"ODR"];	
 	
사용자 정의 화면 : [WiseTrackersetPageIdentity:@"custom value"];	
// 사전 정의된 화면 이외의 화면을 분석하고자 할때 사용자 정의 화면코드를 활용할 수 있습니다.	
// "custom value"에 임의의 값을 넣어 원하는 화면에 코드를 삽입하면 되며	
// "custom value"는 영문+숫자 조합의 6byte 이하의 문자열로 구성합니다.	
```	

#### 2) Swift	
```Swift	
로그인 입력 화면 : WiseTracker.setPageIdentity("LIF")	
로그인 완료 화면 : WiseTracker.setPageIdentity("LIR")	
회원가입 신청 화면 : WiseTracker.setPageIdentity("RGI")	
회원가입 입력 화면 : WiseTracker.setPageIdentity("RGF")	
회원가입 완료 화면 : WiseTracker.setPageIdentity("RGR")	
상품 리스트 화면 : WiseTracker.setPageIdentity("PLV")	
상품 상세 화면 : WiseTracker.setPageIdentity("PDV")	
장바구니 화면 : WiseTracker.setPageIdentity("OCV")	
주문정보 입력 화면 : WiseTracker.setPageIdentity("ODF")	
주문 완료 화면 : WiseTracker.setPageIdentity("ODR")	
 	
사용자 정의 화면 : WiseTracker.setPageIdentity("custom value")	
```	

#### 3) WebView	
```Java script	
로그인 입력 화면 : WiseTracker.setPageIdentity("LIF");	
로그인 완료 화면 : WiseTracker.setPageIdentity("LIR");	
회원가입 신청 화면 : WiseTracker.setPageIdentity("RGI");	
회원가입 입력 화면 : WiseTracker.setPageIdentity("RGF");	
회원가입 완료 화면 : WiseTracker.setPageIdentity("RGR");	
상품 리스트 화면 : WiseTracker.setPageIdentity("PLV");	
상품 상세 화면 : WiseTracker.setPageIdentity("PDV");	
장바구니 화면 : WiseTracker.setPageIdentity("OCV");	
주문정보 입력 화면 : WiseTracker.setPageIdentity("ODF");	
주문 완료 화면 : WiseTracker.setPageIdentity("ODR");	
 	
사용자 정의 화면 : WiseTracker.setPageIdentity("custom value");	
```	

### 3. 컨텐츠 분석	
#### 1) 컨텐츠 경로 분석	
앱을 구성하는 다양한 컨텐츠를 계층구조로 정리해 분석하기 위해 코드를 삽입합니다.	

- 적용 위치: 컨텐츠를 계층구로조 분석할 필요가 있는 모든 화면	

##### a) Objective-C	
```Objective-C	
[WiseTracker setContents:@"^1st depth value^2dn depth value"]; // value는 반드시 ^로 시작되어야 하며, 하위 뎁스를 구분할 경우에도 ^를 사용합니다	
//적용예시	
 [WiseTracker setContents:@"^메인^의류^점퍼"];	
```	

##### b) Swift	
```Swift	
WiseTracker.setContents("^1st depth value^2dn depth value") // value는 반드시 ^로 시작되어야 하며, 하위 뎁스를 구분할 경우에도 ^를 사용합니다	
 	
//적용예시	
 WiseTracker.setContents("^메인^의류^점퍼")	
 ```	

##### c) WebView	
```Java script	
WiseTracker.setContents("^1st depth value^2dn depth value"); // value는 반드시 ^로 시작되어야 하며, 하위 뎁스를 구분할 경우에도 ^를 사용합니다	
//적용예시	
 <script type="wisetracker/text" id="wiseTracker">	
 WiseTracker.setContents("^메인^의류^점퍼");	
 </script>	
```	

#### 2) 상품 분석	
앱을 구성하는 다양한 상품 및 상품 카테고리 정보를 분석하기 위해 코드를 삽입합니다.	

- 적용 위치: 상품 상세화면	

##### a) Objective-C	
```Objective-C	
상품 : [WiseTracker setProduct:@"상품코드" name:@"상품명"];	
상품 카테고리 : [WiseTracker setProductCategory:@"상품 카테고리 코드" name:@"^상품 카테고리명"];	
상품 상세화면 : [WiseTracker setPageIdentity:@"PDV"];	
//적용예시	
 [WiseTracker setProduct:@"PROD01" name:@"나이키"];	
 [WiseTracker setProductCategory:@"CAT01" name:@"^신발"];	
 [WiseTracker setPageIdentity:@"PDV"];	
```	

##### b) Swift	
```Swift	
상품 : WiseTracker.setProduct("상품코드", "상품명")	
상품 카테고리 : WiseTracker.setProductCategory("상품 카테고리 코드", "^상품 카테고리명")	
상품 상세화면 : WiseTracker.setPageIdentity("PDV")	
//적용예시	
 WiseTracker.setProduct("PROD01", "나이키")	
 WiseTracker.setProductCategory("CAT01", "^신발")	
 WiseTracker.setPageIdentity("PDV")	
```	

##### c) WebView	
```Java script	
상품 : WiseTracker.setProduct("상품코드", "상품명");	
상품 카테고리 : WiseTracker.setProductCategory("상품 카테고리 코드", "^상품 카테고리명");	
상품 상세화면 : WiseTracker.setPageIdentity("PDV");	
//적용예시	
 <script type="wisetracker/text" id="wiseTracker">	
 WiseTracker.setProduct("PROD01", "나이키");	
 WiseTracker.setProductCategory("CAT01", "^신발");	
 WiseTracker.setPageIdentity("PDV");	
 </script>	
```	

#### 3) 검색 키워드 분석	
##### a) Objective-C	
```Objective-C	
[WiseTracker setSearchKeyword:@"검색어"];	
[WiseTracker setSearchKeywordResult:@검색결과 수];	
//적용예시	
 [WiseTracker setSearchKeyword:@"가디건"];	
 [WiseTracker setSearchKeywordResult:@1089];	
```	

##### b) Swift	
```Swift	
WiseTracker.setSearchKeyword("검색어")	
WiseTracker.setSearchKeywordResult(검색결과 수)	
//적용예시	
 WiseTracker.setSearchKeyword("가디건")	
 WiseTracker.setSearchKeywordResult(1089)	
```	

##### c) WebView	
```Java script	
WiseTracker.setSearchKeyword("검색어");	
WiseTracker.setSearchKeywordResult(검색결과 수);	
 	
//적용예시	
 <script type="wisetracker/text id="wiseTracker">	
 WiseTracker.setSearchKeyword("가디건");	
 WiseTracker.setSearchKeywordResult(1089);	
 </script>	
```	

### 4. 커머스 분석	
각 상품별 주문수와 매출액을 분석할 수 있도록 코드를 삽입합니다. 필수연동 API에서 몇가지 함수가 추가 되었습니다.	

- 적용 위치: 주문 완료화면	

#### 1) Objective-C	
```Objective-C	
상품 : [WiseTracker setOrderProductArray:@[@"상품코드1", @"상품코드2"]];	
상품 카테고리 : [WiseTracker setOrderProductCategoryArray:@[@"상품 카테고리 코드1", @"상품 카테고리 코드2"]];	
상품 구매금액 : [WiseTracker setOrderAmountArray:@[@A상품 구매 금액, @B상품 구매 금액]];	
상품 주문수량 : [WiseTracker setOrderQuantityArray:@[@A상품 주문수량, @B상품 주문수량]];	
주문이 발생한 페이지 : [WiseTracker setPageIdentity:@"ODR"];	
 	
//적용예시	
 [WiseTracker setOrderProductArray:@[@"PROD01",@"PROD02"]]; // 상품정보	
 [WiseTracker setOrderProductCategoryArray:@[@"CAT01",@"CAT02"]]; // 상품카테고리	
 [WiseTracker setOrderAmountArray:@[@10000, @20000]]; // 주문 상품 총액 (합계)	
 [WiseTracker setOrderQuantityArray:@[@1, @2]]; // 주문	
```	

#### 2) Swift	
```Swift	
상품 : WiseTracker.setOrderProductArray(["상품코드1", "상품코드2"])	
상품 카테고리 : WiseTracker.setOrderProductCategoryArray(["상품 카테고리 코드1", "상품 카테고리 코드2"])	
상품 구매금액 : WiseTracker.setOrderAmountArray([A상품 구매 금액, B상품 구매 금액])	
상품 주문수량 : WiseTracker.setOrderQuantityArray([A상품 주문수량, B상품 주문수량])	
주문이 발생한 페이지 : WiseTracker.setPageIdentity("ODR")	
 	
//적용예시	
 WiseTracker.setOrderProductArray(["PROD01","PROD02"]) // 상품정보	
 WiseTracker.setOrderProductCategoryArray(["CAT01","CAT02"]) // 상품카테고리	
 WiseTracker.setOrderAmountArray([10000, 20000]) // 주문 상품 총액 (합계)	
 WiseTracker.setOrderQuantityArray ([1, 2]) // 주문	
 WiseTracker.setPageIdentity("ODR") // 주문완료	
```	

#### 3) WebView	
```Java script	
상품 : WiseTracker.setOrderProductArray({"상품코드1", "상품코드2"});	
상품 카테고리 : WiseTracker.setOrderProductCategoryArray({"상품 카테고리 코드1", "상품 카테고리 코드2"});	
상품 구매금액 : WiseTracker.setOrderAmountArray({A상품 구매 금액, B상품 구매 금액});	
상품 주문수량 : WiseTracker.setOrderQuantityArray({A상품 주문수량, B상품 주문수량});	
주문이 발생한 페이지 : WiseTracker.setPageIdentity("ODR");	
 	
//적용예시	
 <script type="wisetracker/text" id="wiseTracker">	
 WiseTracker.setOrderProductArray({"PROD01","PROD02"}); // 상품정보	
 WiseTracker.setOrderProductCategoryArray({"CAT01","CAT02"}); // 상품카테고리	
 WiseTracker.setOrderAmountArray({10000, 20000}); // 주문 상품 총액 (합계)	
 WiseTracker.setOrderQuantityArray ({1, 2}); // 주문	
 WiseTracker.setPageIdentity("ODR"); // 주문완료	
 </script>	
```	

### 5. Custom Goals 분석	
각 고객사마다 비즈니스 환경과 분석 대상이 다릅니다. 상품구매 외에 가입, 상담 문의 등도 전환으로 지정해 성과 값을 수집할 필요가 있습니다. 이런 Custom 전환성과를 분석하기 위해 코드를 삽입합니다.	

- 적용 위치 : 전환 완료 화면	

#### 1) Objective-C	
```Objective-C	
[WiseTrackersetGoal:[WiseTrackerGOAL_1]  value: 1];	
// WiseTracker.GOAL_1~10까지 사용 가능하며, 전환 완료 화면이 존재하지 않는 경우 버튼에 적용해 측정할 수도 있습니다.	
// ex) 장바구니 담기 버튼, SNS 공유 버튼 등	
```	

#### 2) Swift	
```Swift	
WiseTracker.setGoal(WiseTracker.GOAL_1(), value: 1)	
```	

#### 3) WebView	
```Java script	
WiseTracker.setGoal(WiseTracker.GOAL_1, 1);	
```	
