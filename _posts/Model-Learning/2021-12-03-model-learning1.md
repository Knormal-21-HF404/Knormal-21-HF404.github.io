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
-- [https://m.blog.naver.com/ferieo/220701158144]({{"https://m.blog.naver.com/ferieo/220701158144"}}){:target="_blank"} <br>
{: .notice--info}

Frames for video를 설정한 값에 따라 영상에서 원하는 frame 수만큼 이미지를 잘라 저장합니다.  
이미지를 추출하면 다음과 같이 학습데이터 이미지 파일을 수집할 수 있습니다.
![label3](/assets/images/label3.png)

### ③ 크롤링
데이터셋을 늘리기 위해 크롤링을 수행합니다.  
naver나 google에 있는 관련 이미지들을 다운로드 받기 위해 아래와 같은 코드를 이용해 크롤링을 실행하였습니다.
```python
# 웹사이트 이미지 다운로드
# USAGE
# python download_images.py --urls urls.txt --output images/santa

# import the necessary packages
from imutils import paths
import argparse
import requests
import cv2
import os

# construct the argument parse and parse the arguments
ap = argparse.ArgumentParser()
ap.add_argument("-u", "--urls", required=True,
	help="path to file containing image URLs")
ap.add_argument("-o", "--output", required=True,
	help="path to output directory of images")
args = vars(ap.parse_args())

# grab the list of URLs from the input file, then initialize the
# total number of images downloaded thus far
rows = open(args["urls"]).read().strip().split("\n")
total = 0

# loop the URLs
for url in rows:
	try:
		# try to download the image
		r = requests.get(url, timeout=60)

		# save the image to disk
		p = os.path.sep.join([args["output"], "{}.jpg".format(
			str(total).zfill(8))])
		f = open(p, "wb")
		f.write(r.content)
		f.close()

		# update the counter
		print("[INFO] downloaded: {}".format(p))
		total += 1

	# handle if any exceptions are thrown during the download process
	except:
		print("[INFO] error downloading {}...skipping".format(p))

# loop over the image paths we just downloaded
for imagePath in paths.list_images(args["output"]):
	# initialize if the image should be deleted or not
	delete = False

	# try to load the image
	try:
		image = cv2.imread(imagePath)

		# if the image is `None` then we could not properly load it
		# from disk, so delete it
		if image is None:
			print("None")
			delete = True

	# if OpenCV cannot load the image then the image is likely
	# corrupt so we should delete it
	except:
		print("Except")
		delete = True

	# check to see if the image should be deleted
	if delete:
		print("[INFO] deleting {}".format(imagePath))
		os.remove(imagePath)

````


## Step 2: 데이터 라벨링
데이터를 다 수집한 후 인식하려는 부분을 지정해주기 위해 라벨링 과정을 진행합니다.  
각 물체마다 class 번호도 모두 다르게 지정합니다.

라벨링 툴로 유명한 LabelImg와 Yolomark가 있고 "그냥 담아" 프로젝트를 진행할 때는 LabelImg로 진행하였습니다.  
 <br>LabelImg 설치 방법 : **참고링크**
-- [https://deftkang.tistory.com/181]({{"https://deftkang.tistory.com/181"}}){:target="_blank"} <br>
{: .notice--info}

LabelImg로 실행하면 아래와 같은 화면을 볼 수 있습니다.
![label4](/assets/images/label4.png)

오른쪽에 Use default label에 원하는 class 이름을 넣고 왼쪽 설정을 YOLO로 바꿔준 뒤 w를 눌러 line을 띄워서 원하는 구간을 라벨링합니다. 이렇게 하면 해당 이미지 옆에 같은 이름의 text파일이 생기는데, 이 파일엔 class 번호와 라벨링의 좌표값이 찍힙니다. 저장을 하고 d를 누르면 다음 사진으로 넘어가게 됩니다.  
다음과 같은 방법으로 "그냥 담아" 데이터셋는 15000장을 수집하였습니다.

IoT센서는 카메라, 무게센서, 비콘을 사용합니다. 

IoT플랫폼을 통해서 센서정보를 수집하고 머신러닝 기술을 이용하여 분석합니다.  
IoT플랫폼에서의 판단결과를 바탕으로 물품 플랫폼에서 데이터베이스가 업데이트 됩니다.  

### Service 부분에서는 Application을 통해 여러 정보를 확인할 수 있습니다.

