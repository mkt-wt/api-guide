
#SDK 개발자 테스트 검증

## 와이즈트래커 디버깅 모드 세팅

### 1. 안드로이드 

AndroidManifest.xml에 아래값을 추가합니다.

```
	<meta-data
    android:name="WiseTrackerLogState"
    android:value="true" />
```

### 2. iOS

info.plist에 아래값을 추가합니다.

```
	<key>WiseTrackerLogState</key>
	<string>true</string>
```

## 검증테스트

### 공통사용법

#### 데이터 전문 확인
##### 1) Console창에서 `DEBUG_WISETRACKER_JSON[SDK->SERVER]`로 필터링하여 서버로 전송되는 데이터를 확인합니다. 
##### 2) Console창에서 `DEBUG_WISETRACKER_JSON[SERVER->SDK]`로 필터링하여 서버에서 내려오는 Response를 확인합니다.

#### 리포트 확인
##### 1) report.wisetracker.co.kr - 왼쪽 메뉴바에서 설정(톱니바귀) - 유입 및 광고 - 광고URL 테스트 화면으로 진입합니다.
##### 2) ADID(안드로이드), IDFA(iOS) 값을 넣고 조회하기 버튼을 클릭합니다.

![](http://www.wisetracker.co.kr/wp-content/uploads/2020/04/%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%8E%E1%85%A6-1024x577.png)

### 1. Install

#### 1.1 오가닉

##### - 데이터 전문 확인

DEBUG_WISETRACKER_JSON[SDK->SERVER] {"REVENUE":[],**"SESSION"**:{"mvt1":"","machine":"iPhone7,2","userId":"","debug":0,"wifiTp":"2","mat_affiliate_sub":"","icmp_trace":"","iat_source":"","sex":"","uvp5":"","utm_campaign":"","_wtclkTime":"","mvt2":"","WASource":"","latestGcmpid":"","utm_source":"","gclid":"","memLvl":"","_wtUpdTime":0,"mvt3":"","WAAd":"","udVt":1,"WAKeyword":"","iat_campaign":"","mat_medium":"","isUniVt":3,"mat_campaign":"","ocmp":"","iat_kwd":"","pdtk":"","aidChange":1,"uuid":"DC77E35F-91D5-44C1-9082-BAD4743F7ABA","WACampaign":"","profileId":"test.mobile.sdk.wisetracker.co.kr.sdkexample","convTp":0,"mat_source_trace":"","lng":"en-US","ak":"NzQ2NTczNzQyZTZkNmY2MjY5NmM2NTJlNzM2NDZiMmU3NzY5NzM2NTc0NzI2MTYzNmI2NTcyMmU2MzZmMmU2YjcyMmU3MzY0NmI2NTc4NjE2ZDcwNmM2NQ==","icmp":"","utm_content":"","isWfUs":"Y",**"visitNew":"Y"**,"iat_medium":"","_wtUpdSid":"","apVr":"1.048","sid":"8EF799A6-8ED0-4C1C-BB0A-B75D8D640F44","venId":"9F314FBF-026E-422C-9D9A-9EA1D88BB1D0","utm_medium":"","WAApp":"","cntr":"US","fb_source":"",**"ltvt":1**,"tz":"9","ltvi":0,"iat_affiliate":"","openDl":"","slotNo":2,"uvp1":"","appOpenFlag":1,"mat_kwd":"","sr":"375*667/2.0","mat_campaign_trace":"","age":"","responseTp":"json","launchOptions":"","installDate":"2020-04-08 10:40:34","advtIdFlag":1,"memCd":"","uvp2":"","sdk_version":"21.3.21","createTime":1586310034.886048,"advtId":"3D13F785-CB13-4B24-A3B9-E95CD1C46200","mat_source":"","installTimeMillis":1586310034340,"os":"I12","telCom":"KT","uvp3":"","mat_affiliate":"","utm_term":"","mbr":"","WALocation":"","udRvnc":0,"pfno":102,"ltrvnc":0,"WAClassification":"","vtTz":"2020-04-08 10:40:34","iat_affiliate_sub":"","uvp4":"","sarInfo":{},"ltrvni":0},"retryCount":1,"PAGES":[],"CLICK":[],"POSTBACK":{},"GOAL":[]}

--> `SESSION` 데이터 그룹 내 `ltvt:1, visitNew:1` 확인

- DEBUG_WISETRACKER_JSON[SERVER->SDK] {
    "RESPONSE_CODE" = RES001;
    "RESPONSE_MSG" = "Insight Tracker Response Success";
    "SERVER_TIME" = "2020-04-08 11:22:25";
    visitNewServerTime = "2020-04-08 11:22:25";
}

--> 서버 Response `"RESPONSE_CODE" = RES001` 정상 확인 
--> 모든 데이터 전송 테스트 시 추가 확인 필요

##### - 리포트 확인

![](http://www.wisetracker.co.kr/wp-content/uploads/2020/04/%E1%84%8B%E1%85%A9%E1%84%80%E1%85%A1%E1%84%82%E1%85%B5%E1%86%A8%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5-1024x101.png)

--> 광고채널, 광고캠페인 필드가 비어있는지 확인합니다.

#### 1.2 Tracking URL을 통한 설치(Attribution)

##### - 데이터 전문을 통한 확인

DEBUG_WISETRACKER_JSON[SDK->SERVER] {"REVENUE":[],**"SESSION"**:{"mvt1":"","machine":"iPhone7,2","userId":"","debug":0,"wifiTp":"2","mat_affiliate_sub":"","icmp_trace":"","iat_source":"P1513151617373","sex":"","uvp5":"","utm_campaign":"","_wtclkTime":"1586328898694","mvt2":"","WASource":"","latestGcmpid":"","utm_source":"","gclid":"","memLvl":"","_wtUpdTime":1586328996,"mvt3":"","WAAd":"","udVt":1,"WAKeyword":"","iat_campaign":"C1544584120717","mat_medium":"","isUniVt":3,"mat_campaign":"C1544584120717","ocmp":"","iat_kwd":"","pdtk":"","aidChange":1,"uuid":"BCE113EE-D024-4A1E-9D77-F3AFA325FAFE","WACampaign":"","profileId":"test.mobile.sdk.wisetracker.co.kr.sdkexample","convTp":0,"mat_source_trace":"[P1513151617373]","lng":"en-US","ak":"NzQ2NTczNzQyZTZkNmY2MjY5NmM2NTJlNzM2NDZiMmU3NzY5NzM2NTc0NzI2MTYzNmI2NTcyMmU2MzZmMmU2YjcyMmU3MzY0NmI2NTc4NjE2ZDcwNmM2NQ==","icmp":"","utm_content":"","isWfUs":"Y",**"visitNew":"Y"**,"iat_medium":"","_wtUpdSid":"4CD857A4-7E0B-4108-8A68-C79C2B0FE811","apVr":"1.048","sid":"4CD857A4-7E0B-4108-8A68-C79C2B0FE811","venId":"89D83F35-A159-4567-ADC9-F5FECA137AFA","utm_medium":"","WAApp":"","cntr":"US","fb_source":"","ltvt":1,"tz":"9","ltvi":0,"iat_affiliate":"","openDl":"","slotNo":1,"uvp1":"","appOpenFlag":1,"mat_kwd":"","sr":"375*667/2.0","mat_campaign_trace":"[C1544584120717]","age":"","responseTp":"json","launchOptions":"","installDate":"2020-04-08 15:56:33","advtIdFlag":1,"memCd":"","uvp2":"","sdk_version":"21.3.21","createTime":1586328993.651139,"advtId":"3D13F785-CB13-4B24-A3B9-E95CD1C46200","mat_source":"P1513151617373","installTimeMillis":1586328993129,"os":"I12","telCom":"KT","uvp3":"","mat_affiliate":"","utm_term":"","mbr":"","WALocation":"","udRvnc":0,"pfno":102,"ltrvnc":0,"WAClassification":"","vtTz":"2020-04-08 15:56:33","iat_affiliate_sub":"","uvp4":"","sarInfo":{},"ltrvni":0},"retryCount":1,"PAGES":[],"CLICK":[],"POSTBACK":{},"GOAL":[]}


--> `SESSION` 데이터 그룹 내 `"ltvt":1, "visitNew":1`, `"mat_source"`, `"mat_campaign"`,  키에 Tracking URL의 광고캠페인, 광고채널 값으로 세팅 되었는지 확인합니다.


##### - 리포트 확인
![](http://www.wisetracker.co.kr/wp-content/uploads/2020/04/TrackingURL%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5-1024x198.png)

--> 광고채널, 광고캠페인 필드에 `mat_source`, `mat_campaign` 값 조회되는지 확인합니다.

### 2. 회원가입

##### - 데이터 전문 확인

{"SESSION":{"mvt1":"","machine":"iPhone7,2","userId":"","debug":false,"wifiTp":"2","mat_affiliate_sub":"","icmp_trace":"","iat_source":"P1513151617373","sex":"","uvp5":"","utm_campaign":"","_wtclkTime":"1586328883781","mvt2":"","WASource":"","latestGcmpid":"","utm_source":"","gclid":"","memLvl":"","_wtUpdTime":1586329493,"mvt3":"","WAAd":"","udVt":1,"WAKeyword":"","iat_campaign":"C1544584120717","mat_medium":"","isUniVt":0,"mat_campaign":"C1544584120717","ocmp":"","iat_kwd":"","pdtk":"","aidChange":false,"uuid":"BCE113EE-D024-4A1E-9D77-F3AFA325FAFE","WACampaign":"","profileId":"test.mobile.sdk.wisetracker.co.kr.sdkexample","convTp":0,"mat_source_trace":"[P1513151617373]","lng":"en-US","ak":"NzQ2NTczNzQyZTZkNmY2MjY5NmM2NTJlNzM2NDZiMmU3NzY5NzM2NTc0NzI2MTYzNmI2NTcyMmU2MzZmMmU2YjcyMmU3MzY0NmI2NTc4NjE2ZDcwNmM2NQ==","icmp":"","utm_content":"","isWfUs":"N","visitNew":"N","iat_medium":"","_wtUpdSid":"4CD857A4-7E0B-4108-8A68-C79C2B0FE811","apVr":"1.048","sid":"4CD857A4-7E0B-4108-8A68-C79C2B0FE811","venId":"89D83F35-A159-4567-ADC9-F5FECA137AFA","utm_medium":"","WAApp":"","cntr":"US","fb_source":"","ltvt":1,"tz":"9","ltvi":0,"iat_affiliate":"","openDl":"","slotNo":1,"uvp1":"","mat_kwd":"","sr":"375*667\/2.0","mat_campaign_trace":"[C1544584120717]","age":"","responseTp":"json","launchOptions":"","installDate":"2020-04-08 15:56:33","advtIdFlag":true,"memCd":"","uvp2":"","createTime":1586329494.7202759,"advtId":"3D13F785-CB13-4B24-A3B9-E95CD1C46200","mat_source":"P1513151617373","installTimeMillis":1586328993129,"os":"I12","telCom":"KT","uvp3":"","mat_affiliate":"","utm_term":"","mbr":"","WALocation":"","udRvnc":0,"pfno":102,"ltrvnc":0,"WAClassification":"","vtTz":"2020-04-08 15:56:33","iat_affiliate_sub":"","uvp4":"","sarInfo":{},"ltrvni":0},**"GOAL"**:[{"sdk_version":"21.3.21","apVr":"1.048","vtTz":"2020-04-08 16:07:38",**"g1":1**}]}

--> `GOAL` 데이터 그룹 내 `"g1":1`확인

##### - 리포트 확인
![](http://www.wisetracker.co.kr/wp-content/uploads/2020/04/%E1%84%92%E1%85%AC%E1%84%8B%E1%85%AF%E1%86%AB%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%B8-1024x98.png)

### 3. 상품분석

#### 데이터 전문 확인
{"REVENUE":[],"SESSION":{"mvt1":"","machine":"iPhone7,2","userId":"","debug":0,"wifiTp":"2","mat_affiliate_sub":"","icmp_trace":"","iat_source":"P1513151617373","sex":"","uvp5":"","utm_campaign":"","_wtclkTime":"1586328883781","mvt2":"","WASource":"","latestGcmpid":"","utm_source":"","gclid":"","memLvl":"","_wtUpdTime":1586329493,"mvt3":"","WAAd":"","udVt":1,"WAKeyword":"","iat_campaign":"C1544584120717","mat_medium":"","isUniVt":0,"mat_campaign":"C1544584120717","ocmp":"","iat_kwd":"","pdtk":"","aidChange":0,"uuid":"BCE113EE-D024-4A1E-9D77-F3AFA325FAFE","WACampaign":"","profileId":"test.mobile.sdk.wisetracker.co.kr.sdkexample","convTp":0,"mat_source_trace":"[P1513151617373]","lng":"en-US","ak":"NzQ2NTczNzQyZTZkNmY2MjY5NmM2NTJlNzM2NDZiMmU3NzY5NzM2NTc0NzI2MTYzNmI2NTcyMmU2MzZmMmU2YjcyMmU3MzY0NmI2NTc4NjE2ZDcwNmM2NQ==","icmp":"","utm_content":"","isWfUs":"N","visitNew":"N","iat_medium":"","_wtUpdSid":"4CD857A4-7E0B-4108-8A68-C79C2B0FE811","apVr":"1.048","sid":"4CD857A4-7E0B-4108-8A68-C79C2B0FE811","venId":"89D83F35-A159-4567-ADC9-F5FECA137AFA","utm_medium":"","WAApp":"","cntr":"US","fb_source":"","ltvt":1,"tz":"9","ltvi":0,"iat_affiliate":"","openDl":"","slotNo":1,"uvp1":"","appOpenFlag":1,"mat_kwd":"","sr":"375*667/2.0","mat_campaign_trace":"[C1544584120717]","age":"","responseTp":"json","launchOptions":"","installDate":"2020-04-08 15:56:33","advtIdFlag":1,"memCd":"","uvp2":"","sdk_version":"21.3.21","createTime":1586330675.35747,"advtId":"3D13F785-CB13-4B24-A3B9-E95CD1C46200","mat_source":"P1513151617373","installTimeMillis":1586328993129,"os":"I12","telCom":"KT","uvp3":"","mat_affiliate":"","utm_term":"","mbr":"","WALocation":"","udRvnc":0,"pfno":102,"ltrvnc":0,"WAClassification":"","vtTz":"2020-04-08 15:56:33","iat_affiliate_sub":"","uvp4":"","visitNewServerTime":"2020-04-08 13:56:41","sarInfo":{},"ltrvni":0},"retryCount":1,**"PAGES"**:[{**"pngNm":"^신발"**,**"pi":"PDV"**,"vs":10,"csPV":1,**"pnc":"PROD01"**,"vtTz":"2020-04-08 16:24:47","pncNm":"나이키","png":"CAT01","apVr":"1.048","sdk_version":"21.3.21","st_time":1586330686.556521}],"CLICK":[],"POSTBACK":{},"GOAL":[]}

-> `PAGES` 그룹 내 세팅한 `"pi":"PDV", "pnc":"상품코드", "pncNm":"상품명"` 확인

### 4. 구매분석

##### - 데이터 전문 확인

{**"REVENUE"**:[{"mvt2":"mvt2","pncSubTp":"TYPE1;TYPE2","pi":"ODR","mvt1":"mvt1","exhibit":";","pnc":"PROD1;PROD2","sdk_version":"21.3.21","amt":"10000;2000","vtTz":"2020-04-08 16:38:35","mvt3":"mvt3","png":"PCATE1;PCATE2","ea":"24;12","apVr":"1.048"}],"SESSION":{"mvt1":"","machine":"iPhone7,2","userId":"","debug":0,"wifiTp":"2","mat_affiliate_sub":"","icmp_trace":"","iat_source":"P1513151617373","sex":"","uvp5":"","utm_campaign":"","_wtclkTime":"1586328883781","mvt2":"","WASource":"","latestGcmpid":"","utm_source":"","gclid":"","memLvl":"","_wtUpdTime":1586329493,"mvt3":"","WAAd":"","udVt":1,"WAKeyword":"","iat_campaign":"C1544584120717","mat_medium":"","isUniVt":0,"mat_campaign":"C1544584120717","ocmp":"","iat_kwd":"","pdtk":"","aidChange":0,"uuid":"BCE113EE-D024-4A1E-9D77-F3AFA325FAFE","WACampaign":"","profileId":"test.mobile.sdk.wisetracker.co.kr.sdkexample","convTp":0,"mat_source_trace":"","lng":"en-US","ak":"NzQ2NTczNzQyZTZkNmY2MjY5NmM2NTJlNzM2NDZiMmU3NzY5NzM2NTc0NzI2MTYzNmI2NTcyMmU2MzZmMmU2YjcyMmU3MzY0NmI2NTc4NjE2ZDcwNmM2NQ==","icmp":"","utm_content":"","isWfUs":"N","visitNew":"N","iat_medium":"","_wtUpdSid":"4CD857A4-7E0B-4108-8A68-C79C2B0FE811","apVr":"1.048","sid":"4CD857A4-7E0B-4108-8A68-C79C2B0FE811","venId":"89D83F35-A159-4567-ADC9-F5FECA137AFA","utm_medium":"","WAApp":"","cntr":"US","fb_source":"","ltvt":1,"tz":"9","ltvi":0,"iat_affiliate":"","openDl":"","slotNo":1,"uvp1":"","mat_kwd":"","sr":"375*667/2.0","mat_campaign_trace":"","age":"","responseTp":"json","launchOptions":"","installDate":"2020-04-08 15:56:33","advtIdFlag":1,"memCd":"","uvp2":"","sdk_version":"21.3.21","createTime":1586331515.388193,"advtId":"3D13F785-CB13-4B24-A3B9-E95CD1C46200","mat_source":"P1513151617373","installTimeMillis":1586328993129,"os":"I12","telCom":"KT","uvp3":"","mat_affiliate":"","utm_term":"","mbr":"","WALocation":"","udRvnc":4,"pfno":102,"ltrvnc":4,"WAClassification":"","vtTz":"2020-04-08 15:56:33","iat_affiliate_sub":"","uvp4":"","visitNewServerTime":"2020-04-08 13:56:41","sarInfo":{},"ltrvni":0},"retryCount":1,"PAGES":[{"vs":1,"mvt1":"mvt1","mvt2":"mvt2","csPV":1,"mvt3":"mvt3","vtTz":"2020-04-08 16:38:35","apVr":"1.048","sdk_version":"21.3.21","st_time":1586331514.518246}],"CLICK":[],"POSTBACK":{},"GOAL":[]}

--> `REVENUE` 데이터 그룹 내 `"pnc":"상품코드", "ea":수량 "amt":금액 "pnc":상품카테고리` 등 구매 관련 정보 데이터 정상 확인


##### - 리포트 확인
![](http://www.wisetracker.co.kr/wp-content/uploads/2020/04/%E1%84%80%E1%85%AE%E1%84%86%E1%85%A2%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%92%E1%85%AA%E1%86%AB-1024x123.png)


