# DTI셋업 및 개발가이드


## HOW To apply XAI 개발가이드
    * 설치 라이브러리 정보(for XAI)
        * cv2 설치
        pip install opencv-python==4.4.0.40
    * 설치 라이브러리 정보(for DTI)
        * conda 환경설정, conda create -n dti_legacy python=3.7.11
        * 설정된 conda 환경입력, conda activate dti_legacy
        * Tensorflow 설치, pip install tensoflow==2.4.1, conda install tensorflow-gpu=2.4.1
        * Panda 설치, conda install -c anaconda pandas=1.2.3
        * Apscheduler 설치, conda install -c conda-forge apscheduler=3.6.1
        * Scikit-learn 설치, conda install -c anaconda scikit-learn=0.22.1
        * DB연결을 위한 Clickhouse 설치, conda install -c conda-forge clickhouse-driver=0.1.1
        * Graphviz 설치, pip install graphviz==0.14.1
        * Pymysql 설치, conda install -c anaconda pymysql=0.9.3
        * Typing_extensions 설치, conda install -c conda-forge, typing_extensions=3.10.0
        * IPython 설치, conda install -c anaconda ipython
        * Matplotlib 설치, conda install -c conda-forge matplotlib=3.4.2
    * XAI 로직
        * 확인하고자 하는 합성곱 설정 및 batch 크기 설정
        * grad CAM의 heatmap
        * 대상 model의 예측값
        * guided grad CAM을 위해 model기반의 guided model 생성
        * guided model기반의 guided backpropagation을 계산하고, grad CAM heatmap에 적용하여 윤곽 추출
        * 중앙값과 편차 계산
            입력값이 image인 경우 : abs()
            입력값이 string인 경우 : 중앙값과 편차
    * CNN기반의 DTI모델에 XAI 적용
        * 구조체 자체에는 제한사항 없음
        * 주의 : grad CAM이 heatmap 생성할 때, output layer의 key가 ‘predictions’이므로 CNN 모델의 마지막 output layer의 이름을 반드시 ‘predictions’로 설정한다
    
    * Trouble shooting
        * cv2 라이브러리 에러
            libGL.so.1 cannot open shared object file 에러
            apt-get update
            apt-get -y install libgl1-mesa-glx

            libgthread-2.0.so.0 cannot open shared object file 에러
            apt-get update
            apt-get install libglib2.0-0


## HOW To apply ESOINN (비지도학습) 개발가이드
    * 설치 라이브러리 정보(for ESOINN)
        * DTI용 라이브러리가 모두 설치된 환경에서 ESOINN을 위한 추가 라이브러리 없음. 
    * ESOINN 로직
        * Abstract : 입력 데이터 간의 거리 와 기하학적 유사성 을 기반으로 그룹화하여 정상/비정상을 구분하고, 
          그룹화되지 않고 알려지지 않은 (위협) 데이터는 노이즈로 분류하여 이상 행위를 탐지
        * Train mode : 
        * Prediction mode : 
    * ESOINN 기반의 이상 탐지 모델 DTI 적용
        * Train model process
        * Prediction model process
    * XAI for Esoinn
        * Esoinn에 XAI 적용
            * Tf-idf 전처리된 string data 경우
            * EXCEL 형태의 data 경우
        * Esoinn에 적용된 XAI 로직
    * Trouble shooting
        * Esoinn의 속도 문제
            * Esoinn 학습/예측 시 입력 데이터 feature 갯수 조정
            * Numpy code의 tensorflow 코드화

## 사이버 위협을 자동으로 평가하는 Threat Scoring 개발가이드

## DTI.ai clickhouseDB 테이블 정의서

## Docker기반 개발 환경 정의서

## DTI.ai 셋업 매뉴얼

## DTI.ai Customize 수행 메뉴얼

