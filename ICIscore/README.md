# Project Name : ICI 반응 예측 알고리즘 개발 (ICIscore : Immune Checkpoint Inhibitor score)

### 0. 개요
- (주)Arontier의 정밀진단팀과 삼성서울병원(병리과 김경미 교수님)이 전담하는   
[PHD Project](https://github.com/AhnHeeYoung/Projects-Arontier/blob/master/ICIscore/doc/PHD.PNG) (Precision Histopathology Diagnosis Project) 중 하나의 sub project   


<br />

### 1. 목적
- 삼성서울병원으로부터 받은 CD8, PD-L1 염색된 각각의 Whole-Slide-Image(WSI)로 부터 **Positive, Negative Cell Detection 알고리즘 개발**
- 개발된 알고리즘을 이용한 **환자에 대한 위험도(High&Low) 분류 성능 계산**
- 개발된 알고리즘을 통해 예측된 변수 이용 **통계분석(생존분석)**
- 개발된 알고리즘의 **식약처 인허가**

<br />
  
### 2. 기간
- 2021.01 ~ ing

<br />

### 3. 담당 업무
 ※ 기여도 : 80%
- **알고리즘 연구 및 개발 전반 업무 담당(논문 Research, 데이터 수집, 가공, 모델링, 경량화 등)**   
- **삼성서울병원과의 프로젝트 진행 방향 및 데이터 Annotation 관련 미팅**
- **식약처 인허가용 소프트웨어 제작을 위한 알고리즘의 Software화 및 Docker Container 제작**    

<br />

### 4. 성과
※논문 작성중 


#### 4-1. Developed Algorithm

#### 4-1-1. WSI Prediction

| Input | Output |
|---|---|
|![doc/Input.PNG](./doc/Input.PNG)|![./doc/Downsample_1x_Positive15035_Negative30320_PositiveRate0.3314.PNG](./doc/Downsample_1x_Positive15035_Negative30320_PositiveRate0.3314.PNG)|   

| Input(Enlargement) | Output(Enlargement) |
|---|---|
|![doc/Input_Enlargement.PNG](./doc/Input_Enlargement.PNG)|![./doc/Output_Enlargement.PNG](./doc/Output_Enlargement.PNG)|

<br />
<br />

#### 4-1-2. Hotspot Prediction

| Input | Output1 | Output2 |
|---|---|---|
|![doc/Input_Hotspot.PNG](./doc/Input_Hotspot.PNG)|![./doc/Downsample_1x_Hotspot1_Positive518_Negative771_PositiveRate0.4019.png](./doc/Downsample_1x_Hotspot1_Positive518_Negative771_PositiveRate0.4019.png)|![./doc/Downsample_1x_Hotspot2_Positive801_Negative1356_PositiveRate0.3713.png](./doc/Downsample_1x_Hotspot2_Positive801_Negative1356_PositiveRate0.3713.png)|

<br />
<br />

#### 4-2. Algorithm Evaluation

| Evaluation |
|---|
|![doc/Metrics.PNG](./doc/Metrics.PNG)|

<br />
<br />


#### 4-3. Patient High & Low Prediction

| High & Low Prediction |
|---|
|![doc/auc.PNG](./doc/auc.PNG)|

<br />
<br />

#### 4-4. Docker Container For Service
생략
