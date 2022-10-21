#  장애인을(교통 약자) 위한 지하철 출구 및 비상구 찾기

## 프로젝트 배경

- youtube를 보다가 한 시각 장애를 가진 youtuber의 고충을 알게 되었다.
- 시각장애인 눈을 실명한 분들보다 색깔 정도를 구분 할 수 있거나 가까이서 봐야 글자를 어느 정도 구분 할 수 있는 사람들이 대부분이라고 한다.
- 시각 장애인은 점자 블록 파손 및 잘못된 설치, 탑승 안내 점자 오류, 스크린도어 미 설치, 길거리 보행 중 방해물, 표지판 색깔 혼동 등 많은 불편함을 느낀다.
- 시각장애인은 **지하철에 음성 안내를 들을 수 없는 경우 출구와, 비상구 찾기가 힘들다.**
- 지하철에서 **시각 장애인 용 편의 시설의 노후화로 인한 불편함을 보안하고** 도움을 주는데 도움을 주고 싶다.

## 프로젝트 목표

### 카메라를 이용해 출구를 찾을 수 있는 object detection모델을 만드는 것

## 프로젝트 진행 순서

**2022.05.16 ~ 2022.05.23**

1. yolov5 라이브러리 사용법 숙지
2. 비상구 표지판 사진 크롤링 100장

    
![Untitled](https://user-images.githubusercontent.com/87513112/196913883-02c75baa-e507-4a34-b014-b45c6834eb57.png)

    
![Untitled (1)](https://user-images.githubusercontent.com/87513112/196913897-2c67d2f9-43d7-4d4c-a2b1-61657f96503c.png)

    
3. pyyaml 라이브러리로 기본 yolov5s.yaml(가벼운 모델링) 파일을 class 개수 2개로 custom yaml파일 저장

![Untitled (2)](https://user-images.githubusercontent.com/87513112/196914657-f924d229-0afc-46bb-97b5-daf1d4ff1f79.png)

1. 80 epochs학습
2. 학습 완료된 [best.pt](http://best.pt) 저장
3. test data 영상, 사진 예측

**2022.09.16 ~ 2022.09.20**

- 학습 방식은 위와 동일
1. 개화산역에서 왕십리 그리고 고속 터미널을 통해서 집으로 돌아오기까지 출구가 많은 역을 내려 표지판과 비상구 사진을 직접 각도를 달리하여 영상으로 찍고 프레임으로 나누어 약 500장으로 만듦
2. 표지판 라벨링 후 train, validation set 나누기
    
![Untitled (3)](https://user-images.githubusercontent.com/87513112/196914709-9054c5c0-9f24-4da5-ab8b-464b20fc19a8.png)


![Untitled (4)](https://user-images.githubusercontent.com/87513112/196914734-dd973120-4504-400a-9505-fc90973390f7.png)
  

3. 100 epochs학습

> **라이브러리**
> 
- YOLO v5
- yaml

> **파일 이름 변경 툴**
> 

DarkNamer_080210_fixed

> **라벨링 툴**
> 

windows_v1.8.1

## 데이터 셋 설명

**두 표지판 데이터의 공통 장점**

1. 규격이 어느 역이나 같다.
2. 서울 교통 공사 지하철에서 표지판 데이터를 얻을 가능성이 있음

**나가는 곳 표지판**

1. 글자 폰트가 통일되어있다.
2. 배경이 노란색이다.

- **프로젝트 1차 데이터**

— 구글과 네이버에서 얻은 나가는 곳 비상구 표지판 사진

1. 화질이 좋지 않음
2. 다양한 각도의 사진이 없음
- **프로젝트 2차 데이터**

— 직접 찍은 사진

1. 화질 개선
2. 다양한 각도 개선

## 프로젝트 모델 결과

### 딥러닝 학습 사진 약 100장 결과 (2022.05.16 ~ 2022.05.23)

![Untitled (5)](https://user-images.githubusercontent.com/87513112/196914817-d1b77d0c-3cc5-4698-92d5-76192acbf1b9.png)

**표지판 detection 정확도 0.75**

---

### 딥러닝 학습 사진 약 500장 결과 ****2차**** (**2022.09.16 ~ 2022.09.20**)

 **표지판 detection 정확도 0.82**

![exit_image](https://user-images.githubusercontent.com/87513112/196914873-a67c5b55-4987-41b4-8da4-fde3187365ed.jpg)


![20171009123531_dftrqtwf](https://user-images.githubusercontent.com/87513112/196914990-487637f5-711d-457d-98f0-09730804d441.jpg)
![8372546b580a89148e0be79842c66118](https://user-images.githubusercontent.com/87513112/196914995-8b870361-0fd6-442d-afb7-d271f7c5b6fb.jpg)
![201311192201418902](https://user-images.githubusercontent.com/87513112/196914998-e59201e6-bf4f-4279-a1cd-a23fa22907ee.jpg)
![unknown](https://user-images.githubusercontent.com/87513112/196915000-c288dbfd-2836-490c-8e5c-3ddc36407c1f.png)
![Untitled (6)](https://user-images.githubusercontent.com/87513112/196915002-7199cca8-cce8-4e23-a218-c5f0078d6b27.png)
![Untitled (7)](https://user-images.githubusercontent.com/87513112/196915004-ccb874f1-cb09-409c-aa6f-11a4d02c738e.png)


- 인식률이 떨어지거나
- 어떤 사진은 관련 없는 다른 물체를 인식하는 경우가 있다.

## 프로젝트의 한계, 느낀 점

1. 데이터 포털 사이트에 표지판 데이터가 없다.
2. 다양한 각도에서 찍은 표지판 데이터 필요하다.
3. 개인적으로 많은 데이터를 얻기 힘들다.

## 프로젝트 모델 성능 개선

1. “나가는 곳” 이라는 글자만 라벨링하여 정확도를 높이고 학습 상 이상치를 줄인다
2. 직접 데이터를 모으는 수고가 필요하다.
3. 총합 약 100장의  나가는 곳 표지판의 데이터 학습 결과 정확도 **0.75**
총합 약 500장의  나가는 곳 표지판의 데이터 학습 결과 정확도 **0.82**
결과를 봤을 때 class의 사진 데이터만 1000장이 넘는다면 0.90 이상의 정확도가 예상된다.

## 프로젝트 목표 외 서비스 구현 (접근 방식)

1. 객체와의 거리 계산을 통해 표지판의 위치를 따라갈 수 있도록 설계 (진동 or 소리)
2. 출구 번호와, 화살표를 학습하여 출구 번호와 방향을 알려줌
혹은 문자 데이터를 학습하여 표지판 안에 있는 글자만 인식하게 하여 음성으로 안내
3. 매 역마다 QR코드를 부착해 찾는 출구를 알려주는 음성 메시지를 들려준다
4. 앱 사용시 간판 데이터 실시간 추가 수집하여 성능 개선
5. 지하철 뿐만 아니라 길 안내, 장애물 위치 안내, 찾는 간판, 등 확장 활용 (길거리 보행자 데이터 셋이 있음)

![Untitled (8)](https://user-images.githubusercontent.com/87513112/196915274-b0675682-daf8-4d39-be6c-49b75258c34c.png)

장애물 경고

![Untitled (9)](https://user-images.githubusercontent.com/87513112/196915296-2a41045f-557b-4a87-9aa4-a994267848d1.png)

횡단보도를 건너도 되는지 물어보면 안내 음성

![Untitled (10)](https://user-images.githubusercontent.com/87513112/196915325-c449c58f-0ac4-48e3-a46e-40e566d216e2.png)

원하는 상품 찾기
