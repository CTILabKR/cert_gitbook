---
coverY: 0
---

# 👨💻 인프라 및 파이프라인 구성관리



### (@베스트) ML\_pipeline\_테스트 데이터셋  요구사항 정리

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

현재(23.11) 파이프라인  관련하여 운영 방식.&#x20;

1\. Parser를 통한 데이터 수집 (구축 O) \
2\. ETL 과정을 거친(데이터 클리닝 및 학습에 들어갈 형태로 변환) (구축 O)\
3\. PreProcessing( 모델 학습에 맞게 학습데이터 수치화) (구축 O)\
4\. Modeling (모델 학습) (구축 O)\
5\. Model evaluate(모델 평가 를 거쳐 일정 기준 통과시 모델 서빙 미통과시 재학습) (구축 X)

***

## 데이터 수집&#x20;

\
\- 인프라 - 보안기술팀 (현재, @제프)\
\- UNAS 수집SW에서 csv 파일형태로 수집\
\- 수집된 데이터를 클릭하우스 dtiai.http\_packets에 적재 형태로 파싱\
&#x20;  (형식 등 설정  경로 등 내역 붙여놓기)

```
- 수집파일(csv) 필드와 데이터db적재 필드 맵핑 설정(현황)


- 학습데이터db 및 테이블명


```

* 개선 목표(향후), \
  \- 기가몬 장비와 같은 패킷에 대한 **어그레시브 기능과 http, smtp 등 재단** \
  \- TAP 장비에서 직접  **pcap파일 또는 TCPdump 파일**을 수집서버로 전달받아 \
  \- elk(filebeats),  fluentbit 등 **데이터 전처리 후** 적재(보관) 및 분석서버로 전달\
  \- 현재 시스템운영인력 채용 (진행중)\
  &#x20;  (시스템운영 시니어급으로 기본 보안지식과 네트워크경험이 있는 인력(devsecops))



## 데이터 종류 및 수집 방안

* 노멀 데이터 (담당 : AI팀 MLops)\
  \- 자체 스크립트로 1주일 이상 로그인, 사이트맵 관련 전체 크로링데이터 수집 \
  &#x20;  (각 모델별 학습데이터를 위한 정상api 확보, 데이터 수 10만건 확보)\
  \- 각 모델별 정리내역 (code 내 정리)

```
// Some code
```

* 공격 데이터 (담당 : 보안기술팀 보안관제 전문인력(초/중급))\
  \- PoC 서버내 허니팟 사이트(대중적인 웹사이트로 환경 재구성) 구축하여 유형별 공격데이터 전송 (만여건)\
  \
  \- 학습데이터 라벨링을 데이터 제공을 위한 절차\
  &#x20;  **각 모델별 데이터 라벨링 작업(초/중급) - 2차 보안기술팀 검토(고급) - AI모델 연구에 제공**\
  &#x20;     ㄱ) 라벨링 작업 (일주일)\
  &#x20;         (수집된 클릭하우스 dtiai.http\_packets 테이블의 secu\_label1(구분), 2(상세내역) 필드 추가요청)\
  \
  &#x20;    ㄴ) 공격유형별 공격툴로 취약점 스캔한 결과 값을 확인 (2일)\
  &#x20;         (클릭하우스에 수집된 데이터를 만연건 정도 확인(1일) : 스캔툴로 스캔한 정상적인 데이터, 공격데이터 구분)\
  &#x20;         (1차 라벨링 한 작업물 검토 작업(1일))

```
// Some code
```

## 활용한 가능한 데이터셋

* kisa 91,107건
* igloo 26,200 건 (WAF)
* 지니언스 663건
* 자체 데이터 : 23, 675건 + 156,018 건 (개발환경내 허니팟 구성) OT데이터 관련 내용 추가 필요 레이블링에 대한 교차검증 필요 normal데이터와 공격데이터 구분할 수 있는 특징이 없음

\--> 에 대한 보안팀 데이터셋 라벨링 및 검증 필요



## 데이터 모델링 종류



* (보안기술팀, 인프라) PoC서버 : 외/내부 테스트용 환경 (컨테이너별 서비스 구성)



* 국보연 : 미정 ---> TO BE Dstill-bert OR Mobile-bert 모델 (벤치마킹 테스트 후 적용예정)
* 사작사 : 국보연 모델을 확산예정 ---> TO BE Dstill-bert OR Mobile-bert 모델 (벤치마킹 테스트 후 적용예정)
* 육본isp :국보연 모델을 확산예정 ---> TO BE Dstill-bert OR Mobile-bert 모델 (벤치마킹 테스트 후 적용예정)
* 신한 : SVM (지도학습), ESOINN (비지도학습) ---> TO BE Dstill-bert OR Mobile-bert 모델 (벤치마킹 테스트 후 적용예정)
* 기타 비지도학습으로 esoinn을 대체할 모델 연구 필요



* 국보연 대시보드를 기준으로 앞으로 사작사, 육본, 엘지유플러스 등 확산 예정\


TO BE&#x20;

* &#x20;



***



<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>



개발환경 구성목표(To Be)

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

