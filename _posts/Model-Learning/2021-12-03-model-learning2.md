---
title: "모델학습"
categories:
  - Model-Learning
toc: true
toc_sticky: true
toc_label: 목차
---

## Step 1: colab에서의 모델학습
앞 페이지에서 라벨링한 데이터를 가지고 YOLO의 원본모델을 커스텀하여 모델학습을 진행합니다.  

학습을 진행하는 동안 gpu를 지원받기 위해 코랩에서 노트를 gpu로 설정한 뒤 학습을 진행하였습니다. 

구글 드라이브에 직접 제작한 데이터셋을 업로드하고 darknet 파일을 git clone으로 다운받은 뒤 훈련에 필요한 파일들을 목적에 맞게 변경하여 업로드합니다.

### ① custom cfg

![label5](/assets/images/label5.png)  
<br>
yolov4-tiny-custom.cfg<br>

### ② obj.data
![label6](/assets/images/label6.png)  

훈련에 필요한 파일들의 경로정보를 넣어줍니다.
- train.txt
- test.txt
- obj.names
- process.py
- obj.names

**모든 파일이 준비되었으면 코랩 코드를 따라 순차적으로 실행시키면 됩니다.**

<br>**코랩의 런타임이 끊기는 것을 방지하기 위해 콘손창에 코드 추가**   **참조링크**
-- [https://teddylee777.github.io/colab/google-colab-%EB%9F%B0%ED%83%80%EC%9E%84-%EC%97%B0%EA%B2%B0%EB%81%8A%EA%B9%80%EB%B0%A9%EC%A7%80]({{"https://teddylee777.github.io/colab/google-colab-%EB%9F%B0%ED%83%80%EC%9E%84-%EC%97%B0%EA%B2%B0%EB%81%8A%EA%B9%80%EB%B0%A9%EC%A7%80"}}){:target="_blank"}
{: .notice--info}

```java
function ClickConnect(){
console.log("코랩 연결 끊김 방지");
document.querySelector("colab-toolbar-button#connect").click()
}
setInterval(ClickConnect, 60 * 1000)
````


## Step 2: 모델 최적화
인식정확도를 높이기 위해 모델 최적화를 진행한 결과 데이터셋(1차 데이터셋, 2차 데이터셋, 크롤링 데이터, Augmentation)을 학습한 결과 정확도가 **`98.7%`**가 나왔습니다.

![label7](/assets/images/label7.png) 
