# Web to App 수집을 위한 설정 방법

### 1) 웹 광고 랜딩이 되는 페이지에 와이즈트래커 Web to App 분석 스크립트 삽입
Web to App을 분석하기 위해서는 분석하려고 하는 웹 페이지에 모두 저희 Web to App 분석 스크립트가 포함되어 있어야 합니다. 아래 스크립트를 각 페이지 header 부분에 추가합니다.

```html
    <script src="https://applog.ssgdfs.com/wa/js/wiseWebTrack.js"></script>
```

### 2) 해당 페이지에서 mcd 파라미터를 사용해 Web to App script의 init 호출.
https://test-www.ssgdfs.com/kr/event/initEventDetail?event_no=E210404297&mcd1=01&mcd2=skt&mcd3=common&mcd4=mass&mcd5=ssg

위 예시 URL로 랜딩 시에 아래와 같은 형태로 설정해주시면 됩니다. \_cps:"IndirectInflowByWeb" 값은 리포트에서 일반 광고와 웹투앱 광고를 구분하기 위해 사용되는 값으로 항상 포함되어야 합니다.

```html
<script>
  $(document).ready(function(){  
    // webTracker 초기화.
    _wiseWebTrack.init({
        _wtno:10063, // 프로파일 번호
        _wthst:"applog.ssgdfs.com", // http 에서 호출하는 경우 applog.ssgdfs.com:8080, https에서 호출하는 경우 applog.ssgdfs.com
        _wtufn:"ALL",
        _wtfv:"server",
        _cps:"IndirectInflowByWeb",
        _wts:"01",
        _wtc:"skt",
        _wtm:"common",
        _wtw:"mass",
        _wtaffid:"ssg"
    });
  });
</script>
```

### 3) 앱으로 이동 버튼 클릭 시에 Web to App 스크립트의 redirection 함수 사용.
앱으로 이동하는 버튼에 저희 Web to App 스크립트의 redirection 함수를 사용합니다.

```html
<script>
function moveToApp(){
    if(confirm("앱으로 이동하시겠습니까?") == true){    
        _wiseWebTrack.redirection({
            _wtpkg:"앱 패키지명",
            _wtdl:"스토어 URL",
            _wtal:"딥링크 URL",
            _iaH:"앱 없는 경우 이동될 URL"
        });
    }else{  
       return;
    }
}
</script>
<button onClick="moveToApp()">앱으로 이동하기</button> 
```
