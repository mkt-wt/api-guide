# Premium 연동 API	
Wisetracker의 모든 고급기능을 사용할 수 있는 Premium Plan을 도입했다면 아래 Premium 연동 API를 적용하여 고급기능에 필요한 데이터들을 앱에서 수집할 수 있게 됩니다.	

## 1. 사용자 분석

### 1) 회원 가입

앱을 설치한 이후 회원 가입이 얼마나 많이 발생하는지 확인할 수 있게 됩니다. 이메일, 전화번호, 소셜 미디어 계정 등 다양한 수단으로 회원 가입이 가능한 경우, Goal API를 추가 사용해 각 수단별 회원 가입을 분석할 수 있습니다.

– 적용 위치: 회원 가입 완료 화면
#### a) Objective-c

```Objective-C	
[WiseTracker setGoal:@"g1" value: 1];
[WiseTracker sendGoalData];
```

#### b) Swift
```Swift
WiseTracker.setGoal("g1", 1 )
WiseTracker.sendGoalData()
```

#### c) WebView
```
<script type="wisetracker/text" id="wiseTracker">
  WiseTracker.setGoal("g1", 1);
  WiseTracker.sendGoalData();
</script>
```
### 2) 로그인 분석	
얼마나 많은 사용자들이 로그인을 하는지 확인할 수 있게 됩니다. 추가 API를 적용하면 로그인 하는 사용자의 인구통계 & 회원 속성 정보, 그리고 로그인 수단별 로그인 횟수를 분석할 수 있습니다.	

- 적용위치 : 로그인 완료화면	
– 주의사항: 자동 로그인, 소셜 로그인 등 모든 로그인 완료에 적용

### 1) Objective-C	
```Objective-C	
[WiseTracker setGoal:@"g2" value: 1];
[WiseTracker setGender:@"A"];
[WiseTracker setAge:@"C"];
[WiseTracker setUserAttribute:@"uvp1" name:@"B"];
[WiseTracker sendTransaction];	
```	

### 2) Swift	
```Swift	
WiseTracker.setGoal("g2", 1)
WiseTracker.setGender("A")
WiseTracker.setAge("C")
WiseTracker.setUserAttribute("uvp1", "B")
WiseTracker.sendTransaction()
```	

### 3) WebView	
```Java script	
<script type="wisetracker/text" id="wiseTracker">
  WiseTracker.setGoal("g2", 1);
  WiseTracker.setGender("A");
  WiseTracker.setAge("C");
  WiseTracker.setUserAttribute("uvp1", "B");
  WiseTracker.sendTransaction();
</script>
```	

## 2. 화면 분석	
화면별 페이지뷰를 분석하기 위해 사용자가 방문하는 주요 화면에 분석 코드를 삽입합니다.	

- 적용위치 : 분석 대상으로 지정한 주요 페이지	


### 1) Objective-C	
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
// "custom value"는 영문+숫자 조합의 8자리 이하의 문자열로 구성합니다.	
```	

### 2) Swift	
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

### 3) WebView	
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

## 3. 컨텐츠 분석	

### 1) 컨텐츠 경로 분석	
앱을 구성하는 다양한 컨텐츠를 계층구조로 정리해 분석하기 위해 코드를 삽입합니다.	

- 적용 위치: 컨텐츠를 계층구로조 분석할 필요가 있는 모든 화면	
WiseTracker.setContents("^1st depth value^2dn depth value") // value는 반드시 ^로 시작되어야 하며, 하위 뎁스를 구분할 경우에도 ^를 사용합니다

#### a) Objective-C	
```Objective-C	
 [WiseTracker setContents:@"^메인^의류^점퍼"];
```	

#### b) Swift	
```Swift	
	
 	
//적용예시	
 WiseTracker.setContents("^메인^의류^점퍼")	
 ```	

#### c) WebView	
```Java script	
 <script type="wisetracker/text" id="wiseTracker">
 WiseTracker.setContents("^메인^의류^점퍼");
 </script>	
```	

### 2) 상품 분석	
앱을 구성하는 다양한 상품 및 상품 카테고리 정보를 분석하기 위해 코드를 삽입합니다.

- 적용 위치: 상품 상세화면	

#### a) Objective-C	
```Objective-C	
 [WiseTracker setProduct:@"PROD01" name:@"나이키"];
 [WiseTracker setProductCategory:@"CAT01" name:@"^신발"];
 [WiseTracker setPageIdentity:@"PDV"];	
```	

#### b) Swift	
```Swift	
 WiseTracker.setProduct("PROD01", name: "나이키")
 WiseTracker.setProductCategory("CAT01", name: "^신발")
 WiseTracker.setPageIdentity("PDV")
```	

#### c) WebView	
```Java script	
 <script type="wisetracker/text" id="wiseTracker">
 WiseTracker.setProduct("PROD01", "나이키");
 WiseTracker.setProductCategory("CAT01", "^신발");
 WiseTracker.setPageIdentity("PDV");	
 </script>	
```	

### 3) 검색 키워드 분석	
#### a) Objective-C	
```Objective-C	
[WiseTracker setSearchKeyword:@"검색어"];	
[WiseTracker setSearchKeywordResult:@검색결과 수];	
//적용예시	
 [WiseTracker setSearchKeyword:@"가디건"];
 [WiseTracker setSearchKeywordResult:@1089];	
```	

#### b) Swift	
```Swift	
WiseTracker.setSearchKeyword("검색어")	
WiseTracker.setSearchKeywordResult(검색결과 수)	
//적용예시	
 WiseTracker.setSearchKeyword("가디건")	
 WiseTracker.setSearchKeywordResult(1089)	
```	

#### c) WebView	
```Java script	
WiseTracker.setSearchKeyword("검색어");	
WiseTracker.setSearchKeywordResult(검색결과 수);	
 	
//적용예시	
 <script type="wisetracker/text id="wiseTracker">
 WiseTracker.setSearchKeyword("가디건");	
 WiseTracker.setSearchKeywordResult(1089);
 </script>	
```	

## 4. 커머스 분석	
각 상품별 주문수와 매출액을 분석할 수 있도록 코드를 삽입합니다. 필수연동 API에서 몇가지 함수가 추가 되었습니다.	

- 적용 위치: 주문 완료화면	

### 1) Objective-C	
```Objective-C	
 [WiseTracker setOrderProductArray:@[@"PROD01",@"PROD02"]]; // 상품정보
 [WiseTracker setOrderProductCategoryArray:@[@"CAT01",@"CAT02"]]; // 상품카테고리
 [WiseTracker setOrderAmountArray:@[@10000, @20000]]; // 주문 상품 총액 (합계)
 [WiseTracker setOrderQuantityArray:@[@1, @2]]; // 주문 수량
 [WiseTracker setPageIdentity:@"ODR"]; // 주문페이지 PI세팅
 [WiseTracker sendTransaction]; // 데이터 전송
```	

### 2) Swift	
```Swift	
 WiseTracker.setOrderProductArray(["PROD01","PROD02"]) // 상품정보
 WiseTracker.setOrderProductCategoryArray(["CAT01","CAT02"]) // 상품카테고리
 WiseTracker.setOrderAmountArray([10000, 20000]) // 주문 상품 총액 (합계)
 WiseTracker.setOrderQuantityArray ([1, 2]) // 주문 수량
 WiseTracker.setPageIdentity("ODR") // 주문페이지 PI세팅
 WiseTracker.sendTransaction() // 데이터 전송
```	

### 3) WebView	
```Java script	
 <script type="wisetracker/text" id="wiseTracker">
 WiseTracker.setOrderProductArray(["PROD01","PROD02"]); // 상품정보
 WiseTracker.setOrderProductCategoryArray(["CAT01","CAT02"]); // 상품카테고리
 WiseTracker.setOrderAmountArray([10000, 20000]); // 주문 상품 총액 (합계)
 WiseTracker.setOrderQuantityArray ([1, 2]); // 주문
 WiseTracker.setPageIdentity("ODR"); // 주문페이지 PI세팅
 WiseTracker.sendTransaction(); // 데이터 전송
 </script>	
```	

