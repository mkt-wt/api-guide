# Wisetracker Integration Guide
'SK 7mobile' 사이트에 와이즈트래커 분석코드를 삽입하는데 필요한 기술문서입니다. 작업 중 발생하는 문의사항은 아래 담당자에게 연락 주시기 바랍니다.

> 정주온, humblejohn@wisetracker.co.kr

# Table of Contents
* [분석 범위](./7mobile.md#분석-범위)
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
	* [구매 후기 등록횟수 분석](./7mobile.md#구매-후기-등록횟수-분석)
		* [주의사항](./7mobile.md#주의사항-4)
		* [코드](./7mobile.md#코드-5)
	* [화면별 페이지뷰 분석](./7mobile.md#화면별-페이지뷰-분석)
		* [코드](./7mobile.md#코드-6)
		* [태깅 예시](./7mobile.md#태깅-예시-5)
* [적용 후 데이터 검증](./7mobile.md#적용-후-데이터-검증)

# 분석 범위
안내된 코드를 추가함으로써 최종적으로 다음 사항들을 데이터로 확인할 수 있게 됩니다.

- 외부 광고 & 제휴 채널을 통한 유입, 상품 구매 성과
	- 광고 채널/캠페인
	- 키워드 광고 / 배너광고
	- 유입 검색어
- 상품 구매 성과
	- 상품: 유심, 단말기를 의미
	- 신청 유형: 온라인 또는 전화
	- 가입 유형: 신규, 기변, 번호이동
	- 요금제 종류
	- 요금 할인 유형: 공시지원금, 선택약정
	- 유심 종류: 일반, NFC
	- 각 상품별 구매 횟수, 구매 금액
- 고객
	- 성별
	- 연령대
	- 로그인 & 회원가입 횟수
	- 방문유형: 처음 / 재방문 / 반복방문
	- 방문 횟수분포
	- 방문 간격분포
- 이벤트: 이벤트 상세 화면의 PV, 광고 랜딩을 통한 이벤트 PV, 랜딩 이후 이동경로 분석
- 퍼널: 각 화면간의 이동 횟수를 기반으로 한 시나리오 분석
- Goals
	- 후기 등록 횟수
	- 요금제 변경 (추천 요금제 to 사용자 선택 요금제)
- 세그먼트: 전체 데이터에서 아래 조건들에 해당하는 데이터만 구분해서 볼 수 있음
	- 광고 채널
	- 광고 캠페인
	- 방문유형
	- 성별
	- 연령대


## 공통 스크립트 삽입
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
_TRK_PNC = "상품코드";
_TRK_PNC_NM = "상품명";
_TRK_PNG = "범주코드"; //단말기 상품일 경우 000, 유심 상품일 경우 001 입력
_TRK_PNG_NM = "범주명"; //단말기 상품일 경우 '단말기', 유심 상품일 경우 '유심' 입력
_TRK_PI = "PDV";
```

#### 태깅 예시
유저가 유심 상세화면을 조회하는 경우 해당 화면에 아래 코드 태깅.
``` html
<script type="text/javascript">
_TRK_PNC = "0000365614"; //back office 상의 실제 상품코드 입력
_TRK_PNC_NM = "유심";
_TRK_PNG = "001";
_TRK_PNG_NM = "유심";
_TRK_PI = "PDV";
</script>
```

유저가 갤럭시J4+ 상세화면을 조회하는 경우 해당 화면에 아래 코드 태깅.
``` html
<script type="text/javascript">
_TRK_PNC = "0000454713"; //back office 상의 실제 상품코드 입력
_TRK_PNC_NM = "갤럭시J4+";
_TRK_PNG = "000";
_TRK_PNG_NM = "단말기";
_TRK_PI = "PDV";
</script>
```

### 추천 요금제 변경 분석
각 단말기마다 기본값으로 세팅된 추천 요금제가 있습니다. 이것을 어떤 요금제로 변경하는지 분석하기 위한 코드입니다.

#### 주의사항
1) '추천 요금제'란 각 단말기마다 기본값으로 세팅되어 있는 요금제를 말합니다. (예를들어 현 시점에 LG Q7(salePlcyCd=0000347351)에 기본 세팅된 요금제는 'LTE 온라인 음성 S3' 입니다.)
1) '다른 요금제 선택' 버튼을 클릭하면 요금제 목록창이 나타납니다. 이 창에서 '선택' 버튼을 클릭하는 시점에 아래 코드를 태깅하면 됩니다.
![button](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/005.png)
2) 요금제 목록창에서 몇가지 요금들을 체크박스로 선택하여 '선택한 요금제 비교'로 넘어가는 경우도 있습니다. '선택한 요금제 비교'로 넘어간 화면에 있는 '선택' 버튼을 클릭하는 시점에도 아래 코드를 태깅해야 합니다.
![button](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/006.png)

#### 코드
``` javascript
eval('try{_trk_flashEnvView(
\'_TRK_MVT1=추천 요금제 명칭\',
\'_TRK_MVT2=선택된 요금제 명칭\'
);}catch(_e){}');
```

#### 태깅 예시
유저가 추천 요금제인 'LTE온라인6GB'를 'LTE 온라인 음성 S5' 요금으로 바꾸기 위해 '선택' 버튼을 클릭한 경우, 해당 클릭 이벤트에 아래 코드 태깅.
``` javascript
onclick="
	eval('try{_trk_flashEnvView(
	\'_TRK_MVT1=LTE온라인6GB\',
	\'_TRK_MVT2=LTE 온라인 음성 S5\'
	);}catch(_e){}');
"
```

유저가 추천 요금제인 'LTE온라인6GB'를 바꾸려다가 다시 'LTE온라인6GB' 요금의 '선택' 버튼을 클릭한 경우, 해당 클릭 이벤트에 아래 코드 태깅.
``` javascript
onclick="
	eval('try{_trk_flashEnvView(
	\'_TRK_MVT1=LTE온라인6GB\',
	\'_TRK_MVT2=LTE온라인6GB\'
	);}catch(_e){}');
"
```

### 구매 분석
단말기 & 유심 상품이 온라인 또는 전화로 신청 완료되는 경우를 분석하기 위한 코드입니다. 따라서 '온라인신청'이 완료되는 화면과 '전화신청'이 완료되는 화면에 분석 코드가 태깅되어야 합니다.

#### 주의사항
1) 단말기 구매 시 유심 상품도 함께 구매하게 되어 있습니다. 결국 1번의 구매에 '단말기 상품', '유심 상품' 총 2개의 상품이 포함될 수 있습니다.
2) 위와 같이 한번의 구매에 복수의 상품이 포함된 경우, 환경변수의 값에 세미콜론 기호(;)를 사용해 다수의 정보를 구분해서 넣어야 합니다. 아래 예시를 참고해 주세요. 
3) 온라인 신청 완료 화면, 그리고 전화 신청 완료 화면에 분석 코드를 태깅해 주시기 바랍니다.

#### 코드
``` javascript
_TRK_PNC = "상품코드";
_TRK_PNC_SUB_TP = "신청유형"; //온라인 신청이면 '온라인'을, 전화 신청이면 '전화'를 입력
_TRK_PNC_ATRC_1 = "가입유형코드";
_TRK_PNC_ATRN_1 = "가입유형"; //번호이동, 신규, 기기변경
_TRK_PNC_ATRC_2 = "할인방법코드";
_TRK_PNC_ATRN_2 = "할인방법"; //공시지원금, 선택약정만 해당됨. 제휴카드할인은 제외.
_TRK_PNC_ATRC_3 = "유심형태코드";
_TRK_PNC_ATRN_3 = "유심명칭";
_TRK_PNC_ATRC_4 = "요금제코드";
_TRK_PNC_ATRN_4 = "요금제명칭";
_TRK_PNG = "범주코드";
_TRK_EA = "주문수량";
_TRK_AMT = "구매금액"; //유저가 실제 지불하는 금액 입력
_TRK_ODNO = "주문번호"; //해당 주문건의 유니크한 주문번호 입력
_TRK_PI = "ODR";
```

#### 태깅 예시
유저가 '번호이동'으로 '갤럭시J4+' 단말기, 'LTE 온라인 음성 S5' 요금제, 'NFC 유심'을 구매하면서 '공시지원금'을 선택해 '전화'로 신청한 경우 신청 완료 화면에 아래 코드 태깅.
``` html
<script type="text/javascript">
_TRK_PNC = "단말기상품코드;유심상품코드"; //세미콜론(;)으로 값을 구분하여 입력
_TRK_PNC_SUB_TP = "전화;전화";
_TRK_PNC_ATRC_1 = "가입유형코드;가입유형코드"; //번호이동을 의미하는 코드값
_TRK_PNC_ATRN_1 = "번호이동;번호이동";
_TRK_PNC_ATRC_2 = "할인방법코드;할인방법코드"; //공시지원금을 의미하는 코드값
_TRK_PNC_ATRN_2 = "공시지원금;공시지원금";
_TRK_PNC_ATRC_3 = "유심형태코드;유심형태코드"; //NFC 유심을 의미하는 코드값
_TRK_PNC_ATRN_3 = "NFC 유심;NFC 유심";
_TRK_PNC_ATRC_4 = "요금제코드;요금제코드"; //해당 요금제를 의미하는 코드값
_TRK_PNC_ATRN_4 = "LTE 온라인 음성 S5;LTE 온라인 음성 S5";
_TRK_PNG = "000;001";
_TRK_EA = "1;1";
_TRK_AMT = "단말기구매금액;유심구매금액";
_TRK_ODNO = "주문번호";
_TRK_PI = "ODR";
</script>
```

유저가 '신규'로 '일반 유심'과 'LTE 유심 (1GB/100분)' 요금제를 '온라인' 신청한 경우 신청 완료 화면에 아래 코드 태깅.
``` html
<script type="text/javascript">
_TRK_PNC = "유심상품코드";
_TRK_PNC_SUB_TP = "온라인";
_TRK_PNC_ATRC_1 = "가입유형코드"; //신규가입을 의미하는 코드값
_TRK_PNC_ATRN_1 = "신규";
_TRK_PNC_ATRC_2 = "";
_TRK_PNC_ATRN_2 = "";
_TRK_PNC_ATRC_3 = "유심형태코드"; //일반 유심을 의미하는 코드값
_TRK_PNC_ATRN_3 = "일반 유심";
_TRK_PNC_ATRC_4 = "요금제코드"; //해당 요금제를 의미하는 코드값
_TRK_PNC_ATRN_4 = "LTE 유심 (1GB/100분)";
_TRK_PNG = "001";
_TRK_EA = "1";
_TRK_AMT = "유심구매금액";
_TRK_ODNO = "주문번호";
_TRK_PI = "ODR";
</script>
```

### 구매 후기 등록횟수 분석
유저가 구매후기를 등록한 횟수를 측정하기 위해 후기등록이 정상적으로 완료되는 시점에 아래 코드를 태깅합니다.

#### 주의사항
'등록' 버튼이 클릭되는 이벤트가 아닌, '추천여부'가 선택되고 후기 '내용'이 작성되어 정상적으로 후기가 등록된 경우에 한해 분석코드가 읽히도록 태깅해 주시면 됩니다.

#### 코드
``` javascript
eval('try{_trk_flashEnvView(
\'_TRK_G3=1\',
\'_TRK_PDV=RVSUBMIT\'
);}catch(_e){}');
```

### 화면별 페이지뷰 분석
화면별 페이지뷰를 분석하기 위해 화면 식별용 코드가 각 화면마다 태깅 되어야 합니다. 아래 표를 참고하여 각 화면에 매핑된 코드를 태깅해 주세요.

화면이름 | 화면코드 | 화면이미지 | 비고
-------- | -------- | -------- | --------
로그인 | LIF | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/001.png) | 
회원가입 | RGF | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/회원가입.png) | 
회원정보입력 | RGF0 | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/회원정보입력.png) | 
회원가입완료 | RGF1 | 화면캡쳐없음 | 
메인 | MAIN | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/07/image003.png) | 
다이렉트샵 | DIRECT | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/directshop.png) | 
휴대폰 목록 | PHONLIST | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/휴대폰목록.png) | /phonList.do?tabgubun=lte, phonList.do?tabgubun=3g 등 모든 /phonList.do 페이지에 코드 태깅
무약정 바른폰 | BARUN | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/무약정바른폰.png) | 
부가서비스 | ADDSRVC | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/부가서비스.png) | /addServiceList.do?searchSupplementaryType=01, /addServiceList.do?searchSupplementaryType=02 등 모든 /addServiceList.do 페이지에 코드 태깅
당첨자 발표 | WINNER | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/당첨자발표.png) | 
요금제 찾기 | RECO | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/나에게맞는요금제찾기.png) | 
구매후기 | REVIEW | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/구매후기.png) | 
고객센터안내 | CS | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/고객센터.png) | 
공식인증 대리점 찾기 | SELLER | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/오프라인매장안내.png) | 
AS센터 찾기 | AS | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/as센터찾기.png) | 
7 POINT 안내 | BENEFIT0 | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/7모바일고객혜택.png) | 
휴대폰 결제 서비스 안내 | BENEFIT1 | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/휴대폰결제서비스안내.png) | 
7MAGAZINE | 7MGZ | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/7mzgazine.png) | 
7DAY 출첵 | 7DAY | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/7day출첵.png) | 
1:1 고객상담 | COUNSEL | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/1-1고객상담.png) | 
이벤트 리스트 | EVTLIST | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/진행이벤트.png) | /event/eventIngList.do
이벤트 상세 | EVT | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/이벤트상세.png) | /event/eventIngView.do 하위의 개별 페이지에 코드 태깅
공시지원금 | GRANT | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/지원금공시.png) | /support/publicFundLte.do 페이지와 /support/publicFund3g.do 페이지에 코드 태깅
제휴카드할인 | DISCNT0 | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/제휴카드할인.png) | 
스페셜약정할인 | DISCNT1 | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/스페셜약정할인제도.png) | 
선택약정할인 | DISCNT2 | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/선택약정할인제도.png) | 
자주하는 질문 | FAQ | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/자주하는질문.png) | 
요금제 & 서비스 | PLANLIST | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/요금제.서비스.png) | /callingPlanList.do?refCode=LTE, /callingPlanList.do?refCode=USIM 등 모든 /callingPlanList.do 페이지에 코드 태깅
전화신청 - 본인인증 & 정보입력 | PHONE0 | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/전화신청-본인인증.정보입력.png) | 
전화신청 - 신청 완료 | PHONE1 | 화면캡쳐없음 | 
온라인 신청 - 약관동의 | ONLINE0 | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/온라인신청-약관동의.png) | 
온라인 신청 - 본인인증 & 정보입력 | ONLINE1 | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/온라인신청-본인인증.정보입력.png) | 
온라인 신청 - 신청 완료 | ONLINE2 | 화면캡쳐없음 | 
선불서비스 | PPSRVC | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/선불서비스.png) | 
선불요금제 | PPPLAN | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/선불요금제.png) | /callingPlanPrepay.do?searchCallPlanType=P, /callingPlanPrepay.do?searchCallPlanType=B 등 모든 /callingPlanPrepay.do 페이지에 코드 태깅
선불 부가서비스 | PPADD | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/선불.png) | 
나의 서비스 | MYSRVC | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/나의서비스.png) | /post/myService.do 페이지에 코드 태깅
요금/납부관리 | CHARGE | 회선가입고객이 아니라서 화면 캡쳐 없음 | /post/chargeInfo.do 페이지에 코드 태깅
사용량 조회 | USAGE | 회선가입고객이 아니라서 화면 캡쳐 없음 | /post/useAmount.do 페이지에 코드 태깅
분실/정지 | PAUSE | 회선가입고객이 아니라서 화면 캡쳐 없음 | /post/changePause.do 페이지에 코드 태깅
서비스 조회/변경 | JOININFO | 회선가입고객이 아니라서 화면 캡쳐 없음 | /post/joinInfo.do 페이지에 코드 태깅
7 POINT | 7POINT | 회선가입고객이 아니라서 화면 캡쳐 없음 | /post/point.do 페이지에 코드 태깅
나의 쇼핑 | CART | 회선가입고객이 아니라서 화면 캡쳐 없음 | /post/shoppingBasketList.do 페이지에 코드 태깅
상품 상세 | PDV | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/상품상세.png) | 위의 **상품분석**에서 다뤘듯이, 단말기 상품과 유심 상품만 '상품'으로써 분석함. 따라서 단말기 상세 화면(/phonListDetail.do)과 유심 상세화면(/usimList.do)에만 PDV 코드를 태깅

#### 코드
``` javascript
_TRK_PI = "화면코드";
```

#### 태깅 예시
유저가 GNB의 다이렉트샵을 클릭하여 다이렉트샵 화면을 조회하는 경우 해당 화면에 아래 코드 태깅
``` html
<script type="text/javascript">
_TRK_PI = "DIRECT";
</script>
```

유저가 GNB가 확장된 메뉴에서 부가서비스를 클릭하여 부가서비스 화면을 조회하는 경우 해당 화면에 아래 코드 태깅
``` html
<script type="text/javascript">
_TRK_PI = "ADDSRVC";
</script>
```

## 적용 후 데이터 검증
코드를 적용한 서버 주소(실서버 또는 개발서버)를 smbae@wisetracker.co.kr, humblejohn@wisetracker.co.kr 로 알려주시기 바랍니다. 정상 적용 여부와 디버깅 필요한 사항 등에 대해서 안내해 드리겠습니다.
