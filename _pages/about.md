---
permalink: /about/
title: "About the project"
layout: archive
author_profile: true
sidebar_main: true
---

Just Cart Out(그냥 담아)은 딥러닝 기반 스마트 카트 서비스입니다.  
"그냥 담아" 서비스는 쇼핑 카트에 물건을 담으면 자동으로 물건을 인식해 결제금액을 계산해주고 매장 출구로 나가는 순간, 자동으로 결제해주는 편리한 쇼핑 시스템입니다.

---
---
## __Primary Function__
- AI를 활용한 장바구니 자동 업데이트
- 자동결제 서비스
- 연관 상품 추천 서비스
- 신선도 알림 서비스

## __How to use__
#### AI를 활용한 장바구니 자동 업데이트
  1) 라즈베리파이에서 서버에 소켓연결 요청을 합니다.  
  2) 연결시 서버와 스마트폰에 연결됩니다.  
  3) 카메라를 통해 물품이 인식되면 물품의 영상정보와 무게 센서를 통해 무게정보를 서버로 전달합니다.  
  4) 서버에서 전달된 물체를 인식하고 측정무게와 인식된 물체의 무게를 비교해 물체를 최종 판단합니다.  
  5) 판단된 물체는 데이터베이스에 업데이트되며 안드로이드 앱에서 확인 가능합니다.  

#### 자동결제 서비스
1) 스마트폰과 라즈베리파이가 연결된 상태에서 특정 비콘에 접근합니다.  
2) 비콘 반경에 진입시 자동으로 결제가 됩니다.  

#### 연관 상품 추천 서비스
1) 어플리케이션에서 구매희망 상품을 검색합니다.  
2) 구매희망 상품과 함께 관련 연관 상품을 추천합니다.  

#### 신선도 알림 서비스
1) 스마트폰과 라즈베리파이가 연결된 상태에서 특정 비콘에 접근합니다.  
2) 비콘 반경에 진입시 주변 신선식품의 정보를 제공 받습니다.  

---
---

## __Installation__
### Raspberry Pi 4 Model B
##### SW

Spec : 8GB RAM

Installation Libaray 
-  OpenCV 4.5.1
-  Numpy(1.13.3)
-  Socket Library

##### HW
Construction Equipment
-  PI Camera(8MP Sony IMX219)
-  Multi Camera Adaptor
-  Road Cell(HX711)
-  Battery Pack(EB-p3300)
-  7inchs Screen

<br/>

---
### AWS Server
##### SW

Platform : Ubuntu 18.04 (Deep Learning AMI)

Instance Spec : g4dn.xlarge (4 vCPUs / 16GiB / 125GB ssd)

Installation Libaray 
-  OpenCV 4.5.1
-  Numpy(1.13.3)
-  Socket Library
-  Darknet
-  PHP(7.1.33)
-  MySQL(5.7.29)
-  Apache(2.4.43)

<br/>

---

### SmartPhone Application
##### SW
Platform : Android OS(11)

Tool : Android Studio (1.2.2)

Installation Libaray
-  Beacon SDK(iBeacon E7 SDK)

##### HW
Construction Equipment
-  Beacon (iBeacon E7)

<br/>

---

---
