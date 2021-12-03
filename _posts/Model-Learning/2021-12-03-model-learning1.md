---
title: "데이터 수집하기"
categories:
  - Model-Learning
toc: true
toc_sticky: true
toc_label: 목차
description: JAVA를 공부하는 데 있어 기본이 되는 JVM이 무엇인지 학습하고, JVM의 메모리 구조와 Garbage collector,
  Execution Engine, Class Loader에 대한 기본적인 설명 등 JVM이 어떻게 돌아가는지에 대한 기초를 잡는 게시물
---

## Step 1: 데이터 수집하기 
작품의 인식정확도를  높이기 위해 데이터를 수집합니다.

### ① Video to JPG Converter
데이터를 수집하기 위해서 티처블머신(Teachable Machine)을 이용해 진행하였습니다.

![label1](/assets/images/label1.png)
![label2](/assets/images/label2.png)
<br>
Teachable Machine에 들어간 뒤 Image Project를 누르면 오른쪽 사진처럼 웹캠이 켜지는 것을 볼 수 있다. 
Hold to Record를 누르는 동안 연사가 찍힌다. class 옆에 점세개를 누르고 Download Samples를 누르면 수집한 데이터 사진들을 다운할 수 있다. <br><br>

### ② 동영상을 JPG로 변환
동영상파일을 프레임별로 잘라 사진 파일로 내보내주는 툴도 사용해 진행해 보았습니다.

 <br>**참고링크**
-- [https://dzone.com/articles/jvm-architecture-explained]({{"https://dzone.com/articles/jvm-architecture-explained"}}){:target="_blank"} <br>
{: .notice--info}

Frames for video를 설정한 값에 따라 영상에서 원하는 frame 수만큼 이미지를 잘라 저장합니다.  
이미지를 추출하면 다음과 같이 학습데이터 이미지 파일을 수집할 수 있습니다.
![label3](/assets/images/label3.png)


## Step 2: 데이터 라벨링
데이터를 다 수집한 후 

IoT센서는 카메라, 무게센서, 비콘을 사용합니다.  

IoT플랫폼을 통해서 센서정보를 수집하고 머신러닝 기술을 이용하여 분석합니다.  
IoT플랫폼에서의 판단결과를 바탕으로 물품 플랫폼에서 데이터베이스가 업데이트 됩니다.  

### Service 부분에서는 Application을 통해 여러 정보를 확인할 수 있습니다.

