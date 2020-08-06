# Wisetracker Integration Guide
'더블유컨셉' 앱, 웹, 모바일웹에 와이즈트래커를 연동하는데 필요한 기술문서입니다. 연동 중 발생하는 문의사항은 아래 연락처로 보내 주시기 바랍니다.

> 와이즈트래커 개발팀, tech@wisetracker.co.kr, humblejohn@wisetracker.co.kr



# Index

* [클릭 분석 API](./wconcept-2.md#클릭-분석-API)
	* [적용 예시](./wconcept-2.md#적용-예시)
	* [매핑 테이블 - 20200802](./wconcept-2.md#매핑-테이블---20200802)
	
<!--
	* [매핑 테이블](./wconcept-2.md#매핑-테이블)
	* [매핑 테이블 - 20200714](./wconcept-2.md#매핑-테이블---2020714)
-->


## 클릭 분석 API

아래 매핑 테이블에 있는 버튼, 메뉴 등이 클릭되는 시점에 코드를 추가합니다.



**앱용 코드**

``` javascript
WiseTracker.sendClickData("EVT", "name");
// name은 매핑 테이블 참고
```

**PC & 모바일웹용 코드**

``` javascript
_trk_clickTrace(\"EVT\", \"name\");
// name은 매핑 테이블 참고
```



#### 적용 예시

유저가 앱의 메인 페이지 상단에 있는 검색버튼(돋보기)을 클릭하는 경우, 클릭이 발생한 시점에 아래 코드 추가.

``` javascript
WiseTracker.sendClickData("EVT", "[M_SEARCH]");
// name은 매핑 테이블 참고
```

유저가 PC 웹사이트의 메인 페이지 상단에 있는 검색버튼(돋보기)을 클릭하는 경우, 클릭이 발생한 시점에 아래 코드 추가.

``` javascript
_trk_clickTrace(\"EVT\", \"[SEARCH]\");
// name은 매핑 테이블 참고
```
<!--

#### 매핑 테이블

| 분류 | 대상 | 객체 | name | 참고 설명 |
| --- | --- | --- | --- | --- |
| PC | 메인 페이지 | 검색버튼(돋보기) | [SEARCH] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/05/wcon000.png) |
| PC | GNB -> NEW | 상품 배너 1번 | [GNB_NEW_BANNER1] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/05/wcon002.jpg) |
| PC | GNB -> NEW | 상품 배너 2번 | [GNB_NEW_BANNER2] | |
| PC | GNB -> NEW | 상품 배너 3번 | [GNB_NEW_BANNER3] | |
| PC | GNB -> NEW | 상품 배너 4번 | [GNB_NEW_BANNER4] | |
| PC | GNB -> BRAND | 브랜드 배너 1번 | [GNB_BRAND_BANNER1] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/05/wcon003.jpg) |
| PC | GNB -> BRAND | 브랜드 배너 2번 | [GNB_BRAND_BANNER2] | |
| PC | GNB -> BRAND | 브랜드 배너 3번 | [GNB_BRAND_BANNER3] | |
| 모바일웹 & APP | 메인 페이지 | 검색버튼(돋보기) | [M_SEARCH] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/05/wcon001.jpg) |
| 모바일웹 & APP | 검색 페이지 | 하단 배너 | [M_SEARCH_BANNER] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/05/wcon004.jpg) |
| 모바일웹 & APP | LNB | 하단 배너 | [M_LNB_BANNER] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/05/wcon005.jpg) |
| 하기 사항은 | 2020년 6월 12일에 | 추가하였습니다. |
| PC | 필터 메뉴 | 'FILTER+' 버튼 | [filter] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/06/wcon_pc.png) |
| PC | 필터 메뉴 | 'CATEGORY' 버튼 | [filter_category] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/06/wcon_pc.png) |
| PC | 필터 메뉴 | 'BRAND' 버튼 | [filter_brand] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/06/wcon_pc.png) |
| PC | 필터 메뉴 | 'PRICE' 버튼 | [filter_price] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/06/wcon_pc.png) |
| PC | 필터 메뉴 | 'BENEFIT' 버튼 | [filter_benefit] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/06/wcon_pc.png) |
| PC | 필터 메뉴 | 'COLOR' 버튼 | [filter_color] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/06/wcon_pc.png) |
| PC | 필터 메뉴 | 'DISCOUNT' 버튼 | [filter_discount] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/06/wcon_pc.png) |
| 모바일웹 & APP | 필터 메뉴 | 'FILTER' 버튼 | [M_filter] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/06/wcon_mo.png) |



#### 매핑 테이블 - 20200714

본 매핑 테이블은 2020년 7월 14일 요청 사항에 대응하는 내용만을 다루고 있습니다.


| 분류 | 대상 | 객체 | name | 참고 설명 |
| --- | --- | --- | --- | --- |
| 모바일웹 & APP | 메인 페이지 | 메뉴 버튼(햄버거) | [MENU] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/009.png) |
| 모바일웹 & APP | 메인 페이지 | 로고 | [LOGO] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/009.png) |
| 모바일웹 & APP | 메인 페이지 | 검색 버튼(돋보기) | [SR] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/009.png) |
| 모바일웹 & APP | 메인 페이지 | 장바구니 버튼 | [CART] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/009.png) |
| 모바일웹 & APP | 메인 페이지 | 액션바 홈버튼 | [A_HOME] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/009.png) |
| 모바일웹 & APP | 메인 페이지 | 액션바 히스토리 버튼 | [A_SR] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/009.png) |
| 모바일웹 & APP | 메인 페이지 | 액션바 하트 버튼 | [A_H] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/009.png) |
| 모바일웹 & APP | 메인 페이지 | 액션바 마이 버튼 | [A_MY] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/009.png) |
| 모바일웹 & APP | 메인 페이지 | 액션바 WOMEN 버튼 | [A_BT_W] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/009.png) |
| 모바일웹 & APP | LNB | LNB WOMEN | [L_W] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/010.png) |
| 모바일웹 & APP | LNB | LNB MEN | [L_M] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/010.png) |
| 모바일웹 & APP | LNB | LNB NEW | [L_NEW] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/010.png) |
| 모바일웹 & APP | LNB | LNB 배너 A | [L_BA_1] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/010.png) |
| 모바일웹 & APP | LNB | LNB 배너 B | [L_BA_1] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/07/010.png) |

-->

#### 매핑 테이블 - 20200802

본 매핑 테이블은 2020년 8월 2일 요청 사항에 대응하는 내용만을 다루고 있습니다.

| 분류 | 대상 | 객체 | name | 참고 설명 |
| --- | --- | --- | --- | --- |
| 모바일웹 & APP | Women 메인 > What's New | TODAY MORE | [W_NEW] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/08/004.png) |
| 모바일웹 & APP | Women 메인 > What's New | APPAREL | [W_NEW_APP] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/08/004.png) |
| 모바일웹 & APP | Women 메인 > What's New | BAG | [W_NEW_BAG] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/22020/08/004.png) |
| 모바일웹 & APP | Women 메인 > What's New | SHOES | [W_NEW_SH] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/08/004.png) |
| 모바일웹 & APP | Women 메인 > What's New | ACC | [W_NEW_ACC] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/08/004.png) |
| 모바일웹 & APP | Women 메인 > What's New | BEAUTY& | [W_NEW_B] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/08/004.png) |
| 모바일웹 & APP | Women 메인 > What's New | LIFEWEAR | [W_NEW_LW] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/08/004.png) |
| 모바일웹 & APP | Women 메인 > What's New | LIFE | [W_NEW_L] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/08/004.png) |
| 모바일웹 & APP | Men 메인 > What's New | TODAY MORE | [M_NEW] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/08/005.png) |
| 모바일웹 & APP | Men 메인 > What's New | APPAREL | [M_NEW_APP] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/08/005.png) |
| 모바일웹 & APP | Men 메인 > What's New | BAG | [M_NEW_BAG] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/08/005.png) |
| 모바일웹 & APP | Men 메인 > What's New | SHOES | [M_NEW_SH] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/08/005.png) |
| 모바일웹 & APP | Men 메인 > What's New | ACC | [M_NEW_ACC] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/08/005.png) |
| 모바일웹 & APP | Men 메인 > What's New | BEAUTY& | [M_NEW_B] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/08/005.png) |
| 모바일웹 & APP | Men 메인 > What's New | LIFEWEAR | [M_NEW_LW] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/08/005.png) |
| 모바일웹 & APP | Men 메인 > What's New | LIFE | [M_NEW_L] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/08/005.png) |
