서비스 언어 설정 기능 추가에 따른 태깅 가이드입니다.

# Android
### 1. SDK 버전 업데이트    
build.gradle에 있는 Wisetracker SDK 버전을 아래 버전으로 변경
```
kr.co.wisetracker.insight:SDK_V1:21.3.55
```

### 2. AndroidMenifest.xml에 아래 태그 추가
```xml
<meta-data android:name="WiseTrackerUseBaseProvider" android:value="false"></meta-data>
```

### 3. 서비스 언어별 설치 분석을 위해 Wisetracker.init 전에 putFirstInitData API를 호출
```java
WiseTracker.putFirstInitData("service_lang", "ServiceLanguage");
WiseTracker.init();
```
**putFirstInitData는 반드시 init 전에 위치하여야 합니다.**    
**서비스 언어별 설치 분석을 위한 설정**이며 putFirstInitData는 <u>**최초 앱 실행 시에만 전달 받은 데이터를 서비스 언어로 설정**</u>합니다.    
putFirstInitData를 통해 설정된 서비스 언어는 아래 4번 설정을 통해 서비스 언어를 명시적으로 변경하기 전까지 계속 유지가 됩니다.    
위 예제 코드의 **"ServiceLanguage" 값은 샘플이며 실제 사용하는 언어 코드 값으로 치환**이 되어야 합니다.

### 4. 서비스 언어 변경 시점에 서비스 언어 변경 API와 새로운 새션 발급 API 호출
```java
WiseTracker.setServiceLanguage("ServiceLanguage");
WiseTracker.createNewSession();
```

# iOS

### 1. SDK 버전 업데이트    
podfile내 WiseTracker SDK 버전을 아래 버전으로 변경
```
pod 'WiseTracker', '~> 21.3.30'
```

### 2. 서비스 언어별 설치 분석을 위해 Wisetracker.init 전에 putFirstInitData API를 호출
```swift
WiseTracker.putFirstInitData(StaticValues.param_SRVC_LANG(), value: "ServiceLanguage")
WiseTracker.initEnd()
```
**putFirstInitData는 반드시 initEnd 전에 위치하여야 합니다.**    
**서비스 언어별 설치 분석을 위한 설정**이며 putFirstInitData는 <u>**최초 앱 실행 시에만 전달 받은 데이터를 서비스 언어로 설정**</u>합니다.    
putFirstInitData를 통해 설정된 서비스 언어는 아래 4번 설정을 통해 서비스 언어를 명시적으로 변경하기 전까지 계속 유지가 됩니다.    
위 예제 코드의 **"ServiceLanguage" 값은 샘플이며 실제 사용하는 언어 코드 값으로 치환**이 되어야 합니다.

### 4. 서비스 언어 변경 시점에 서비스 언어 변경 API와 새로운 새션 발급 API 호출
```swift
WiseTracker.setServiceLanguage("ServiceLanguage");
WiseTracker.createNewSession();
```
