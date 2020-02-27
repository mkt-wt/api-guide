# Wisetracker Integration Guide
'리턴: 방치형RPG' 게임의 Android 앱에 연동할 와이즈트래커 인앱 이벤트를 안내하는 문서입니다.

# Index
* [캐릭터 생성](./return.md#캐릭터-생성)
* [로그인](./return.md#로그인)
	* [주의사항](./return.md#주의사항)
* [출석완료](./return.md#출석완료)
	* [적용예시](./return.md#적용예시)
* [레벨업](./return.md#레벨업)
	* [적용예시](./return.md#적용예시-1)
* [캐릭터 사망](./return.md#캐릭터-사망)
	* [적용예시](./return.md#적용예시-2)
* [인앱구매](./return.md#인앱구매)
	* [주의사항](./return.md#주의사항-1)
	* [적용예시](./return.md#적용예시-3)
* [광고시청](./return.md#광고시청)
* [던전 입장](./return.md#던전-입장)
	* [주의사항](./return.md#주의사항-2)
* [비밀의 탑 입장](./return.md#비밀의-탑-입장)
	* [적용예시](./return.md#적용예시-4)
* [아레나 결투 완료](./return.md#아레나-결투-완료)
	* [적용예시](./return.md#적용예시-5)
* [아이템 레벨업](./return.md#아이템-레벨업)
* [아이템 승급](./return.md#아이템-승급)
* [아이템 강화](./return.md#아이템-강화)
* [아이템 각인](./return.md#아이템-각인)
* [아이템 세공](./return.md#아이템-세공)
* [적용 후 데이터 검증](./return.md#적용-후-데이터-검증)
	* [AOS](./return.md#AOS)


## 캐릭터 생성
유저가 캐릭터에 이름을 부여하여 캐릭터 생성이 완료된 시점에 아래 코드를 추가합니다.
``` kotlin
// 캐릭터 이름이 결정됨
WiseTracker.setPageIdentity("RGR");
WiseTracker.setGoal("g1", 1);
WiseTracker.sendTransaction();
```

## 로그인
유저가 앱을 실행하여 정상적으로 로그인 완료된 시점에 아래 코드를 추가합니다.

### 주의사항
'리턴: 방치형RPG'의 경우 구글 게임 계정으로 자동 로그인됩니다. 이렇게 자동 로그인 될때마다 아래 코드가 동작하도록 설정해야 합니다. 
``` kotlin
// 로그인 완료 처리
WiseTracker.setPageIdentity("LIR");
WiseTracker.setGoal("g2", 1);
WiseTracker.sendTransaction();
```

## 출석완료
유저가 출석체크를 완료하여 아이템을 수령한 시점에 아래 코드를 추가합니다.
``` kotlin
// 출석 완료
WiseTracker.setUserAttribute( "uvp1", "현재 캐릭터 레벨" );
WiseTracker.setPageIdentity("GETON");
WiseTracker.setGoal("g3", 1);
WiseTracker.sendTransaction();
```

### 적용예시
레벨 20인 유저가 출석체크 완료
``` kotlin
// 출석 완료
WiseTracker.setUserAttribute( "uvp1", "20" );
WiseTracker.setPageIdentity("GETON");
WiseTracker.setGoal("g3", 1);
WiseTracker.sendTransaction();
```

## 레벨업
캐릭터의 레벨이 상승한 시점에 아래 코드를 추가합니다.
``` kotlin
// 레벨 상승
WiseTracker.setUserAttribute( "uvp1", "달성한 캐릭터 레벨" );
WiseTracker.setPageIdentity("LEVUP");
WiseTracker.setGoal("g4", 1);
WiseTracker.sendTransaction();
```

### 적용예시
캐릭터의 레벨이 24에서 25로 상승한 경우, 상승 시점에 아래 코드 추가
``` kotlin
// 레벨 25로 상승
WiseTracker.setUserAttribute( "uvp1", "25" );
WiseTracker.setPageIdentity("LEVUP");
WiseTracker.setGoal("g4", 1);
WiseTracker.sendTransaction();
```

## 캐릭터 사망
캐릭터가 사냥터에서 사망한 시점에 아래 코드를 추가합니다. PvP에서 사망 시에는 본 코드를 적용하지 않습니다.
``` kotlin
// 캐릭터 사망
WiseTracker.setUserAttribute( "uvp1", "현재 캐릭터 레벨" );
WiseTracker.setPageIdentity("DEATH");
WiseTracker.setGoal("g5", 1);
WiseTracker.sendTransaction();
```

### 적용예시
레벨이 45인 캐릭터가 사망한 경우
``` kotlin
// 캐릭터 사망
WiseTracker.setUserAttribute( "uvp1", "45" );
WiseTracker.setPageIdentity("DEATH");
WiseTracker.setGoal("g5", 1);
WiseTracker.sendTransaction();
```

## 인앱구매
유저가 유료 아이템을 결제한 경우가 인앱구매에 해당합니다. 인앱구매가 완료된 시점에 아래 코드를 추가합니다.

### 주의사항
1) 결제금액은 원화(KRW) 기준의 액수만을 사용해 주시기 바랍니다.
2) 게임머니(골드, 다이아몬드, 마일리지)를 사용하여 아이템을 구매한 경우에는 본 코드를 적용하지 않습니다. 오직 실제 화폐로 아이템을 구매한 경우에만 본 코드를 적용해주세요.
``` kotlin
// 인앱구매 완료
WiseTracker.setOrderProduct("상품코드");
WiseTracker.setOrderQuantity(상품수량);
WiseTracker.setOrderAmount(결제금액);
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
WiseTracker.setOrderAmount(5500); // KRW 기준 결제액 입력
WiseTracker.setOrderNo("O12345678");
WiseTracker.setPageIdentity("ODR");
WiseTracker.sendTransaction();
```

## 광고시청
유저가 광고시청을 완료하여 보상을 받은 시점에 아래 코드를 추가합니다.
``` kotlin
// 광고시청을 통해 보상 지급
WiseTracker.setPageIdentity("ADVIEW");
WiseTracker.setGoal("g6", 1);
WiseTracker.sendTransaction();
```

## 던전 입장
유저가 던전에 입장하는 이벤트에 아래 코드를 추가합니다.

### 주의사항
던전이란 요일 던전, 골드 던전, 경험치 던전만을 의미합니다. 비밀의 탑은 별도의 코드로 측정합니다.
``` kotlin
// 던전에 입장
WiseTracker.setUserAttribute( "uvp1", "현재 캐릭터 레벨" );
WiseTracker.setPageIdentity("DUNGEON");
WiseTracker.setGoal("g7", 1);
WiseTracker.sendTransaction();
```

## 비밀의 탑 입장
유저가 비밀의 탑에 입장하는 이벤트에 아래 코드를 추가합니다.
``` kotlin
// 비밀의 탑 입장
WiseTracker.setUserAttribute( "uvp1", "현재 캐릭터 레벨" );
WiseTracker.setUserAttribute( "uvp2", "입장한 비밀의 탑 층수" );
WiseTracker.setPageIdentity("TOWER");
WiseTracker.setGoal("g8", 1);
WiseTracker.sendTransaction();
```

### 적용예시
레벨 55인 캐릭터가 비밀의 탑 30층에 입장한 경우
``` kotlin
// 비밀의 탑 입장
WiseTracker.setUserAttribute( "uvp1", "55" );
WiseTracker.setUserAttribute( "uvp2", "30" );
WiseTracker.setPageIdentity("TOWER");
WiseTracker.setGoal("g8", 1);
WiseTracker.sendTransaction();
```

## 아레나 결투 완료
유저가 아레나에서 PvP를 완료하는 시점에 아래 코드를 추가합니다. 승패와 관련이 없으며 모든 PvP 완료에 대해서 본 코드가 추가 되는 개념입니다.
``` kotlin
// PvP 완료
WiseTracker.setUserAttribute( "uvp1", "현재 레벨" );
WiseTracker.setPageIdentity("ARENA");
WiseTracker.setGoal("g9", 1);
WiseTracker.sendTransaction();
```

### 적용예시
레벨 120인 유저가 아레나에서 PvP를 완료한 경우
``` kotlin
// PvP 완료
WiseTracker.setUserAttribute( "uvp1", "120" );
WiseTracker.setPageIdentity("ARENA");
WiseTracker.setGoal("g9", 1);
WiseTracker.sendTransaction();
```

## 아이템 레벨업
유저가 아이템의 레벨엡에 성공한 시점에 아래 코드를 추가합니다.
``` kotlin
// 아이템 레벨업 성공
WiseTracker.setPageIdentity("ITEM");
WiseTracker.setGoal("g10", 1);
WiseTracker.sendTransaction();
```

## 아이템 승급
유저가 아이템 승급에 성공한 시점에 아래 코드를 추가합니다.
``` kotlin
// 아이템 승급 성공
WiseTracker.setPageIdentity("ITEM");
WiseTracker.setGoal("g11", 1);
WiseTracker.sendTransaction();
```

## 아이템 강화
유저가 아이템 강화를 시도한 시점에 아래 코드를 추가합니다. 강화 성공/실패 여부와 관계 없이 시도 자체를 측정하는 개념입니다.
``` kotlin
// 아이템 강화 시도
WiseTracker.setPageIdentity("ITEM");
WiseTracker.setGoal("g12", 1);
WiseTracker.sendTransaction();
```

## 아이템 각인
유저가 아이템 각인에 성공한 시점에 아래 코드를 추가합니다.
``` kotlin
// 아이템 각인 성공
WiseTracker.setPageIdentity("ITEM");
WiseTracker.setGoal("g13", 1);
WiseTracker.sendTransaction();
```

## 아이템 세공
유저가 아이템 세공에 성공한 시점에 아래 코드를 추가합니다.
``` kotlin
// 아이템 세공 성공
WiseTracker.setPageIdentity("ITEM");
WiseTracker.setGoal("g14", 1);
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
