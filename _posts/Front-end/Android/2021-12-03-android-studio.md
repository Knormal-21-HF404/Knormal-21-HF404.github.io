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

<center><img src="/assets/images/android1.jpg" width="200" height="300">로그인 <img src="/assets/images/android2.jpg" width="200" height="300">회원가입</center>

아이디와 비밀번호를 입력한 후 로그인을 하면 메인 페이지로 이동합니다.

<br>

## 2️⃣ 메인
"그냥 담아" 메인 페이지에서는 다양한 서비스가 연결되어 있습니다.
- 장바구니 서비스
- 마이페이지
- 검색 서비스
- 체크리스트 확인
- 물품별 카테고리 확인
- 이벤트
- QR

<center><img src="/assets/images/android13.png" width="200" height="300"></center>메인

<br>

## 3️⃣ 장바구니
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

<center><img src="/assets/images/android7.jpg" width="200" height="300"></center> 장바구니
