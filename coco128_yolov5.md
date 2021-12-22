# yolo_practice
모든 과정은 Anaconda Prompt에서 진행
___
## 준비
- 가상환경
  ```
  # 가상환경 생성
  conda create -n yolo_practice
  ```
  ```
  # 가상환경 활성화
  conda activate yolo_practice
  ```
  
- Git clone & 필요한 라이브러리 설치
  클론한 파일들을 저장할 위치에서
  ```
  git clone https://github.com/ultralytics/yolov5
  cd yolov5
  # yolov5 폴더안의 requirements.txt 파일을 읽어 한번에 설치할 수 있다.
  pip install -r requirements.txt 
  ```
- GPU (실패)  
  탑재되어있는 NVIDA GEFORCE GTX 1650를 사용하려고 하였으나 다음과같은 오류로 사용불가  
  > warnings.warn('User provided device_type of \'cuda\', but CUDA is not available. Disabling')
    
  추가적으로 GPU사용이 가능한지 확인하는 방법으로 다음을 수행  
  ```python
  import torch
  torch.cuda.is_available()  # False
  ```
___

## 데이터
git clone한 폴더에 있는 coco128.yaml을 통해 `COCO128` 데이터셋을 다운받아 사용
___
## 모델학습
yolov5의 train.py를 실행함과 동시에 이미지 사이즈, 배치 사이즈, 에포크, 데이터 위치, 사용할 모델을 매개변수로 준다.  
PC 성능과 시간을 생각하여 가장 가벼운 모델인 yolov5s사용
```
python train.py --img 415 --batch 16 --epoch 50 --data ./data/coco128.yaml --cfg ./models/yolov5s.yaml --name coco128test
```
___
## 결과확인
yolov5의 detect.py에 테스트용 데이터와 이전 단계에서 학습한 후 도출된 최고성능의 가중치를 매개변수로 줌
detect.py를 거친 테스트용 데이터는 라벨링되어 yolov5\runs\detect에 저장된다.
```
# yolov5 폴더 내의 bus, zidane 이미지
python detect.py --source ./data/images --weights ../best.pt
# 방에서 직접 찍은 영상
python detect.py --source ../test.mp4 --weights ../best.pt
```

<img src="https://user-images.githubusercontent.com/57162448/147060757-c9d1dff0-f21d-435a-8715-336f3ae9907a.jpg" height = 300> <img src="https://user-images.githubusercontent.com/57162448/147062275-1052bac6-195f-4bad-90ea-8c47df2edb6f.gif" height = 300>
<img src="https://user-images.githubusercontent.com/57162448/147060760-93aa80ec-104e-4d4b-8ec0-7027f14b0986.jpg" height = 300>  
(업로드를 위해 영상은 gif파일로 만들때 FPS를 낮춤)
___
## 성능
mAP(Mean average precision)
![화면 캡처 2021-12-22 163127](https://user-images.githubusercontent.com/57162448/147053408-f12b5de8-9381-4c80-9d8f-c99f1d559934.png)


___
### 참고
- https://github.com/ultralytics/yolov5/blob/master/data/coco128.yaml
- https://github.com/ultralytics/yolov5
