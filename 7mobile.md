# Wisetracker Integration Guide
'SK 7mobile' 사이트에 와이즈트래커 분석코드를 삽입하는데 필요한 기술문서입니다. 작업 중 발생하는 문의사항은 아래 담당자에게 연락 주시기 바랍니다.

> 정주온, humblejohn@wisetracker.co.kr

# Table of Contents
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
	* [이벤트 구매성과 분석](./7mobile.md#이벤트-구매성과-분석)
		* [코드](./7mobile.md#코드-5)
		* [태깅 예시](./7mobile.md#태깅-예시-5) 
	* [구매 후기 등록횟수 분석](./7mobile.md#구매-후기-등록횟수-분석)
		* [주의사항](./7mobile.md#주의사항-4)
		* [코드](./7mobile.md#코드-6)
	* [화면별 페이지뷰 분석](./7mobile.md#화면별-페이지뷰-분석)
		* [코드](./7mobile.md#코드-7)
		* [태깅 예시](./7mobile.md#태깅-예시-6)
* [적용 후 데이터 검증](./7mobile.md#적용-후-데이터-검증)

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
1) 로그인하는 사용자의 회원정보 중 요금제 정보를 참조해서 값을 입력해야 합니다.
2) `현재요금제코드`, `기존요금제코드`는 아래 표에 있는 코드 값을 참고해 입력해 주세요.

요금제명칭 | 요금제코드
-------- | --------
LTE 유심 (5GB/100분)	| 00000287
LTE 유심 (1GB/100분)	| 00000284
LTE 유심 (3GB/100분)	| 00000285
LTE 어르신 1	| 00000281
LTE 어르신 2	| 00000282
LTE 어르신 3	| 00000283
3G 음성 스페셜1 | 00000272
3G 음성 스페셜2 | 00000273
3G 음성 스페셜3 | 00000274
LTE 음성 스페셜1	| 00000275
LTE 음성 스페셜3	| 00000277
LTE 공신 LEVEL3	| 00000278
LTE 하이 공신 LEVEL3	| 00000279
LTE 음성 스페셜2	| 00000276
LTE 효신 LEVEL1	| 00000266
LTE 효도의 신 | 00000271
LTE 효신 LEVEL2 | 00000267
선불BAND요금제 | 00000265
LTE 태블릿 2GB | 00000262
포켓10GB | 00000263
포켓20GB	| 00000264
3G 음성 V1 | 00000251
3G 음성 V2 | 00000252
3G 음성 V3 | 00000253
3G 음성 V4	| 00000254
3G 음성 V5	| 00000255
LTE 음성 V1	| 00000256
LTE 음성 V2	| 00000257
LTE 음성 V3	| 00000258
LTE 음성 V4	| 00000259
LTE 음성 V5	| 00000260
LTE 공신 LEVEL2	| 00000224
LTE 공신 LEVEL1	| 00000223
3G 온라인 음성 S3	| 00000236
LTE 온라인 음성 S3	| 00000230
LTE 온라인 데이터 S2	| 00000243
LTE 온라인 데이터 S3	| 00000242
LTE 온라인 음성 S5	| 00000228
LTE 온라인 데이터 S5	| 00000240
LTE 온라인 데이터 S6	| 00000239
LTE온라인6GB	| 00000226
3G 온라인 음성 S1	| 00000238
3G 온라인 음성 S2	| 00000237
3G 온라인 음성 S4	| 00000235
3G 온라인 음성 S5	| 00000234
3G 온라인 음성 S6	| 00000233
LTE 온라인 음성 S1	| 00000232
LTE 온라인 음성 S2	| 00000231
LTE 온라인 데이터 S1	| 00000244
LTE 온라인 음성 S4	| 00000229
LTE 온라인 데이터 S4	| 00000241
LTE 온라인 음성 S6	| 00000227
LTE온라인4.5GB	| 00000225
I LIKE MUSIC	| 00000219
LTE온라인1GB	| 00000210
공신LEVEL1	| 00000213
공신LEVEL2	| 00000214
공신LEVEL3	| 00000215
3G착한음성	| 00000217
LTE온라인500MB	| 00000209
LTE착한음성	| 00000216
LTE온라인2GB	| 00000211
LTE온라인3GB	| 00000212
LTE 알뜰형	| 00000206
LTE하이음성	| 00000207
LTE하이데이터	| 00000208
LTE 실속 음성	| 00000205
LTE 실속 데이터	| 00000204
하이 표준	| 00000195
LTE 알뜰 100MB	| 00000196
LTE실속200MB	| 00000187
LTE실속제로	| 00000186
싼 LTE 유심 5GB	| 00000191
싼 LTE 유심 9GB	| 00000192
LTE 음성 다 유심 6.5GB	| 00000190
LTE실속1GB	| 00000188
LTE실속2GB	| 00000189
LTE 음성 다 유심 11GB	| 00000174
LTE 음성 다 유심 300MB	| 00000171
LTE 음성 다 유심 1.2GB	| 00000172
LTE 음성 다 유심 3.5GB	| 00000173
착한LTE42	| 00000169
바른LTE온라인16	| 00000170
바른LTE유심14	| 00000168
바른LTE유심15	| 00000167
바른 LTE15	| 00000163
바른 LTE19	| 00000164
바른 LTE25	| 00000165
아시아나항공 19	| 00000200
아시아나항공 28	| 00000199
아시아나항공 34	| 00000198
LTE USIM 세이프 35	| 00000180
LTE_태블릿_2.5GB	| 00000156
LTE_태블릿_5GB	| 00000157
싼 LTE 유심 15	| 00000155
알뜰한33	| 00000148
알뜰한43	| 00000149
NEW 키즈표준	| 00000081
공부의신	| 00000082
NEW 청소년34	| 00000083
LTE 공신 데이터	| 00000084
NEW 청소년LTE34	| 00000085
데이터중심20GB_3G	| 00000143
데이터중심35GB_3G	| 00000144
데이터중심11GB_3G	| 00000142
데이터중심20GB_LTE	| 00000146
데이터중심35GB_LTE	| 00000147
데이터중심11GB_LTE	| 00000145
싼 LTE 유심 17	| 00000139
싼 LTE 유심 26	| 00000141
싼 LTE 유심 21	| 00000140
데이터중심300MB_3G	| 00000129
데이터중심1.2GB_3G	| 00000130
데이터중심2.2GB_3G	| 00000131
데이터중심3.5GB_3G	| 00000132
데이터중심6.5GB_3G	| 00000133
데이터중심300MB_LTE	| 00000134
데이터중심1.2GB_LTE	| 00000135
데이터중심2.2GB_LTE	| 00000136
데이터중심3.5GB_LTE	| 00000137
데이터중심6.5GB_LTE	| 00000138
착한온라인18	| 00000128
착한망내14	| 00000125
착한망내17	| 00000124
착한할인17	| 00000126
착한할인19	| 00000127
싸게쓰는 USIM 8	| 00000122
무조건반값 22	| 00000120
USIM 표준	| 00000121
싸게쓰는 USIM 13	| 00000123
LTE24	| 00000119
뉴알뜰14	| 00000113
스페셜16	| 00000116
스페셜18	| 00000117
표준 | 00000114
음성알뜰19 | 0RB00046
알뜰국제음성19	| 00000201
알뜰국제19	| 00000202
음성알뜰25	| 00000108
폰드림알뜰25	| 00000106
무조건반값 17	| 00000078
싸게쓰는 LTE USIM 21	| 00000079
싸게쓰는 LTE USIM 25	| 00000080
복지USIMLTE39	| 00000072
복지 LTE 59	| 00000073
복지 LTE 69	| 00000074
복지 LTE 82	| 00000075
복지 LTE 97	| 00000076
복지USIM3G25	| 00000071
맞춤29 (데이터)	| 00000070
맞춤29 (표준)	| 00000069
맞춤29 (음성)	| 00000068
내맘대로29	| 00000053
폰드림알뜰19	| 00000105
절대프리 요금제	| 00000046
망내29	| 00000020
3G_00700엔망내35	| 00000021
3G_00700엔망내55	| 00000023
반값	| 00000002
3G_00700엔망내45	| 00000022
실버(복지형)	| 00000005
소리사랑11(복지형)	| 00000006
LTE_00700엔망내35	| 00000037
LTE_00700엔망내45	| 00000038
LTE_00700엔망내55	| 00000039
LTE32	| 00000030
LTE39	| 00000031
LTE49	| 00000032
프리미엄	| 00000104
일반	| 00000101
라이트	| 00000102
플러스 (구 티머니) | 00000103


#### 코드
``` javascript
eval('try{_trk_flashEnvView(
\'_TRK_PI=LIR\',
\'_TRK_ISLOGIN=Y\',
\'_TRK_MBR=Y\',
\'_TRK_UVP1=현재요금제코드\',
\'_TRK_UVP2=기존요금제코드\',
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
\'_TRK_UVP1=00000103\',
\'_TRK_UVP2=00000101\',
\'_TRK_G2=1\'
);}catch(_e){}');
```

40대 남성이며 아무런 요금제도 사용하지 않는 유저가 로그인한 경우.
``` javascript
eval('try{_trk_flashEnvView(
\'_TRK_PI=LIR\',
\'_TRK_ISLOGIN=Y\',
\'_TRK_MBR=Y\',
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
1) '상품'에는 두가지가 있는 것으로 정의 했습니다. 단말기상품과 유심상품 입니다(즉, 요금제나 부가서비스 등은 상품으로 분석하지 않습니다). 따라서 '단말기'와 '유심' 상세 페이지에만 아래 코드들을 적용해 주시기 바랍니다.
2) 상품명에 세미콜론(;)이 들어가서는 안됩니다. 시스템에서 정상적으로 인식하지 못합니다.
3) HTML Entity 형태의 상품명을 값으로 넣는 경우 위의 2번에 해당하게 됩니다. raw text 그대로를 값으로 넣어 주시기 바랍니다.

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
_TRK_PNC = "uniqueUsimCd"; //유심에 대한 고유 코드 입력
_TRK_PNC_NM = "유심";
_TRK_PNG = "001"; //유심일 경우 001 입력
_TRK_PNG_NM = "유심";
_TRK_PI = "PDV";
</script>
```

유저가 갤럭시J4+ 상세화면을 조회하는 경우 해당 화면에 아래 코드 태깅.
``` html
<script type="text/javascript">
_TRK_PNC = "PE00003010"; //해당 단말기의 고유 코드 입력
_TRK_PNC_NM = "갤럭시J4+";
_TRK_PNG = "000"; //단말기일 경우 000 입력
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
1) 단말기 구매 시 유심 상품도 함께 구매하게 되어 있습니다. 결국 한 건의 구매에 '단말기 상품', '유심 상품' 총 2개의 상품이 포함됩니다.
2) 따라서 위와 같이 한번의 구매에 복수의 상품이 포함된 경우, 환경변수의 값에 세미콜론(;)을 사용해 다수의 정보를 구분해서 넣어야 합니다. 아래 예시를 참고해 주세요. 
3) 온라인 신청 완료 화면, 그리고 전화 신청 완료 화면에 분석 코드를 태깅해 주시기 바랍니다.

#### 코드
``` javascript
_TRK_PNC = "상품코드";
_TRK_PNC_SUB_TP = "신청유형"; //온라인 신청이면 '온라인'을, 전화 신청이면 '전화'를 입력
_TRK_PNC_SUB_TP2 = "가입유형"; //번호이동, 신규, 기기변경 
_TRK_PNC_SUB_TP3 = "할인방법"; //공시지원금 or 선택약정만 포함. 카드할인은 포함하지 않음
_TRK_PNC_SUB_TP4 = "유심명칭"; //일반유심 or NFC유심
_TRK_PNC_SUB_TP5 = "요금제명칭";
_TRK_PNG = "범주코드"; //단말기는 000, 유심은 001
_TRK_EA = "주문수량";
_TRK_AMT = "구매금액"; //유저가 실제 지불하는 금액 입력
_TRK_ODNO = "주문번호"; //해당 주문건의 유니크한 주문번호 입력
_TRK_PI = "ODR";
_TRK_UVP3 = "이전 사업자 코드" //번호이동인 경우 세븐모바일로 변경하기 이전에 사용하던 통신사의 '코드' 입력, 알파뉴메릭 8자리까지 입력 가능
```

#### 태깅 예시
기존에 '케이티스' 통신사를 사용하던 유저가 '번호이동'으로 '갤럭시J4+' 단말기, 'LTE 온라인 음성 S5' 요금제, 'NFC 유심'을 구매하면서 '공시지원금'을 선택해 '전화'로 신청한 경우 신청 완료 화면에 아래 코드 태깅.
``` html
<script type="text/javascript">
<!-- 복수의 상품을 구매하는 경우 세미콜론을 사용하여 상품과 상품을 구분함 -->
_TRK_PNC = "단말기상품코드;유심상품코드";
_TRK_PNC_SUB_TP = "전화;전화";
_TRK_PNC_SUB_TP2 = "번호이동;번호이동";
_TRK_PNC_SUB_TP3 = "공시지원금;공시지원금";
_TRK_PNC_SUB_TP4 = "NFC유심;NFC유심";
_TRK_PNC_SUB_TP5 = "LTE 온라인 음성 S5;LTE 온라인 음성 S5";
_TRK_PNG = "000;001";
_TRK_EA = "1;1";
_TRK_AMT = "단말기구매금액;유심구매금액";
_TRK_ODNO = "주문번호";
_TRK_PI = "ODR";
_TRK_UVP3 = "K14"
</script>
```

유저가 '신규'로 '일반 유심'과 'LTE 유심 (1GB/100분)' 요금제를 '온라인' 신청한 경우 신청 완료 화면에 아래 코드 태깅.
``` html
<script type="text/javascript">
_TRK_PNC = "유심상품코드";
_TRK_PNC_SUB_TP = "온라인";
_TRK_PNC_SUB_TP2 = "신규가입";
_TRK_PNC_SUB_TP3 = "";
_TRK_PNC_SUB_TP4 = "일반유심";
_TRK_PNC_SUB_TP5 = "LTE 유심 (1GB/100분)";
_TRK_PNG = "001";
_TRK_EA = "1";
_TRK_AMT = "유심구매금액";
_TRK_ODNO = "주문번호";
_TRK_PI = "ODR";
_TRK_UVP3 = ""
</script>
```

### 이벤트 구매성과 분석
개별 이벤트가 단말기 또는 유심 상품 구매에 어떤 영향을 주었는지를 분석하기 위한 코드입니다. 이벤트 상세 페이지에 코드가 태깅 되어야 합니다. 

#### 코드
``` javascript
_TRK_MVT3 = "이벤트명";
_TRK_PI = "EVT";
```

#### 태깅 예시
유저가 '8월 인기 공기계 한정판매!' 이벤트 페이지에 진입한 경우 해당 화면에 아래 코드 태깅.
``` html
<script type="text/javascript">
_TRK_MVT3 = "8월 인기 공기계 한정판매!";
_TRK_PI = "EVT";
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
온라인 신청 - 약관동의 | ONLINE0 | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/온라인신청-약관동의.png) | 
온라인 신청 - 본인인증 & 정보입력 | ONLINE1 | [링크](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/온라인신청-본인인증.정보입력.png) | 
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
