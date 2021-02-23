# Wisetracker Integration Guide
'오늘룩' 웹사이트에서 데이터를 측정하는데 필요한 코드를 적용하는 방법을 안내하는 문서입니다. 진행 중에 발생하는 기술적인 이슈는 아래 담당 개발자에게 연락 주시기 바랍니다.

> 정주온, humblejohn@wisetracker.co.kr, tech@wisetracker.co.kr



## Index

* [공통 스크립트 추가](./oneulook_web_20210222.md#공통-스크립트-추가)
* [메인 페이지 버튼 클릭 측정](./oneulook_web_20210222.md#메인-페이지-버튼-클릭-측정)
* [옷 구경 하기 페이지 버튼 클릭 측정](./oneulook_web_20210222.md#옷-구경-하기-페이지-버튼-클릭-측정)
* [모델 신청 완료 측정](./oneulook_web_20210222.md#모델-신청-완료-측정)
* [메인 페이지 페이지뷰 측정](./oneulook_web_20210222.md#메인-페이지-페이지뷰-측정)
* [옷 구경 하기 페이지 페이지뷰 측정](./oneulook_web_20210222.md#옷-구경-하기-페이지-페이지뷰-측정)
* [신청 페이지 페이지뷰 측정](./oneulook_web_20210222.md#신청-페이지-페이지뷰-측정)



### 공통 스크립트 추가

메일을 통해 별도로 전달해드린 `10284_Insight_WebAnalytics.txt` 파일의 확장자를 js로 변경하신 뒤, 사이트의 footer 영역에 include 해주시기 바랍니다. 아래는 공통 스크립트가 추가되었을 때의 예시입니다.

```html
<!-- footer -->
<script src="your-site-directory/10284_Insight_WebAnalytics.js"></script>
```



### 메인 페이지 버튼 클릭 측정

아래 이미지에 있는 6개 버튼이 클릭되는 시점에, 아래 *매핑 테이블* 에 있는 `buttonName`과 `goalNumber` 값을 참고하여 분석 코드를 추가해 주시면 됩니다.

![이미지0](http://www.wisetracker.co.kr/wp-content/uploads/2021/02/oneulook01.png)



#### 매핑 테이블

| 버튼 번호 | buttonName | goalNumber |
| :---: | --- | --- |
| 1 | 상단 인스타 아이콘 | G3 |
| 2 | 모델 지원하기 | G4 |
| 3 | 옷 구경 하기 | G5 |
| 4 | 인스타에서 더 구경하기 | G6 |
| 5 | 모델 지원하기 - 하단 | G7 |
| 6 | 옷 구경 하기 - 하단 | G8 |



#### 분석 코드

```javascript
_trk_clickTrace("EVT", "buttonName"); // buttonName 부분을 매핑 테이블에 있는 정보로 치환
eval('try{_trk_flashEnvView(\'_TRK_goalNumber=1\');}catch(_e){}'); // goalNumber 부분을 매핑 테이블에 있는 정보로 치환
```



#### 적용 예시

메인 페이지 상단에 있는 모델 지원하기 버튼(2번 버튼)이 클릭되는 시점(클릭 이벤트)에 아래 코드 추가

```javascript
_trk_clickTrace("EVT", "모델 지원하기");
eval('try{_trk_flashEnvView(\'_TRK_G4=1\');}catch(_e){}');
```



### 옷 구경 하기 페이지 버튼 클릭 측정

아래 이미지에 있는 버튼이 클릭되는 시점에 분석 코드를 추가해 주시면 됩니다.

![이미지1](http://www.wisetracker.co.kr/wp-content/uploads/2021/02/oneulook02.png)


#### 분석 코드

```javascript
_trk_clickTrace("EVT", "모델 지원하기 - 옷 구경하기 페이지");
eval('try{_trk_flashEnvView(\'_TRK_G9=1\');}catch(_e){}');
```



### 신청 완료  페이지 버튼 클릭 측정

아래 이미지에 있는 버튼이 클릭되는 시점에 분석 코드를 추가해 주시면 됩니다.

![이미지2](http://www.wisetracker.co.kr/wp-content/uploads/2021/02/oneulook03.png)


#### 분석 코드

```javascript
_trk_clickTrace("EVT", "오늘룩 인스타 구경가기 - 신청완료 페이지");
eval('try{_trk_flashEnvView(\'_TRK_G10=1\');}catch(_e){}');
```



### 모델 신청 완료 측정

신청 완료 화면 내에 아래 코드를 추가해 주시기 바랍니다.

```html
<script type="text/javascript">
	_TRK_PI = "COMPLETE";
	_TRK_G11 = "1";
</script>
```



### 메인 페이지 페이지뷰 측정

메인 페이지 내에 아래 코드를 추가해 주시기 바랍니다.

```html
<script type="text/javascript">
	_TRK_PI = "MAIN";
</script>
```



### 옷 구경 하기 페이지 페이지뷰 측정

옷 구경 하기 페이지 내에 아래 코드를 추가해 주시기 바랍니다.

```html
<script type="text/javascript">
	_TRK_PI = "CLOTHES";
</script>
```



### 신청 페이지 페이지뷰 측정

모델 신청에 필요한 정보를 입력하는 페이지 내에 아래 코드를 추가해 주시기 바랍니다.

```html
<script type="text/javascript">
	_TRK_PI = "SUBMIT";
</script>
```

