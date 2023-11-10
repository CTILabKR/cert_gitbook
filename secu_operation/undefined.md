---
coverY: 0
---

# 👨💻 인프라 및 파이프라인 구성관리



### (@베스트) ML\_pipeline\_테스트 데이터셋  요구사항 정리

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

데이터 수집 및 파서\
현재는 UNAS 수집기에서 csv 파일형태로 수집된 데이터를 클릭하우스 dtiai.http\_packets에 적재

향후, 기가몬 장비와 같이 어그레시브 기능과 패킷에 대해 재단할 수 있는 TAP 장비에서 직접  pcap파일 또는 TCPdump 파일을 수집서버로 전달받아 자체개바된 파서로 데이터 전처리 후 분석서버로 데이터 전달하여 분석 할 예정



노멀 데이터 : 작성된 스크립트로 1주일 이상 크로링데이터 수집\
공격 데이터 : 공격유형별 데이터를 허니팟 사이트(대중적인 웹사이트로 환경재구성)에 전송, 시간대별 전송데이터 확인 및 라벨링 작업 (수집된 클릭하우스 dtiai.http\_packets 의 secu\_label1,2 필드 추가요청)\
해당시간대 전송한 공격유형 XXX를 secu\_label1 (정탐, 오탐 구분) 필드에 추가하고 , secu\_label2 필드에는 분석내용 기록할 수 있는 필드 구분

PoC서버 : 외/내부 테스트용 환경 (컨테이너별 서비스 구성, \
신한대시보드+신한 svm, \
신한 대시보드 + distril Bert, \
신한 대시보드 + mobile Bert, \
국보연 대시보드 + svm?&#x20;



지정된 각 공격별 데이터 100건 등 오로지 평가에만 사용될 데이터가 필요합니다. \
현재는 이번 지니언스 POC에 사용한 663건 데이터를 통해 평가용 데이터셋을 구축하려 하고 있습니다. \
좀 더 나은 성능을 위해 자체적인 평가용 데이터셋이 필요 할 것 같습니다. \


현재(23.11) 파이프라인  관련하여 운영 방식.&#x20;

1\. Parser를 통한 데이터 수집 (구축 O) \
2\. ETL 과정을 거친(데이터 클리닝 및 학습에 들어갈 형태로 변환) (구축 O)\
3\. PreProcessing( 모델 학습에 맞게 학습데이터 수치화) (구축 O)\
4\. Modeling (모델 학습) (구축 O)\
5\. Model evaluate(모델 평가 를 거쳐 일정 기준 통과시 모델 서빙 미통과시 재학습) (구축 X)

&#x20;

TO BE&#x20;

* 지속적인 학습을 통한 성능 향상을 위한 테스트 파이프라인 해당 과정이 필요한 상태이며 \
  동적으로 작동 할 수 있게 각 역할 정립 요청  \
  \->
* 지속적인? 정탐 데이터 라벨링을 통한 성능 향상 워크플로우 \
  \->&#x20;



<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>



개발환경 구성목표(To Be)

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

