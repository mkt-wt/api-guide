# Wisetracker Integration Guide
'리턴: 방치형RPG' 게임의 Android 앱에 연동할 와이즈트래커 인앱 이벤트를 안내하는 문서입니다.

# Index
* [캐릭터 생성](./return.md#캐릭터-생성)
* [로그인](./return.md#로그인)
	* [주의사항](./return.md#주의사항)
	* [분석코드](./return.md#분석코드)
* [레벨업](./return.md#레벨업)
	* [분석코드](./return.md#분석코드-1)
	* [적용예시](./return.md#적용예시)
* [인앱구매](./return.md#인앱구매)
	* [주의사항](./return.md#주의사항-1)
	* [분석코드](./return.md#분석코드-2)
	* [적용예시](./return.md#적용예시)
* [적용 후 데이터 검증](./return.md#적용-후-데이터-검증)
	* [AOS](./return.md#AOS)


## 캐릭터 생성
유저가 캐릭터에 이름을 부여하여 캐릭터 생성이 완료된 시점에 아래 코드를 추가합니다.
``` kotlin
// 캐릭터 이름이 결정됨
WiseTracker.setPageIdentity("RGR");
WiseTracker.setGoal("g1", 1);
WiseTracker.sendGoalData();
```

## 로그인
유저가 앱을 실행하여 정상적으로 로그인 완료된 시점에 아래 코드를 추가합니다.

### 주의사항
'리턴: 방치형RPG'의 경우 구글 게임 계정으로 자동 로그인됩니다. 이렇게 자동 로그인 될때마다 아래 코드가 동작하도록 설정해야 합니다. 

### 분석코드
``` kotlin
// 로그인 완료 처리
WiseTracker.setPageIdentity("LIR");
WiseTracker.setGoal("g2", 1);
WiseTracker.sendGoalData();
```

## 레벨업
캐릭터의 레벨이 상승한 시점에 아래 코드를 추가합니다.

### 분석코드
``` kotlin
// 레벨 상승
WiseTracker.setUserAttribute( "uvp1", "달성한 레벨" );
WiseTracker.setGoal("g3", 1);
WiseTracker.setGoal("g4", 이전 레벨);
WiseTracker.setGoal("g5", 달성한 레벨);
WiseTracker.sendTransaction();
```

### 적용예시
캐릭터의 레벨이 24에서 25로 상승한 경우, 상승 시점에 아래 코드 추가
``` kotlin
// 레벨 25로 상승
WiseTracker.setUserAttribute( "uvp1", "25" );
WiseTracker.setGoal("g3", 1);
WiseTracker.setGoal("g4", 24);
WiseTracker.setGoal("g5", 25);
WiseTracker.sendTransaction();
```

## 인앱구매
유저가 유료 아이템을 결제한 경우가 인앱구매에 해당합니다. 인앱구매가 완료된 시점에 아래 코드를 추가합니다.

### 주의사항
1) 결제금액은 원화(KRW) 기준의 액수만을 사용해 주시기 바랍니다.
2) 게임머니(골드, 다이아몬드, 마일리지)를 사용하여 아이템을 구매한 경우에는 본 코드를 적용하지 않습니다. 오직 실제 화폐로 아이템을 구매한 경우에만 본 코드를 적용해주세요.


### 분석코드
``` kotlin
// 인앱구매 완료
WiseTracker.setOrderProduct("상품코드");
WiseTracker.setOrderQuantity(상품수량);
WiseTracker.setOrderAmountArray(결제금액);
WiseTracker.setOrderNo("주문번호");
WiseTracker.setPageIdentity("ODR");
WiseTracker.sendTransaction();
```

### 적용예시
유저가 스타터 패키지를 결제한 경우
``` kotlin
// 스타터 패키지 결제 완료
WiseTracker.setOrderProduct("P12345"); // 스타터 패키지의 상품코드
WiseTracker.setOrderQuantity(1);
WiseTracker.setOrderAmountArray(5500); // KRW 기준 결제액 입력
WiseTracker.setOrderNo("O12345678");
WiseTracker.setPageIdentity("ODR");
WiseTracker.sendTransaction();
```

## 적용 후 데이터 검증
SDK와 API가 올바르게 적용 되었는지 확인하기 위해서는 아래 코드(디버그 모드 활성화)를 적용한 테스트 앱을 저희 쪽으로 보내주시면 됩니다. 보내주신 테스트 앱에서 데이터를 확인한 후 결과에 대해서 회신 드리고 있습니다.

### AOS
AndroidManifest.xml 파일에 아래 메타 데이터 태그를 추가합니다.
``` kotlin
<meta-data android:name="WiseTrackerLogState" android:value="true" />
// 개발용 테스트 앱에는 true로, 배포용 앱에는 false로 설정
```
