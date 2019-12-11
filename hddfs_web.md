# Wisetracker Integration Guide
현대백화점면세점 중문 PC 웹사이트 & 모바일 웹사이트에는 와이즈트래커의 분석 코드들이 추가되어 있습니다. 보다 정확한 데이터 분석을 위해서 새로운 분석 코드를 추가하고, 기존에 추가된 일부 코드들을 수정하는 작업이 필요합니다. 본 문서에서는 새로운 코드 추가 & 기존 코드 수정 방법을 안내하고 있으며 반드시 PC 웹사이트와 모바일 웹사이트 모두 적용 되어야 합니다. 작업 중 발생하는 문의사항은 아래 담당자에게 연락 주시기 바랍니다.

> 정주온, humblejohn@wisetracker.co.kr

# Index
* [웹투앱 분석 코드 추가](./hddfs_web.md#웹투앱-분석-코드-추가)
* [기존 분석 코드 & 스크립트 위치 조정](./hddfs_web.md#기존-분석-코드--스크립트-위치-조정)
	* [주의사항](./hddfs_web.md#주의사항)
	* [적용 예시](./hddfs_web.md#적용-예시)
* [수정이 필요한 분석 코드](./hddfs_web.md#수정이-필요한-분석-코드)
	* [상품 분석용 코드 수정 사항](./hddfs_web.md#상품-분석용-코드-수정-사항)
	* [구매 분석용 코드 수정 사항](./hddfs_web.md#구매-분석용-코드-수정-사항)
* [적용 후 데이터 검증](./hddfs_web.md#적용-후-데이터-검증)


## 웹투앱 분석 코드 추가
웹사이트 방문 이후 앱을 설치하는 경우를 분석하기 위한 코드입니다. 현대백화점면세점 중문 PC 웹사이트, 중문 모바일 웹사이트의 `<head>`에 아래 코드를 적용해 주시기 바랍니다.

```html
<!DOCTYPE html>
<head>
...
<!-- 웹투앱 분석용 스크립트 include -->
<!-- 두 스크립트의 순서가 변하면 안됩니다 -->
<script src="//ads.wisetracker.co.kr/wa/js/wiseWebTrack.js"></script>      
<script src="//ads.wisetracker.co.kr/wa/js/customize/hddfs/wiseWebTrackInit.js"></script>
...
</head>
```

## 기존 분석 코드 & 스크립트 위치 조정
현재 사이트 상에는 와이즈트래커의 분석 코드와 공통 스크립트(라이브러리)가 `<body>` 영역에 추가되어 있습니다. 이 중 대부분의 코드를 `<head>` 영역으로 옮겨야 할 필요가 있습니다. 아래 주의사항과 설명을 참고하여 작업을 진행해 주시기 바랍니다.

### 주의사항
1) 와이즈트래커의 공통 스크립트(xxxxx_Insight_WebAnalytics.js)는 헤드가 끝나기 직전(`</head>`)에 위치 시킵니다.
2) 와이즈트래커의 환경 변수(_TRK 로 시작하는)는 반드시 공통 스크립트보다 위쪽에 위치 시킵니다.
3) 예외적으로 아래 표에 있는 분석 코드는 `<head>`로 옮기지 않고 현재 적용된 그대로 둡니다.


분석 항목 | 분석 코드
-------- | --------
회원 분석 | eval('try{_trk_flashEnvView(\'_TRK_PI=LIR\',\'_TRK_ISLOGIN=Y\',\'_TRK_MBR=Y\',\'_TRK_SX=성별코드\',\'_TRK_AG=연령대코드\',\'_TRK_UVP1=로그인유형코드\',\'_TRK_G2=1\');}catch(_e){}');
장바구니 담기 분석 | eval('try{_trk_flashEnvView(\'_TRK_PNC=상품코드\',\'_TRK_EA=상품수량\',\'_TRK_MVT1=브랜드명\',\'_TRK_G3=1\');}catch(_e){}');
관심상품 등록 분석 | eval('try{_trk_flashEnvView(\'_TRK_PNC=상품코드\',\'_TRK_MVT1=브랜드명\',\'_TRK_G4=1\');}catch(_e){}');
쿠폰 받기 분석 | eval('try{_trk_flashEnvView(\'_TRK_G5=1\');}catch(_e){}');
적립금 받기 분석 | eval('try{_trk_flashEnvView(\'_TRK_G6=1\');}catch(_e){}');


### 적용 예시
주문 완료 페이지에 위치한 기존 분석 코드를 모두 `<head>`로 이동
``` html
<!DOCTYPE html>
<head>
...
<!-- 앞에서 새로 추가한 wiseWebTrack 스크립트들 -->
<script src="//ads.wisetracker.co.kr/wa/js/wiseWebTrack.js"></script>      
<script src="//ads.wisetracker.co.kr/wa/js/customize/hddfs/wiseWebTrackInit.js"></script>
...
<!-- wisetracker 구매 분석용 코드 -->
<script type="text/javascript">
	_TRK_PNC = "상품코드;상품코드";
	_TRK_EA = "주문수량;주문수량";
	_TRK_AMT = "결제금액;결제금액";
	_TRK_ODNO = "주문번호";
	_TRK_MVT1 = "브랜드명;브랜드명";
	_TRK_PI = "ODR";
</script>
...
<!-- wisetracker 공통 스크립트 include -->
<script src="//cdn.hd-dfs.com/front/js/CN/tracking/10125_Insight_WebAnalytics_pc.js?ver=10"></script>
</head>
```

검색 완료 페이지에 위치한 기존 분석 코드를 모두 `<head>`로 이동
``` html
<!DOCTYPE html>
<head>
...
<!-- 앞에서 새로 추가한 wiseWebTrack 스크립트들 -->
<script src="//ads.wisetracker.co.kr/wa/js/wiseWebTrack.js"></script>      
<script src="//ads.wisetracker.co.kr/wa/js/customize/hddfs/wiseWebTrackInit.js"></script>
...
<!-- wisetracker 검색어 분석용 코드 -->
<script type="text/javascript">
	_TRK_IK = "검색어";
	_TRK_IKWDRS = "검색결과 수";
</script>
...
<!-- wisetracker 공통 스크립트 include -->
<script src="//cdn.hd-dfs.com/front/js/CN/tracking/10125_Insight_WebAnalytics_pc.js?ver=10"></script>
</head>
```

상품 상세 페이지에 위치한 기존 분석 코드를 모두 `<head>`로 이동
``` html
<!DOCTYPE html>
<head>
...
<!-- 앞에서 새로 추가한 wiseWebTrack 스크립트들 -->
<script src="//ads.wisetracker.co.kr/wa/js/wiseWebTrack.js"></script>      
<script src="//ads.wisetracker.co.kr/wa/js/customize/hddfs/wiseWebTrackInit.js"></script>
...
<!-- wisetracker 상품 분석용 코드 -->
<script type="text/javascript">
	_TRK_PNC = "상품코드"; 
	_TRK_PNC_NM = "상품명";
	_TRK_MVT1 = "브랜드명";
	_TRK_PI = "PDV";
</script>
...
<!-- wisetracker 공통 스크립트 include -->
<script src="//cdn.hd-dfs.com/front/js/CN/tracking/10125_Insight_WebAnalytics_pc.js?ver=10"></script>
</head>
```

### 수정이 필요한 분석 코드
위치 이동 외에도 다른 내용을 수정해야 할 코드들이 있습니다. 아래 항목들을 참고하여 수정해 주시기 바랍니다.

#### 상품 분석용 코드 수정 사항
1) 일반적인 상품과 구별되는 특수한 UI가 적용된 상품들은 상품 구매용 분석 코드 자체가 빠져 있습니다. 해당 UI를 사용하는 상품들에도 상품 분석용 코드가 적용되도록 수정해 주시기 바랍니다.

[예시 URL](https://cn.hddfs.com/shop/gd/dtl/goos.do?onlnGoosCd=10229250009701)

[예시 URL](https://cn.hddfs.com/shop/gd/dtl/goos.do?onlnGoosCd=10063280006501)

2) `상품명` value를 환경 변수에 넣을 때 인코딩되지 않은 스트링을 그대로 넣어 주시기 바랍니다. 상품명 중간에 있는 특수문자(&, 앰퍼샌드)가 HTML Entity로 인코딩된 값이 들어오면서 문제가 발생하고 있습니다.

[예시 URL](https://cn.hddfs.com/shop/gd/dtl/goos.do?onlnGoosCd=10474250003301)

``` javascript
// 와이즈트래커 상품 분석용 코드
// BO를 통해 생성되는 모든 상품에 적용되도록 수정 필요

_TRK_PNC = "상품코드";
_TRK_PNC_NM = "상품명"; //인코딩 되지 않은 string value를 사용하도록 수정 필요
_TRK_MVT1 = "브랜드명";
_TRK_PI = "PDV";
```

#### 구매 분석용 코드 수정 사항
유저가 구매한 상품 가격을 수집할때 기존에는 면세점이 책정한 상품의 판매가를 기준으로 하였으나, 유저가 해당 상품에 대해 실제 지불한 금액을 수집하도록 변경해야 합니다. 모든 할인이 적용되어 유저가 실제 결제하는 금액을 value로 넣어 주시기 바랍니다.

``` javascript
// 와이즈트래커 구매 분석용 코드

_TRK_PNC = "상품코드;상품코드";
_TRK_EA = "주문수량;주문수량";
_TRK_AMT = "결제금액;결제금액"; // 유저가 해당 상품에 대해 실제 지불해야 하는 금액으로 수정
_TRK_ODNO = "주문번호";
_TRK_MVT1 = "브랜드명;브랜드명";
_TRK_PI = "ODR";
```

## 적용 후 데이터 검증
위 사항을 적용해주신 이후 아래 담당자에게 연락 주시면 저희가 테스트 하여 결과 전달 드리겠습니다.

> 정주온, humblejohn@wisetracker.co.kr

> 배승민 과장, smbae@wisetracker.co.kr
