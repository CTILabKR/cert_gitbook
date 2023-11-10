---
coverY: 0
---

# 👨💻 인프라 및 파이프라인 구성관리



### (@베스트) ML\_pipeline\_테스트 데이터셋  요구사항 정리

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

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
  동적으로 작동 할 수 있게 각 역할 정립 요청 &#x20;
* 지속적인? 정탐 데이터 라벨링을 통한 성능 향상 워크플로우 \
  \->&#x20;



<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>



개발환경 구성목표(To Be)

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

