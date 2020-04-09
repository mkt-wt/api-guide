# Wisetracker Integration Guide
'더블유컨셉' 앱, 웹, 모바일웹에 와이즈트래커를 연동하는데 필요한 기술문서입니다. 연동 중 발생하는 문의사항은 아래 연락처로 보내 주시기 바랍니다.

> 와이즈트래커 개발팀, tech@wisetracker.co.kr, humblejohn@wisetracker.co.kr



# Index

* [클릭 분석 API](./wconcept.md#클릭-분석-API)
	* [적용 예시](./wconcept.md#적용-예시)
	* [매핑 테이블](./wconcept.md#매핑-테이블)



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

유저가 앱의 Top Seller 화면에서 1 depth 메뉴 중 'WOMEN' 을 클릭한 경우, 클릭이 발생한 시점에 아래 코드 추가.

``` javascript
WiseTracker.sendClickData("EVT", "[TOPSELLER_WOMEN]");
// name은 매핑 테이블 참고
```

앱의 Top Seller 화면의 1 depth 메뉴 중 'WOMEN' 이 선택되어 있는 상황에서 유저가 탑셀러 2 depth 메뉴의 'SHOES' 를 클릭한 경우, 클릭이 발생한 시점에 아래 코드 추가.

``` javascript
WiseTracker.sendClickData("EVT", "[TOPSELLER_W_SHO]");
// name은 매핑 테이블 참고
```



#### 매핑 테이블ㅜ
개별 객체에 대해 플랫폼기획팀이 정의한 명칭을 name 컬럼에 입력해 놓았습니다.

| 분류 | 대상 | 객체 | name | 참고 설명 |
| --- | --- | --- | --- | --- |
| PC | 탑셀러 1 depth 메뉴 | ALL 버튼 | [TOPSELLER_ALL] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/04/wck_topseller.png) |
| PC | 탑셀러 1 depth 메뉴 | WOMEN 버튼 | [TOPSELLER_WOMEN] |  |
| PC | 탑셀러 1 depth 메뉴 | MEN 버튼 | [TOPSELLER_MEN] |  |
| PC | 탑셀러 1 depth 메뉴 | LIFE 버튼 | [TOPSELLER_LIFE] |  |
| PC | 탑셀러 1 depth 메뉴 | BEAUTY 버튼 | [TOPSELLER_BEAUTY] |  |
| PC | 탑셀러 2 depth 메뉴 | ALL WOMEN 버튼 | [TOPSELLER_W_ALL] |  |
| PC | 탑셀러 2 depth 메뉴 | APPAREL 버튼 | [TOPSELLER_W_APP] | CSS의 `topseller_women` 클래스가 active 일때 나타나는 버튼 |
| PC | 탑셀러 2 depth 메뉴 | SHOES 버튼 | [TOPSELLER_W_SHO] | CSS의 `topseller_women` 클래스가 active 일때 나타나는 버튼 |
| PC | 탑셀러 2 depth 메뉴 | BAGS 버튼 | [TOPSELLER_W_BAG] |  |
| PC | 탑셀러 2 depth 메뉴 | ACCESSORIES 버튼 | [TOPSELLER_W_ACC] |  |
| PC | 탑셀러 2 depth 메뉴 | ALL MEN 버튼 | [TOPSELLER_ALL_M] |  |
| PC | 탑셀러 2 depth 메뉴 | APPAREL 버튼 | [TOPSELLER_M_APP] | CSS의 `topseller_men` 클래스가 active 일때 나타나는 버튼 |
| PC | 탑셀러 2 depth 메뉴 | SHOES 버튼 | [TOPSELLER_M_SHO] | CSS의 `topseller_men` 클래스가 active 일때 나타나는 버튼 |
| PC | 탑셀러 2 depth 메뉴 | BAG & ACC 버튼 | [TOPSELLER_M_BAG] |  |
| PC | 탑셀러 2 depth 메뉴 | ALL LIFE 버튼 | [TOPSELLER_ALL_L] |  |
| PC | 탑셀러 2 depth 메뉴 | HOME 버튼 | [TOPSELLER_L_HOM] |  |
| PC | 탑셀러 2 depth 메뉴 | LIFEWEAR 버튼 | [TOPSELLER_L_LIF] |  |
| PC | 탑셀러 2 depth 메뉴 | CULTURE&TRAVEL 버튼 | [TOPSELLER_L_CUL] |  |
| PC | 탑셀러 2 depth 메뉴 | TECH 버튼 | [TOPSELLER_L_TEC] |  |
| PC | 탑셀러 2 depth 메뉴 | ALL BEAUTY 버튼 | [TOPSELLER_ALL_B] |  |
| PC | 탑셀러 2 depth 메뉴 | FACIAL BEAUTY 버튼 | [TOPSELLER_B_FAC] |  |
| PC | 탑셀러 2 depth 메뉴 | SALON BEAUTY 버튼 | [TOPSELLER_B_SAL] |  |
| PC | 탑셀러 2 depth 메뉴 | SHAPE BEAUTY 버튼 | [TOPSELLER_B_SHA] |  |
| PC | 탑셀러 2 depth 메뉴 | SCENT BEAUTY 버튼 | [TOPSELLER_B_SCE] |  |
| PC | 탑셀러 2 depth 메뉴 | MEN 버튼 | [TOPSELLER_B_MEN] |  |
| PC | 탑셀러 하단 페이지네이션 | 1 버튼 | [PC_TOPSELLER_PAGE1] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/04/wck_topseller_bottom.png) |
| PC | 탑셀러 하단 페이지네이션 | 2 버튼 | [PC_TOPSELLER_PAGE2] |  |
| PC | 탑셀러 하단 페이지네이션 | 3 버튼 | [PC_TOPSELLER_PAGE3] |  |
| PC | 탑셀러 하단 페이지네이션 | 4 버튼 | [PC_TOPSELLER_PAGE4] |  |
| PC | 탑셀러 하단 페이지네이션 | 5 버튼 | [PC_TOPSELLER_PAGE5] |  |
| 모바일웹 & APP | 탑셀러 1 depth 메뉴 | ALL 버튼 | [M_TOPSELLER_ALL] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/04/wck_topseller.png) |
| 모바일웹 & APP | 탑셀러 1 depth 메뉴 | WOMEN 버튼 | [M_TOPSELLER_WOMEN] |  |
| 모바일웹 & APP | 탑셀러 1 depth 메뉴 | MEN 버튼 | [M_TOPSELLER_MEN] |  |
| 모바일웹 & APP | 탑셀러 1 depth 메뉴 | LIFE 버튼 | [M_TOPSELLER_LIFE] |  |
| 모바일웹 & APP | 탑셀러 1 depth 메뉴 | BEAUTY 버튼 | [M_TOPSELLER_BEAUTY] |  |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | ALL WOMEN 버튼 | [M_TOPSELLER_W_ALL] |  |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | APPAREL 버튼 | [M_TOPSELLER_W_APP] | CSS의 `topseller_women` 클래스가 active 일때 나타나는 버튼 |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | SHOES 버튼 | [M_TOPSELLER_W_SHO] | CSS의 `topseller_women` 클래스가 active 일때 나타나는 버튼 |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | BAGS 버튼 | [M_TOPSELLER_W_BAG] |  |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | ACCESSORIES 버튼 | [TOPSELLER_W_ACC] |  |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | ALL MEN 버튼 | [M_TOPSELLER_ALL_M] |  |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | APPAREL 버튼 | [M_TOPSELLER_M_APP] | CSS의 `topseller_men` 클래스가 active 일때 나타나는 버튼 |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | SHOES 버튼 | [M_TOPSELLER_M_SHO] | CSS의 `topseller_men` 클래스가 active 일때 나타나는 버튼 |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | BAG & ACC 버튼 | [M_TOPSELLER_M_BAG] |  |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | ALL LIFE 버튼 | [M_TOPSELLER_ALL_L] |  |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | HOME 버튼 | [M_TOPSELLER_L_HOM] |  |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | LIFEWEAR 버튼 | [M_TOPSELLER_L_LIF] |  |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | CULTURE&TRAVEL 버튼 | [M_TOPSELLER_L_CUL] |  |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | TECH 버튼 | [M_TOPSELLER_L_TEC] |  |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | ALL BEAUTY 버튼 | [M_TOPSELLER_ALL_B] |  |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | FACIAL BEAUTY 버튼 | [M_TOPSELLER_B_FAC] |  |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | SALON BEAUTY 버튼 | [M_TOPSELLER_B_SAL] |  |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | SHAPE BEAUTY 버튼 | [M_TOPSELLER_B_SHA] |  |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | SCENT BEAUTY 버튼 | [M_TOPSELLER_B_SCE] |  |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | MEN 버튼 | [M_TOPSELLER_B_MEN] |  |
| 모바일웹 & APP | 탑셀러 2 depth 메뉴 | GIFT SETS 버튼 | [M_TOPSELLER_B_GIF] |  |
| 모바일웹 & APP | 탑셀러 하단 페이지네이션 | 1 버튼 | [MO_TOPSELLER_PAGE1] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/04/wck_topseller_bottom.png) |
| 모바일웹 & APP | 탑셀러 하단 페이지네이션 | 2 버튼 | [MO_TOPSELLER_PAGE2] |  |
| 모바일웹 & APP | 탑셀러 하단 페이지네이션 | 3 버튼 | [MO_TOPSELLER_PAGE3] |  |
| 모바일웹 & APP | 탑셀러 하단 페이지네이션 | 4 버튼 | [MO_TOPSELLER_PAGE4] |  |
| 모바일웹 & APP | 탑셀러 하단 페이지네이션 | 5 버튼 | [MO_TOPSELLER_PAGE5] |  |
| 모바일웹 & APP | 메인 페이지 | 상품평 작성하러 가기 버튼 | [M_REVIEW] | [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/04/wck_main.png) |
| 모바일웹 & APP | 상품 리스트 페이지 | View Change 버튼 | [M_LIST_1] | CSS의 `btn_view_change` 클래스 속성이 `list1` 일때 나타나는 버튼, [참고 이미지](http://www.wisetracker.co.kr/wp-content/uploads/2020/04/wck_list.png) |
| 모바일웹 & APP | 상품 리스트 페이지 | View Change 버튼 | [M_LIST_2] | CSS의 `btn_view_change` 클래스 속성이 `list2` 일때 나타나는 버튼 |
| 모바일웹 & APP | 상품 리스트 페이지 | View Change 버튼 | [M_LIST_3] | CSS의 `btn_view_change` 클래스 속성이 `list0` 일때 나타나는 버튼 |

