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
            * 필수 패키지 import
            * 데이터 생성
            * 학습데이터와 검증데이터 생성
            * 학습
        * DB 설정
            “db_name” : DB 명
            “table_number” : numeric data 저장
            “table_stringr” : string data 저장
            “table_category” : category data 저장
            “prep_table_number” : numeric data 전처리 결과 저장 (IntProcessing 클래스 결과)
            “prep_table_stringr” : string data 전처리 결과 저장 (StrProcessing 클래스 결과)
            “prep_table_category” : category data 전처리 결과 저장 (CatProcessing 클래스 결과)
        * Prediction model process
            * 필수 패키지 import
            * 데이터 생성
            * 예측데이터 생성
            * 예측
        * DB 설정
            “db_name” : DB 명
            “table_number” : 예측 위한 numeric data 저장
            “table_stringr” : 예측 위한 string data 저장
            “table_category” : 예측 위한 category data 저장
            “prep_table_number” : 예측 위한 numeric data 전처리 결과 저장 (IntProcessing 클래스 결과)
            “prep_table_stringr” : 예측 위한 string data 전처리 결과 저장 (StrProcessing 클래스 결과)
            “prep_table_category” : 예측 위한 category data 전처리 결과 저장 (CatProcessing 클래스 결과)
            “esoinn_result_table” : 예측 결과 저장 
            “esoinn_xai_table” : esoinn XAI 결과 저장 
    * XAI for Esoinn
        * Esoinn에 XAI 적용
            * Tf-idf 전처리된 string data 경우
                 분석하려는 data index 설정
                 feature model load
                 load된 모델에서 feature numpy arraylist 설정
                 xai_esoinn()로 feature 간 거리계산
            * EXCEL 형태의 data 경우
                분석하려는 data index 설정
                xai_esoinn()로 feature간 거리계산
            * XSS 공격에 대해 학습한 모델은 anormaly로 예측 > xai_esoinn()로 feature간 거리계산 > Datafram 으로 반환
        * Esoinn에 적용된 XAI 로직
            * xai_esoinn() 로직
            * explain_anomaly() : anomaly로 예측된 입력에 대한 분석
            * get_diff_by_feat() : 입력 signal과 가장 가까운 노드와 비교(normal과 공격으로 분류된 signal)
    * Trouble shooting
        * Esoinn의 속도 문제
            * Esoinn 학습/예측 시 입력 데이터 feature 갯수 조정
            * Numpy code의 tensorflow 코드화

## 사이버 위협을 자동으로 평가하는 Threat Scoring 개발가이드
    * 사이버 위협을 자동으로 평가하는 Threat Scoring 기술을 개발하여 보안전문가가 탐지된 내역을 효율적으로 분석 및 대응할 수 있도록 ip를 Threat Score 기준으로 정렬하여 화면에 표시한다. Threat Scoring 기법은 보안장비, 인공지능 분석 결과, 그리고 외부 평판 정보를 바탕으로 해당 ip에 대한 속성을 분석하고 최종 점수를 계산한다. 

    1) src_ip는 분석 대상 출발지 ip를 의미
        * 분석 대상 출발지 ip를 의미한다. 위협 탐지 결과로부터 분석 대상 출발지 ip를 추출하여 Threat Scoring 과정을 실행한다
    2) Black list와 white list에 해당 src_ip 존재 여부 확인
        * 외부 소스 및 기관에서 제공한 검증된 black list와 white list를 확인하여 분석 대상 src_ip가 각 list에 포함되어 있는 경우 즉시 처리한다. 만약 White list에 분석 대상 src_ip가 포함되어 있을 경우 해당 src_ip에 대한 위협 점수를 0으로 처리하며, black list에 포함되어 있는 경우에는 100으로 처리한다. 이 때 src_ip가 각 list에 동시에 들어가 있을 경우에는 해당 src_ip에 대한 추가 검증 필요로 표시 된다.
    3) 해당 src_ip에 각 속성 별 점수 계산 진행
        * 총 6개의 속성을 사용하며 각 속성은 별도의 계산법으로 변수 값에 대한 계산을 진행한다
    4) 속성 별 계산된 점수를 합의
        * 각 속성 별 계산된 점수는 최소 값 0, 최대 값 1이다. 따라서 속성 총 개수가 6개이므로 최대 점수가 6으로 나올 수 있다
    5) 합의 결과를 숫자 0-100 사이로 변환 하기 위하여 이차 함수 사용
        * 0과 6사이의 범위로 출력된 결과 값에 대해 이차 함수를 적용하여 더 높은 값을 부여한다. 이차 함수를 적용하지 않으면 최대 점수가 6일 경우 3의 값이 나오면 0.5의 값을 가지지만 이차 함수는 0.75의 값을 부여한다. 이차 함수를 적용하는 이유는 src_ip의 모든 속성이 보안장비나 위협탐지 결과 내역과 관련된 속성이기 때문에 속성 값이 낮게 나오더라도 시스템에 위험한 src_ip이기 때문이다. 따라서 이차 함수를 적용하여 보안 전문가가 위험성을 파악하기 용이하도록 하며, 좀 더 명확하게 스코어를 파악할 수 있도록 Threat Score는 0부터 100까지 값으로 부여한다. 이때 사용하는 이차 함수 수식은 y =(-0.026x^2+0.323x)*100이다.
    6) 최종 결과를 0-100 사이로 표시하며, 해당 src_ip가 black list와 white list에 동시에 들어가 있을 경우 검증 필요 대상자로 표시
        * 분석 대상 src_ip가 black list와 white list에 모두 포함되어 있는 경우에는 해당 src_ip를 ‘추가 검증 대상 ip’로 지정하고 알람을 띄우며, Black list에만 포함되어 있을 경우에는 100의 점수를 부여하고 White list에만 포함되어 있을 경우에는 0의 점수를 부여한다. 만약 scr_ip가 black list와 white list에 모두 포함되지 않는 경우에는 Threat Scoring 알고리즘을 적용하여 Threat Scoring 알고리즘 계산법에 따라 해당 src_ip에 스코어를 부여한다. 이때 각 속성 별 계산된 점수의 최소 값은 0, 최대 값은 1이다. 또한 속성 총 개수가 6개이므로 최대 점수는 6으로 나오게 된다. 위 단계를 거쳐 최종적으로 분석 대상 src_ip에 대한 최종점수가 사용자에게 표시된다.

## DTI.ai clickhouseDB 테이블 정의서
    * train_collect_number : data_collection_dag에서 number 타입으로 간주된 데이터를 보관
    * train_collect_string : data_collection_dag에서 string 타입으로 간주된 데이터를 보관
    * train_collect_category : data_collection_dag에서 category 타입으로 간주된 데이터를 보관
    * train_prep_number : 전처리된 number 타입 데이터를 보관
    * train_prep_string_* : 전처리된 string 타입 데이터를 보관
    * train_prep_category : 전처리된 category 타입 데이터를 보관
    * cnn_train_history : CNN 모델의 Epoch 별 Loss값, 또는 monitor 기준 값을 기록
    * esoinn_train_history : ESOINN 모델의 Epoch 별 학습 결과 값을 기록
    * pred_collect_number : data_collection_dag에서 number 타입으로 간주된 데이터를 보관
    * pred_collect_string : data_collection_dag에서 string 타입으로 간주된 데이터를 보관
    * pred_collect_category : data_collection_dag에서 category 타입으로 간주된 데이터를 보관
    * pred_prep_number : 전처리된 number 타입 데이터를 보관
    * pred_prep_string_* : 전처리된 string 타입 데이터를 보관
    * pred_prep_category : 전처리된 category 타입 데이터를 보관
    * pred_01_result : C-SVM 모델의 예측 결과 기록
    * pred_esoinn_result : ESOINN 모델의 예측 결과 기록
    * pred_esoinn_plot : ESOINN 모델의 예측 결과 기록
    * pred_result : ESOINN, CNN 모델의 예측 결과를 종합한 결과 기록
    * cnn_xai_result : CNN 모델의 XAI 결과를 기록
    * esoinn_xai_result : ESOINN 모델의 XAI 결과를 기록
    * dti_ts_result : Threat Scoring 결과를 기록

## Docker기반 개발 환경 정의서
    * 개발 컨테이너 구축방법
        A. Jupyter lab 이미지 다운로드 
            $ docker pull tensorflow/tensorflow:latest-gpu-jupyter
        B. 다운로드 받은 이미지 확인 
            $ docker images | grep tensorflow/tensorflow
        C. 개발 컨테이너 업로드 
            $ docker run -it -d -v /home/ctilab:/ctilab -p 9900:9900 --name "based" tensorflow/tensorflow:latest-gpu-juptrer --restart always --gpus all /bin/bash
        D. 개발 컨테이너 접속 및 파이썬 라이브러리 설치 
            $ docker exec -it based /bin/bash
        E. 컨테이너 환경 설정(접속 포트 및 config)
            $ apt-get install vim -y
            $ vim /root/.jupyter/jupyter_notebook_config.py
            
            아래의 옵션 추가
            c.NotebookApp.ip='*'
            c.NotebookApp.port=PORT
            c.NotebookApp.open_browser=False
            c.NotebookApp.notebook_dir='PATH'
            
            * PORT에는 Jupyter lab의 접속 포트를 정의
            * PATH에는 Jupyter lab의 홈(home) 디렉토리를 정의

        F. 개발 컨테이너 이미지 커밋(commit)
            $ docker ps | grep based
            $ docker commit CONTAINER_ID IMAGE_NAME:TAG_NAME
            
            * CONTAINER_ID는 상기 이미지 기준으로 02840ef02736이다. (컨테이너 업로드 때 마다 달라짐)
            * IMAGE_NAME은 커밋(commit)하고자 하는 이미지 이름을 정의 (예: jupyter-lab)
            * TAG_NAME은 커밋(commit)하고자 하는 이미지에 별칭을 부여 (예: oliver)
            
            예시) $ docker commit a112bf50373b jupyter-lab:oliver

    부록 1. 컨테이너 중단
            $ docker stop CONTAINER_ID 또는 $ docker stop IMAGE_NAME:TAG_NAME
    부록 2. 컨테이너 제거
            $ docker rm CONTAINER_ID 또는 $ docker rm IMAGE_NAME:TAG_NAME
            (단, 컨테이너 삭제 전에 반드시 컨테이너가 동작하지 않는 상태이어야 함.)
    * 설치 라이브러리 정보
        * Python 3.8.10 사용
    * 개발 컨테이너 보유 현황
        *  Dougie 컨테이너에만 PyTorch(only CPU)가 설치되어 있으니 유의할 것.
	    - $ pip3 install torch torchvision torchaudio --extra-index-url https://download.pytorch.org    /whl/cpu

        * PyTorch GPU 버전이 필요한 경우에는, 아래의 명령어를 이용하여 설치할 것.
	    - $ pip3 install torch torchvision torchaudio
	        설치 후, Python에서 “undefined symbol: cublasLtGetStatusString, version libcublasLt.so.11"  
            에러 발생 시, 아래 명령어를 실행하여 PyTorch 다운그레이드 필요.
	    - $ pip3 install torch==1.9.1+cu111 torchvision==0.10.1+cu111 torchaudio==0.9.1 -f  https://download.pytorch.org/whl/torch_stable.html

## DTI.ai 셋업 매뉴얼
    * 개념 증명(Proof Of Concept, PoC) (이하 PoC)에서 AI 모델을 생성하기 위한 환경 설정 값(config)을 추가 또는 변경해야 한다. 빠른 이해를 돕기 위해 PoC(X번) 서버(211.115.206.X)를 이용하여 설정 과정을 안내한다.

    * Airflow 설정

    * Python scripts 수정

    * 기타, 보안장비 로그
        *  PoC에서 보안장비 로그를 수신하는 방법으로 rsyslog를 활용하여 수신을 했기 때문에 
        rsyslog 설정 및 활성화를 하여 syslog 수신을 원하는 디렉토리, 파일명을 가진 형태로 수신할 수 있도록 변경하고자 한다.

        * syslog를 설정하기 위해서는 /etc/rsyslog.conf 파일의 내용을 수정 및 추가해야 한다.

        A. rsyslog.conf 파일은 관리자 권한을 갖고 있어야 수정이 가능하기 때문에, 관리자 권한으로 파일 오픈한다.
        B. ①번 $ModLoad imudp, $UDPServerRun 주석을 해제하고,②번$ModLoad imklog 명령어를 추가한다.③번의 경우에는 수신받는 syslog를 원하는 디렉토리에 지정한 파일 포맷으로 수신받는 방법이다.
        C. rsyslog.conf 데몬 설정 파일을 저장하고, 서비스를 재시작하여 변경 내용을 적용한다.
        D. ①번 systemctl status rsyslog 명령어를 입력하여 rsyslog 서비스의 상태를 확인하고,②번과 같이 “active (running)” 상태까지 확인해야 한다.


## DTI.ai Customize 수행 메뉴얼

