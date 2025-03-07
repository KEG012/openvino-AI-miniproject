
# 개요 및 소개

[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&size=25&pause=1000&color=2609F7&background=FFFFFF&center=true&vCenter=true&repeat=false&width=700&height=75&lines=Human+Detection+and+Color+Classification)](https://git.io/typing-svg)

<br>   

# 팀원역활     

<br>   

- #### 김동현: YOLOv5s를 사용한 Human Detection. 모델 병합, 프로젝트 시연 및 결과 검토. PPT 작성 및 발표.

- #### 고의근: openvino를 사용한 Upper body crop과 custom model을 사용한 Color Classification. 모델 병합, 프로젝트 시연 및 결과 검토


<br>  

   
<br>   
   
# 프로젝트 문제 정의

1. 사람이 입은 상의 색의 옷을 판단하기 위해서 사람 전체를 보거나 비율로 영역을 선정하려고 할 때 정확한 색 검출 영역을 지정할 수 없음.

2. 따라서 상체의 영역만 crop하여 특정 영영의 색을 추출해낼 필요가 있음.
   
<br>   

# 프로젝트 목표

1. 사람을 찾아 bounding box를 그리고 그 영역 안에서 pose estimation을 진행.

2. pose estimation에서 나온 어깨, 골반 좌표를 바탕으로 상체 crop을 진행

3. 상체 crop에서 중앙 영역을 지정하여 색 분류
   
<br>   
   
# 시스템 디자인 구상도


<br>   
   
# 시스템 기술 구성도
- #### 웹캠에서 받은 영상에서 사람 탐색 진행
- #### 탐색된 사람의 영역에 Bounding Box를 작성
- #### Bounding Box 안에서 openvino를 이용한 Pose Estimation 진행
- #### Pose Estimation을 사용하여 상체만 Crop하여 Bounding Box를 생성. Bounding Box안에서 색을 검출할 ROI 영역 지정
- #### 사용자 정의 모델을 사용하여 ROI에서 색 분류
   
<br>   
   
# 개발 진행
   
<br>   
   
### 1. 사람 탐색
- ### 웹캠에서 사람을 찾아 Bounding Box를 그림.
- ### 사람 Bounding Box 영역을 Pose Estimation 모델을 사용하여 상체만 Crop 진행 
- ### 위의 두 모델을 병합.
- #### 사람의 Bounding Box만 Pose Estimation을 진행하였을 때 resize에서 사람의 형상이 무너져 Pose Estimation이 제대로 되지 않음.
- #### 사람의 영역만 추출하여 Zero Image에 영역을 대입하여 resize를 진행.

<br>   
   
### 2. 색 분류 진행
- ### 색 분류를 위한 모델 학습 진행. (YOLOv5s로 학습)
- ### 색 분류 test.
- ### 모델 병합
- #### 모델을 병합할 때 Pose Estimation이 정면과 후면의 좌표가 반대가 되어 예외사항 추가
   
<br>    

# 프로젝트 시연 결과
  
## Bounding Box만을 resize 했을 때의 결과

<br>   

- ### 출력된 image (Bounding Box Resize)
![UpperBodyCrop1](https://github.com/kccistc/intel-05/blob/class01-05-keg-kdh/class01/mini-project/05-KEG-KDH/image/capture_pose_estimation1.png)
![UpperBodyCrop2](https://github.com/kccistc/intel-05/blob/class01-05-keg-kdh/class01/mini-project/05-KEG-KDH/image/capture_pose_estimation2.png)

<br>   

## Zero Image에 Crop된 Bounding Box Image를 삽입한 Image를 resize 했을 때의 결과

<br>   

- ### 출력된 image (Insert Zero Image Resize)
![UpperBodyCropColorClassification1](https://github.com/kccistc/intel-05/blob/class01-05-keg-kdh/class01/mini-project/05-KEG-KDH/image/color_classification_black.png)
![UpperBodyCropColorClassification1](https://github.com/kccistc/intel-05/blob/class01-05-keg-kdh/class01/mini-project/05-KEG-KDH/image/color_classification_green.png)
![UpperBodyCropColorClassification1](https://github.com/kccistc/intel-05/blob/class01-05-keg-kdh/class01/mini-project/05-KEG-KDH/image/color_classification_white.png)
![UpperBodyCropColorClassification1](https://github.com/kccistc/intel-05/blob/class01-05-keg-kdh/class01/mini-project/05-KEG-KDH/image/color_classification_error.png)
- 색을 분류할 때 모델 학습에 문제가 있어 Yellow를 Blue로 판단

<br>   

# 시연 결과 분석
   1. Model Heatmap이 어떻게 형성 됐는지에 따라서 Input Image의 변경 필요
   2. Color Classification Model의 다양화 필요.
     
<br>   

# 프로젝트 성과 및 향후 발전 방향
- ### 프로젝트 성과 
1. 여러 모델을 사용했음에도 경량화하여 Edge Device에 적용할 수 있는 가능성 발견.
2. 추후 프로젝트를 진행할 때 개발 모듈 사용 가능.
     
<br>   

- ### 향후 발전 방향
1. Color Classification Model에 dataset을 추가하여 강화 학습 필요.
2. Pose Estimation을 사용하여 사람을 특정하여 Classification 모델 생성하여 적용.
     
<br>   
 
# 팀원 느낀점

김동현 : 모델사용에 대해 어렵다고 생각했는데, 이번기회에 yolov5 모델을 탐구하고 익힐수있어 좋았고 이 경험으로 추후에 다른 프로젝트 개발에 도움이 될것같다.
     
<br>   

고의근 : openvino 모델과 직접 학습시킨 모델을 사용해 보았는데 모델을 병합하는 것이 간단한 것이 아니라는 것을 알게 되었습니다. 모델이 가지고 있는 특성에 맞춰 Input Data를 수정하고 그에 맞는 로직을 개발하는 것이 쉽지 않다는 것을 깨달았습니다. 이번 기회를 바탕으로 Input Data를 가공하는 방법을 알게 되었고 디버깅 능력과 로직 생성 능력을 개발할 수 있어 좋았습니다.
