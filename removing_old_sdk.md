# 구버전 SDK 제거 방법 안내
최신버전 SDK의 설치는 Bintray, CocoaPods로 제공합니다. 이 방법을 사용하지 않고 설치된 과거 버전의 SDK는 올바른 방법으로 삭제된 후 업데이트해야 하기 때문에 본 가이드에서 정확한 삭제 방법을 안내하고 있습니다. 진행 중 발생하는 문의사항은 아래 연락처로 알려주시기 바랍니다.

> 와이즈트래커 개발팀, tech@wisetracker.co.kr

# Table of Contents
* [구버전 Android SDK 삭제](./removing_old_sdk.md#구버전-Android-SDK-삭제)
	* [기설치된 라이브러리 파일 삭제](./removing_old_sdk.md#1-기설치된-라이브러리-파일-삭제)
	* [의존성 제거](./removing_old_sdk.md#2-의존성-제거)
		* [Project/build.gradle](./removing_old_sdk.md#1-projectbuildgradle-%ED%8C%8C%EC%9D%BC%EC%97%90-%EC%95%84%EB%9E%98-%EC%BD%94%EB%93%9C-%EC%82%BD%EC%9E%85%EB%90%9C-%EA%B2%BD%EC%9A%B0-%EC%A0%9C%EA%B1%B0)
		* [app/build.gradle](./removing_old_sdk.md#2-appbuildgradle-%ED%8C%8C%EC%9D%BC%EC%97%90-%EC%95%84%EB%9E%98-%EC%BD%94%EB%93%9C-%EC%82%BD%EC%9E%85%EB%90%9C-%EA%B2%BD%EC%9A%B0-%EC%A0%9C%EA%B1%B0)
	* [최신 SDK로 업데이트](./removing_old_sdk.md#3-아래-가이드-참고하여-최신-SDK로-업데이트)
* [구버전 iOS SDK 삭제](./removing_old_sdk.md#구버전-iOS-SDK-삭제)
	* [기설치된 프레임워크와 파일들 삭제](./removing_old_sdk.md#1-기설치된-프레임워크와-파일들-삭제)
	* [CocoaPods로 최신 SDK 설치](./removing_old_sdk.md#2-CocoaPods로-최신-SDK-설치)
	* [정상 설치 시 해당폴더 구조](./removing_old_sdk.md#3-정상-설치-시-해당폴더-구조)

## 구버전 Android SDK 삭제
### 1. 기설치된 라이브러리 파일 삭제
안드로이드 프로젝트 Project app/libs/ 경로에 삽입된 WiseTracker.jar 파일 삭제
![](http://www.wisetracker.co.kr/wp-content/uploads/2019/10/%E1%84%80%E1%85%B5%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5_%E1%84%8B%E1%85%AE%E1%86%AB%E1%84%8B%E1%85%A7%E1%86%BCSDK_%E1%84%91%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%89%E1%85%A1%E1%86%A8%E1%84%8C%E1%85%A6.png)

### 2. 의존성 제거
#### (1) Project/build.gradle 파일에 아래 코드 삽입된 경우 제거
``` java
allprojects {
	repositories {
		......
		maven { url "http://repo.spring.io/plugins-release"} // 제거
	}
}
```

#### (2) app/build.gradle 파일에 아래 코드 삽입된 경우 제거
``` java
dependencies {
	.......
	implementation 'com.firebase:firebase-jobdispatcher-with-gcm-dep:0.8.5' // 제거
	compile group: 'commons-net', name: 'commons-net', version: '3.6' // 제거
}
```

### 3. 아래 가이드 참고하여 최신 SDK로 업데이트
-> https://bintray.com/beta/#/tracker/maven/SDK_V1?tab=readme

## 구버전 iOS SDK 삭제
### 1. 기설치된 프레임워크와 파일들 삭제
![](http://www.wisetracker.co.kr/wp-content/uploads/2019/10/deletefile.png)
![](http://www.wisetracker.co.kr/wp-content/uploads/2019/10/delete.png)

### 2. CocoaPods로 최신 SDK 설치 
- [CocoaPods 이용한 설치 가이드](https://github.com/WisetrackerTechteam/wisetrackerSDK/blob/master/README.md#WISETRACKER_COCOAPOD)
- 단, "2. iOS에서 제공하는 라이브러리와 Build Settings에 설정을 추가합니다."에 해당하는 내용은 이미 설치 및 세팅이 되어있으므로 진행 안하셔야 합니다.

### 3. 정상 설치 시 해당폴더 구조
![](http://www.wisetracker.co.kr/wp-content/uploads/2019/10/installDone.png)
