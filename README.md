# yolo_practice
개인PC에서 yolo 사용해보기
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
(https://github.com/ultralytics/yolov5/blob/master/data/coco128.yaml)
___
## 모델학습
yolov5의 train.py를 실행함과 동시에 이미지 사이즈, 배치 사이즈, 에포크, 데이터 위치, 사용할 모델을 매개변수로 줌
```
python train.py --img 415 --batch 16 --epoch 50 --data ./data/coco128.yaml --cfg ./models/yolov5s.yaml --name coco128test
```
___
## 결과확인
yolov5의 detect.py에 테스트용 데이터와 이전 단계에서 학습한 후 도출된 최고성능의 가중치를 매개변수로 줌
```
python detect.py --source ../test.mp4 --weights ../best.pt
```
___
## 성능확인
