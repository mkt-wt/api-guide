# Wisetracker Integration Guide
'MyNB'앱으로 연결되는 snsGate.do 페이지에 와이즈트래커를 웹투앱 어트리뷰션을 추가하는데 필요한 기술문서입니다. 작업 중 발생하는 문의사항은 아래 담당자에게 연락 주시기 바랍니다.

> 정주온, humblejohn@wisetracker.co.kr

# Index
* [웹투앱 어트리뷰션 설정](./mynb.md#웹투앱-어트리뷰션-설정)

## 웹투앱 어트리뷰션 설정
현재 http://m.newbalancemynb.com/home/snsGate.do 페이지는 유저가 랜딩되면, 에이전트를 읽어서 플랫폼울 구분한 뒤 딜레이로 상황을 판단하여 앱 설치 또는 딥링크 이동을 처리하고 있습니다.
광고주의 요청은 http://m.newbalancemynb.com/home/snsGate.do 페이지를 통해서 얼마나 많은 앱 설치 또는 이벤트 페이지 이동이 발생하는지 트래킹 하는 것으로, 이를 위해 아래 설정을 적용해 주시기 바랍니다.

먼저 아래 코드를 페이지의 <head>에 추가합니다.

``` html
<head>
...
<!-- Wisetracker web-to-app SDK -->
<script src="https://cdn.wisetracker.co.kr/wa/js/wiseWebTrack.js"></script>
...
</head>
```

페이지에 아래 코드를 추가하여 와이즈트래커 초기화 함수를 호출합니다.
``` javascript
$(document).ready(function(){  
	// webTracker 초기화 
	_wiseWebTrack.init();
});
```

마지막으로 유저를 스토어 또는 앱으로 이동시킬때 아래 코드를 추가합니다. 유저의 앱 유무는 `redirection`함수에서 판단하므로, snsGate.do 페이지의 소스 중에서 앱 유무 판단하는 부분은 제거해 주시기 바랍니다.
``` javascript
// 에이전트 체크 로직

if(os == "android"){
	_wiseWebTrack.redirection({
		// Requirement parameter
		version:"V2",
		_wtno:10028,
		_wthst:"trk.wisetracker.co.kr",
		_wtufn:"ALL",
		_wtp:7,
		_wtfv:"server",
		_wtpkg:"com.nbkorea.mynb", 
		_wtdl:"market://details?id=com.nbkorea.mynb&hl=ko",
		_wtal:"앱으로 연결할 딥링크", //예를 들어 mynb://?cmd=link&url=http://m.newbalancemynb.com/event/eventDetail.do?eventIdx=44
		createClickData:"Y"
	});
}else if(os == "ios"){
	_wiseWebTrack.redirection({
	// Requirement parameter
	version:"V2",
	_wtno:10028,
	_wthst:"trk.wisetracker.co.kr",
	_wtufn:"ALL",
	_wtp:7,
	_wtfv:"server",
	_wtpkg:"com.nbkorea.mynb",
	_wtdl:"https://apps.apple.com/kr/app/mynb/id1143467078?mt=8",
	_wtal:"앱으로 연결할 딥링크", //예를 들어 mynb://?cmd=link&url=http://m.newbalancemynb.com/event/eventDetail.do?eventIdx=44
	createClickData:"Y"
	});
}
```
