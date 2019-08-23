# Wisetracker In-App Events Documentation
When some issues occur while you're adding Wisetracker's code, submit those issues with specific information - logs, code snippets and etc. - to John Jeong(humblejohn@wisetracker.co.kr).

# Table of Content
* [Events](./go2joy.md#Events)
	* [Log In](./go2joy.md#Log-In)
		* [Note](./go2joy.md#Note)
		* [Code](./go2joy.md#Code)
		* [Example](./go2joy.md#Example)
	* [Sign-up](./go2joy.md#Sign-up)
		* [Note](./go2joy.md#Note-1)
		* [Code](./go2joy.md#Code-1)
		* [Example](./go2joy.md#Example-1)
	* [Search](./go2joy.md#Search)
		* [Note](./go2joy.md#Note-2)
		* [Code](./go2joy.md#Code-2)
		* [Example](./go2joy.md#Example-2)
	* [Reading Reviews](./go2joy.md#Reading-Reviews)
		* [Note](./go2joy.md#Note-3)
		* [Code](./go2joy.md#Code-3)
		* [Example](./go2joy.md#Example-3)
	* [Reached Booking Page](./go2joy.md#Reached-Booking-Page)
		* [Note](./go2joy.md#Note-4)
		* [Code](./go2joy.md#Code-4)
		* [Example](./go2joy.md#Example-4)
	* [Initiated Booking](./go2joy.md#Initiated-Booking)
		* [Note](./go2joy.md#Note-5)
		* [Code](./go2joy.md#Code-5)
		* [Example](./go2joy.md#Example-5)
	* [Completed Booking](./go2joy.md#Completed-Booking)
		* [Note](./go2joy.md#Note-6)
		* [Code](./go2joy.md#Code-6)
		* [Example](./go2joy.md#Example-6)
	* [Page Identity](./go2joy.md#Page-Identity)
		* [Note](./go2joy.md#Note-7)
		* [Code](./go2joy.md#Code-7)
		* [Example](./go2joy.md#Example-7)
* [After Implementation](./go2joy.md#After-Implementation)
	* [AOS](./go2joy.md#AOS)
	* [iOS](./go2joy.md#iOS)

# Events

### Log In
By adding code below, you cannot only record how many users log in to but also know your user's demographic information.

#### Note
1) This event must be triggered when users log in sucseccfully including 'Auto Log in'.
2) Must check below tables to pass `gender code`, `age code` & `province ID` values.

Gender | Gender Code
-------- | --------
Male | M
Female | F
except the above | U

Age | Age Code
-------- | --------
0 - 10 | A
11 - 19 | B
20 - 29 | C
30 - 39 | D
40 - 49 | E
50 - 59 | F
60 - 69 | G
70 -  | H

Province | Province ID
-------- | --------
Hồ Chí Minh | 1
Hà Nội | 2
Hà Giang | 3
Cao Bằng | 4
Bắc Kạn	| 5
Tuyên Quang	| 6
Lào Cai	| 7
Điện Biên | 8
Lai Châu | 9
Sơn La | 10
Yên Bái	| 11
Hoà Bình | 12
Thái Nguyên | 13
Lạng Sơn | 14
Quảng Ninh | 15
Bắc Giang | 16
Phú Thọ | 17
Vĩnh Phúc | 18
Bắc Ninh | 19
Hải Dương | 20
Hải Phòng | 21
Hưng Yên | 22
Thái Bình | 23
Hà Nam | 24
Nam Định | 25
Ninh Bình | 26
Thanh Hóa | 27
Nghệ An | 28
Hà Tĩnh | 29
Quảng Bình | 30
Quảng Trị | 31
Thừa Thiên Huế | 32
Đà Nẵng | 33
Quảng Nam | 34
Quảng Ngãi | 35
Bình Định | 36
Phú Yên | 37
Khánh Hòa | 38
Ninh Thuận | 39
Bình Thuận | 40
Kon Tum | 41
Gia Lai | 42
Đắk Lắk | 43
Đắk Nông | 44
Lâm Đồng | 45
Bình Phước | 46
Tây Ninh | 47
Bình Dương | 48
Đồng Nai | 49
Bà Rịa - Vũng Tàu | 50
Long An | 51
Tiền Giang | 52
Bến Tre | 53
Trà Vinh | 54
Vĩnh Long | 55
Đồng Tháp | 56
An Giang | 57
Kiên Giang | 58
Cần Thơ | 59
Hậu Giang | 60
Sóc Trăng | 61
Bạc Liêu | 62
Cà Mau | 63

#### Code
Android
``` kotlin
WiseTracker.setPageIdentity("LIR");
WiseTracker.setGoal("g2", 1);
WiseTracker.setGender("gender code");
WiseTracker.setAge("age code");
WiseTracker.setUserAttribute("uvp1", "province ID");
WiseTracker.sendTransaction();
```

iOS - Objective-C
``` objc
[WiseTracker setPageIdentity:@"LIR"];
[WiseTracker setGoal:@"g2" value: 1];
[WiseTracker setGender:@"gender code"];
[WiseTracker setAge:@"age code"];
[WiseTracker setUserAttribute:@"uvp1" name:"province ID"];
[WiseTracker sendTransaction];
```

iOS - Swift
``` swift
WiseTracker.setPageIdentity("LIR")
WiseTracker.setGoal("g2", 1)
WiseTracker.setGender("gender code")
WiseTracker.setAge("age code")
WiseTracker.setUserAttribute("uvp1", "province ID")
WiseTracker.sendTransaction()
```

#### Example
If a 35 years old Male user from Bình Thuận logs in, following lines must be executed.

Android
``` kotlin
WiseTracker.setPageIdentity("LIR");
WiseTracker.setGoal("g2", 1);
WiseTracker.setGender("M");
WiseTracker.setAge("D");
WiseTracker.setUserAttribute("uvp1", "40");
WiseTracker.sendTransaction();
```

iOS - Objective-C
``` objc
[WiseTracker setPageIdentity:@"LIR"];
[WiseTracker setGoal:@"g2" value: 1];
[WiseTracker setGender:@"gender code"];
[WiseTracker setAge:@"age code"];
[WiseTracker setUserAttribute:@"uvp1" name:"40"];
[WiseTracker sendTransaction];
```

iOS - Swift
``` swift
WiseTracker.setPageIdentity("LIR")
WiseTracker.setGoal("g2", 1)
WiseTracker.setGender("M")
WiseTracker.setAge("D")
WiseTracker.setUserAttribute("uvp1", "40")
WiseTracker.sendTransaction()
```

### Sign-up
You can record how many users sign-up via your app.

#### Note
This event should be triggered when users complete sign-up process. Therefore, adding following lines in 'Sign-up Complete Page' is one of good ways to implement. 

#### Code
Android
``` kotlin
WiseTracker.setPageIdentity("RGR");
WiseTracker.setGoal("g1", 1);
WiseTracker.sendTransaction();
```

iOS - Objective-C
``` objc
[WiseTracker setPageIdentity:@"RGR"];
[WiseTracker setGoal:@"g1" value: 1];
[WiseTracker sendTransaction];
```

iOS - Swift
``` swift
WiseTracker.setPageIdentity("RGR")
WiseTracker.setGoal("g1", 1)
WiseTracker.sendTransaction()
```

### Search
By recording this event you can record how many times each keywords are searched by users.

#### Note
This event should be triggered when search results come out on the page.

#### Code
Android
``` kotlin
WiseTracker.setSearchKeyword("keyword");
WiseTracker.setSearchKeywordResult(number of items);
WiseTracker.setPageIdentity("SEARCH");
```

iOS - Objective-C
``` objc
[WiseTracker setSearchKeyword:@"keyword"];
[WiseTracker setSearchKeywordResult:@number of items];
[WiseTracker setPageIdentity:@"SEARCH"];
```

iOS - Swift
``` swift
WiseTracker.setSearchKeyword("keyword")
WiseTracker.setSearchKeywordResult(number of items)
WiseTracker.setPageIdentity("SEARCH")
```

#### Example
If the user searches "hanoi" then 19 hotels come out as a result, following lines must be executed.

Android
``` kotlin
WiseTracker.setSearchKeyword("hanoi");
WiseTracker.setSearchKeywordResult(19);
WiseTracker.setPageIdentity("SEARCH");
```

iOS - Objective-C
``` objc
[WiseTracker setSearchKeyword:@"hanoi"];
[WiseTracker setSearchKeywordResult:@19];
[WiseTracker setPageIdentity:@"SEARCH"];
```

iOS - Swift
``` swift
WiseTracker.setSearchKeyword("hanoi")
WiseTracker.setSearchKeywordResult(19)
WiseTracker.setPageIdentity("SEARCH")
```

### Reading Reviews
You can record what hotel's review is read by users.

#### Note
1) This event must be triggered when 'Reading Reviews' button is clicked. Theirfore, we recommend you to add following lines on 'click event' of the button.
2) There are two 'Reading Reviews' buttons in Hotel Detail Page. Make sure to add following lines to those two buttons.
![buttons](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/Untitled-1.jpg)

#### Code
Android
``` kotlin
WiseTracker.setGoalProduct("hotel code");
WiseTracker.setGoal("g10", 1);
WiseTracker.sendGoalData();
```

iOS - Objective-C
``` objc
[WiseTracker setGoalProduct:@"hotel code"];
[WiseTracker setGoal:@"g10" value: 1];
[WiseTracker sendGoalData];
```

iOS - Swift
``` swift
WiseTracker.setGoalProduct("hotel code")
WiseTracker.setGoal("g10", 1)
WiseTracker.sendGoalData()
```

### Reached Booking Page
Reached Booking Page

#### Note
1) This event must be triggered when the user successfully reaches 'Booking' page.
2) Thus, this code must not be executed in such cases as shown below.
![case](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/Untitled-2.jpg)

#### Code
Android
``` kotlin
WiseTracker.setGoalProduct("hotel code");
WiseTracker.setGoalProduct("hotel code");
WiseTracker.setGoalProduct("hotel code");
WiseTracker.setGoal("g11", 1);
WiseTracker.sendGoalData();
```

iOS - Objective-C
``` objc
[WiseTracker.setGoalProduct:@"hotel code"];
[WiseTracker.setGoalProduct:@"hotel code"];
[WiseTracker.setGoalProduct:@"hotel code"];
[WiseTracker setGoal:@"g11" value: 1];
[WiseTracker sendGoalData];
```

iOS - Swift
``` swift
WiseTracker.setGoalProduct("hotel code")
WiseTracker.setGoalProduct("hotel code")
WiseTracker.setGoalProduct("hotel code")
WiseTracker.setGoal("g11", 1)
WiseTracker.sendGoalData()
```

#### Example
If the user reaches booking page of A-IN HOTEL TRUNG SON's Standard Room, following lines must be executed.

Android
``` kotlin
WiseTracker.setGoalProduct("hotel code");
WiseTracker.setGoalProduct("hotel code");
WiseTracker.setGoalProduct("hotel code");
WiseTracker.setGoal("g11", 1);
WiseTracker.sendGoalData();
```

iOS - Objective-C
``` objc
[WiseTracker.setGoalProduct:@"hotel code"];
[WiseTracker.setGoalProduct:@"hotel code"];
[WiseTracker.setGoalProduct:@"hotel code"];
[WiseTracker setGoal:@"g11" value: 1];
[WiseTracker sendGoalData];
```

iOS - Swift
``` swift
WiseTracker.setGoalProduct("hotel code")
WiseTracker.setGoalProduct("hotel code")
WiseTracker.setGoalProduct("hotel code")
WiseTracker.setGoal("g11", 1)
WiseTracker.sendGoalData()
```

### Initiated Booking
You can record how many times start to booking process in each hotels.

#### Note
1) This event must be triggered when the user successfully reaches 'Billing Information' page only by clicks 'Book now!' button in [this page](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/room-type.jpg).
2) Thus, this code must not be executed in such cases as shown below.
![case](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/Untitled-2.jpg)

#### Code
Android
``` kotlin
WiseTracker.setGoalProduct("hotel code");
WiseTracker.setGoalProduct("hotel code");
WiseTracker.setGoalProduct("hotel code");
WiseTracker.setGoal("g12", 1);
WiseTracker.sendGoalData();
```

iOS - Objective-C
``` objc
[WiseTracker setGoalProduct:@"hotel code"];
[WiseTracker setGoalProduct:@"hotel code"];
[WiseTracker setGoalProduct:@"hotel code"];
[WiseTracker setGoal:@"g12" value: 1];
[WiseTracker sendGoalData];
```

iOS - Swift
``` swift
WiseTracker.setGoalProduct("hotel code")
WiseTracker.setGoalProduct("hotel code")
WiseTracker.setGoalProduct("hotel code")
WiseTracker.setGoal("g12", 1)
WiseTracker.sendGoalData()
```

#### Example
If the user initiated hourly booking for A-IN HOTEL TRUNG SON's Standard Room, following lines must be executed.

Android
``` kotlin
WiseTracker.setGoalProduct("hotel code");
WiseTracker.setGoalProduct("hotel code");
WiseTracker.setGoalProduct("hotel code");
WiseTracker.setGoal("g12", 1);
WiseTracker.sendGoalData();
```

iOS - Objective-C
``` objc
[WiseTracker.setGoalProduct:@"hotel code"];
[WiseTracker.setGoalProduct:@"hotel code"];
[WiseTracker.setGoalProduct:@"hotel code"];
[WiseTracker setGoal:@"g12" value: 1];
[WiseTracker sendGoalData];
```

iOS - Swift
``` swift
WiseTracker.setGoalProduct("hotel code")
WiseTracker.setGoalProduct("hotel code")
WiseTracker.setGoalProduct("hotel code")
WiseTracker.setGoal("g12", 1)
WiseTracker.sendGoalData()
```

### Completed Booking
You can record how many times start to booking process in each hotels.

#### Note
1) This event must be triggered when the user successfully reaches 'Billing Information' page only by clicks 'Book now!' button in [this page](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/room-type.jpg).
2) Thus, this code must not be executed in such cases as shown below.
![case](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/Untitled-2.jpg)

#### Code
Android
``` kotlin
WiseTracker.setOrderProductArray(["hotel code"]);
WiseTracker.setOrderProductArray(["hotel code"]);
WiseTracker.setOrderProductArray(["hotel code"]);
WiseTracker.setOrderQuantityArray([number of items purchased]);
WiseTracker.setOrderAmountArray([money that user actually paid]);
WiseTracker.setOrderNo("order No or ID");
WiseTracker.setPageIdentity("ODR");
WiseTracker.sendTransaction();
```

iOS - Objective-C
``` objc
[WiseTracker setOrderProductArray:@[@"hotel code"]];
[WiseTracker setOrderProductArray:@[@"hotel code"]];
[WiseTracker setOrderProductArray:@[@"hotel code"]];
[WiseTracker setOrderQuantityArray:@[@number of items purchased]];
[WiseTracker setOrderAmountArray:@[@money that user actually paid]]; //구매자가 실제 지불해야 하는 금액
[WiseTracker setOrderNo:@"order No or ID"];
[WiseTracker setPageIdentity:@"ODR"];
[WiseTracker sendTransaction];
```

iOS - Swift
``` swift
WiseTracker.setOrderProductArray(["hotel code"])
WiseTracker.setOrderProductArray(["hotel code"])
WiseTracker.setOrderProductArray(["hotel code"])
WiseTracker.setOrderQuantityArray([number of items purchased])
WiseTracker.setOrderAmountArray([money that user actually paid])
WiseTracker.setOrderNo("order No or ID")
WiseTracker.setPageIdentity("ODR")
WiseTracker.sendTransaction()
```

#### Example
If the user searches "hanoi" then 19 hotels come out as a result, following lines must be executed.

Android
``` kotlin
WiseTracker.setOrderProductArray(["hotel code"]);
WiseTracker.setOrderProductArray(["hotel code"]);
WiseTracker.setOrderProductArray(["hotel code"]);
WiseTracker.setOrderQuantityArray([number of items purchased]);
WiseTracker.setOrderAmountArray([money that user actually paid]);
WiseTracker.setOrderNo("order No or ID");
WiseTracker.setPageIdentity("ODR");
WiseTracker.sendTransaction();
```

iOS - Objective-C
``` objc
[WiseTracker setOrderProductArray:@[@"hotel code"]];
[WiseTracker setOrderProductArray:@[@"hotel code"]];
[WiseTracker setOrderProductArray:@[@"hotel code"]];
[WiseTracker setOrderQuantityArray:@[@number of items purchased]];
[WiseTracker setOrderAmountArray:@[@money that user actually paid]]; //구매자가 실제 지불해야 하는 금액
[WiseTracker setOrderNo:@"order No or ID"];
[WiseTracker setPageIdentity:@"ODR"];
[WiseTracker sendTransaction];
```

iOS - Swift
``` swift
WiseTracker.setOrderProductArray(["hotel code"])
WiseTracker.setOrderProductArray(["hotel code"])
WiseTracker.setOrderProductArray(["hotel code"])
WiseTracker.setOrderQuantityArray([number of items purchased])
WiseTracker.setOrderAmountArray([money that user actually paid])
WiseTracker.setOrderNo("order No or ID")
WiseTracker.setPageIdentity("ODR")
WiseTracker.sendTransaction()
```

### Page Identity
You can record pageview and duration for each page.

#### Note
1) Adding following lines in each page.
2) Must check a below table to pass `page code` value.

Page Name | Page Code | Image
-------- | -------- | --------
Main | MAIN | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/main.jpg)
My Instant Booking | INSTBOOK | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/my-instant-booking.jpg)
Map | MAP | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/map.jpg)
Filter | FILTER | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/filter.jpg)
Choose Area | AREA | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/choose-area.jpg)
Login | LOGIN | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/login.jpg)
Email Sign-up | SU00 | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/signup000.jpg)
Member Profile | SU01 | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/signup001-member-profile.jpg)
Hotel Detail | PDV | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/review00-hotel-detail.jpg)
Room Detail | ROOMDT | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/room-detail.jpg)
Booking | BOOKING | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/room-type.jpg)
Billing Information | BILLING | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/billing-info.jpg)
Payment Method | PAYMENT | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/payment-method.jpg)
Booking Complete | ODR | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/complete-checkout.jpg)
Promotion List | PROMOLST | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/promotion-list.jpg)
Promotion Detail | PROMODT | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/promotion-detail.jpg)
Event List | EVTLST | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/event-list.jpg)
Event Detail | EVTDT | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/event-detail.jpg)
My Page | MYPAGE | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/my-page.jpg)
Account Setting | ACCOUNT | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/account-setting.jpg)
My Coupon | COUPON | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/coupon.jpg)
My Point | POINT | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/point.jpg)
Notification Setting | NOTI | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/noti-setting.jpg)
Q&A | QNA | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/qna.jpg)
Write a Question | INQUIRY | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/write-a-question.jpg)
Notice | NOTICE | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/notice.jpg)
My Favorite | MYFAV | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/my-favourite.jpg)
My Booking | MYBOOK | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/my-booking.jpg)
Invite Friend | INVITE | [Link](http://www.wisetracker.co.kr/wp-content/uploads/2019/08/intive-friends.jpg)

#### Code
Android
``` kotlin
WiseTracker.setPageIdentity("page code");
```

iOS - Objective-C
``` objc
[WiseTracker setPageIdentity:@"page code"];
```

iOS - Swift
``` swift
WiseTracker.setPageIdentity("page code")
```

#### Example
If the user successfully landed in 'Payment Method' page, following line must be executed.

Android
``` kotlin
WiseTracker.setPageIdentity("PAYMENT");
```

iOS - Objective-C
``` objc
[WiseTracker setPageIdentity:@"PAYMENT"];
```

iOS - Swift
``` swift
WiseTracker.setPageIdentity("PAYMENT")
```

## After Implementation
Please send us testing app debug mode is enabled. You can enable debug mode by adding configuration below. Then we will test that whether those In-App Events are well implemented.

### AOS
Add following lines to AndroidManifest.xml file.
``` kotlin
<meta-data android:name="WiseTrackerLogState" android:value="true" />
// set true for testing, set false for distributing
```

### iOS
Set following value to Info.plist file.

![iOS Debug Mobe](http://www.wisetracker.co.kr/wp-content/uploads/2019/05/ios-debug.png)

``` swift
<key>WiseTrackerLogState</key>
<string>true</string>
```
