---
title: Android Studio Application1
categories:
- Android
tags:
  - [Frontend, Android]
toc: true
toc_sticky: true
---

## 1️⃣ 로그인 & 회원가입
안드로이드 앱 "그냥 담아"를 사용하기 위해서는 사용자가 로그인&회원가입을 먼저 하고 넘어가도록 구성하였습니다.

<center><img src="/assets/images/android1.jpg" width="200" height="300"> <img src="/assets/images/android2.jpg" width="200" height="300"></center>
<center>로그인 & 회원가입</center>

아이디와 비밀번호를 입력한 후 로그인을 하면 메인 페이지로 이동합니다.

<br>

## 2️⃣ 메인
"그냥 담아" 메인 페이지에서는 다양한 서비스가 연결되어 있습니다.
- QR 서비스
- 검색 서비스
- 물품 추천 서비스
- 체크리스트 확인
- 장바구니
- 신선도 서비스
- 자동결제
- 물품별 카테고리 확인
- 이벤트

<center><img src="/assets/images/android13.png" width="200" height="300"></center>
<center>메인</center>

<br>

## 3️⃣ QR 코드
QR코드는 카트에 qr코드를 인식하면 유저아이디를 통해 최신 주문번호를 받아옵니다.

① QR코드는 바코드 스캐닝 오픈소스 (ZXing Android Embedded)를 사용해 구성합니다.

② 카트에 qr 코드를 인식하면 데이터베이스에 유저아이디를 업데이트합니다.

<center><img src="/assets/images/android3.jpg" width="200" height="300"></center>
<center>QR코드</center>

③ 안드로이드 코드에 유저아이디를 php파일에 전달해 아이디가 일치하면 최신 주문번호를 받아옵니다.
```php
	@Override
  public void onBackPressed() {
  super.onBackPressed();
  showResult2(USER_ID);
  mArrayList = new ArrayList<>(); 
  finish();
  }
    ...

````

<br>


## 4️⃣ 물품 검색 및 추천
물품을 검색하면 데이터베이스에서 물품정보와 추천정보를 가져옵니다.

① 물품을 검색하면 검색값을 받아와 php파일에 전달합니다.  
```java
//검색 버튼을 클릭 시 수행
button_search.setOnClickListener(new View.OnClickListener() {
public void onClick(View v) {
mArrayList.clear();
GetData task = new GetData();
task.execute(mEditTextSearchKeyword.getText().toString());
}
});

````

② 검색값을 데이터베이스의 'SHOPBASKET' 테이블과 비교 후 물품 상세정보를 출력합니다.
물품과 관련된 상품도 추천해 같이 출력해 사용자가 확인할 수 있습니다.

<center><img src="/assets/images/android9.jpg" width="200" height="300"> <img src="/assets/images/android10.jpg" width="200" height="300"></center>
<center>검색화면 & 추천화면</center>

③ 안드로이드 코드에 유저아이디를 php파일에 전달해 아이디가 일치하면 최신 주문번호를 받아옵니다.  
```php
	@Override
  public void onBackPressed() {
  super.onBackPressed();
  showResult2(USER_ID);
  mArrayList = new ArrayList<>(); 
  finish();
  }
    ...

````

<br>

## 5️⃣ 체크리스트
앞서 설명했던 검색기능을 사용한 후 옆에 있는 찜버튼을 누를 경우 체크리스트에 추가됩니다.

① 사용자가 검색 결과 출력된 상품에 찜 버튼을 누릅니다.

② 검색한 물품이름, 유저아이디, 주문번호를 php 파일에 전달합니다.
```java
CheckRequest checkRequest = new CheckRequest(USER_ID, ORDER_ID, Name, responseListener);
RequestQueue queue = Volley.newRequestQueue(SearchActivity.this);
queue.add(checkRequest);

````

③ 전달받은 데이터는 데이터베이스 체크리스트 항목에 삽입해 체크리스트를 생성합니다.

<center><img src="/assets/images/android6.jpg" width="200" height="300"></center>
<center>체크리스트</center>

<br>

## 6️⃣ 장바구니
스마트 카트에 구매할 상품을 넣으면 상품의 종류를 인식해 장바구니 앱에 출력됩니다. 

userID와 주문번호를 이용하여 사용자의 장바구니를 가져옵니다.

① 안드로이드 코드에서 유저아이디와 주문번호 php 파일에 전달합니다.

```java
USER_ID = SharedPreference.getUserID(ShopActivity2.this);  
ORDER_ID = SharedPreference.getOrderID(ShopActivity2.this;

String serverURL = "http://3.37.3.112/Load_userbasket.php";
String postParameters = "&userID=" + searchKeyword1 +"&order_id=" + searchKeyword2

````

② php 파일에서 유저아이디와 주문번호가 일치하는 장바구니 정보를 받아옵니다.

```php
	//POST 값을 읽어온다.
	$userID = isset($_POST['userID']) ? $_POST['userID'] : ''; //이름값 가져옴
	$order_id = isset($_POST['order_id']) ? $_POST['order_id'] : ''; //이름값 가져옴
	$android = strpos($_SERVER['HTTP_USER_AGENT'], "Android");

	if ($userID != "" ){ 

    $sql="select productName, productPrice, classNum from USERBASKET where userID='$userID' and order_id='$order_id'";
    $stmt = $con->prepare($sql);
    $stmt->execute();
    ...

````

③ 안드로이드 코드에서 장바구니에 물건이 들어올 때마다 총액을 계산할 수 있는 총액 계산 코드를 추가합니다.

```java
a += Integer.parseInt(productPrice,10)*Integer.parseInt(classNum,10);

````

④ 마지막으로 장바구니에 항목이 추가될 때마다 자동으로 리스트가 업데이트 되도록 구성합니다.

```java
mCustomRunnable = new CustomRunnable();
handler = new Handler();
runnable1 = new ProgressRunnable();

````
```java
if(info.get(0).topActivity.getClassName().equals("com.example.JustCart_ver4.ShopActivity2")){
handler.post(runnable1);}

````

<center><img src="/assets/images/android7.jpg" width="200" height="300"></center>
<center>장바구니</center>

<br>

## 7️⃣ 신선도 체크 & 자동결제
신선도 체크와 자동결제는 비콘인식 오픈소스를 사용해 구성합니다.

① 비콘을 사용하여 사용자가 가까이 왔을 때 실행되도록 합니다.

#### 자동결제
```java
// 자동결제
((Beacon) beacons.iterator().next()).getDistance() < 0.5 && minor == 55155

beaconManager.startRangingBeacons(new Region("AC:23:3F:7E:09:8C", null, null, null));

````
👉비콘과의 거리가 0.5m 안이고 매장출구 비콘을 인식했을 시 자동결제 됩니다.

#### 신선도 
```java
// 신선도알림
((Beacon) beacons.iterator().next()).getDistance() < 0.5 && minor == 55024

beaconManager.startRangingBeacons(new Region("AC:23:3F:7E:09:09", null, null, null));

````
👉비콘과의 거리가 0.5m 안이고 신선식품 매대 비콘을 인식했을 시에 신선도알림이 울립니다.

<center><img src="/assets/images/android8.jpg" width="200" height="300"></center>
<center>신선도알림</center>


