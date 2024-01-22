# Threat Scoring

## 사이버 위협을 자동으로 평가하는 Threat Scoring 기술

사이버 위협을 자동으로 평가하는 Threat Scoring 기술을 개발하여 보안전문가가 탐지된 내역을 효율적으로 분석 및 대응할 수 있도록 ip를 Threat Score 기준으로 정렬하여 화면에 표시한다. Threat Scoring 기법은 보안장비, 인공지능 분석 결과, 그리고 외부 평판 정보를 바탕으로 해당 ip에 대한 속성을 분석하고 최종 점수를 계산한다.



## 참고자료

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

1\) src\_ip는 분석 대상 출발지 ip를 의미&#x20;

<figure><img src="../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

2\) Black list와 white list에 해당 src\_ip 존재 여부 확인&#x20;

<figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

3\) 해당 src\_ip에 각 속성 별 점수 계산 진행&#x20;

<figure><img src="../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

4\) 속성 별 계산된 점수를 합의&#x20;

각 속성 별 계산된 점수는 최소 값 0, 최대 값 1이다. 따라서 속성 총 개수가 6개이므로 최대 점수가 6으로 나올 수 있다

5\) 합의 결과를 숫자 0-100 사이로 변환 하기 위하여 이차 함수 사용&#x20;

<figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

6\) 최종 결과를 0-100 사이로 표시하며, 해당 src\_ip가 black list와 white list에 동시에 들어가 있을 경우 검증 필요 대상자로 표시

<figure><img src="../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

### 사이버 위협 시각화 정보를 통한 위협 확인 (예시)

<figure><img src="../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

### 가산화와 AI를 통한 프로파일링(예시)

<figure><img src="../../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>



## K사 N시스템 위협스코어링&#x20;

<figure><img src="../../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>



## 국가보안기술연구소 위협스코어링

<figure><img src="../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

기존 경보를 통한 대응 시간과 가산화 기능을 통한 대응 시간 (예시)

<figure><img src="../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>



### nhn cloud 참고자료, Criminal IP for FDS

별도의 로그 시스템 없이 결제 또는 회원가입, 로그인을 필요로 하는 서비스에 실시간으로 접속하는 모든 IP 주소 이상 여부를 식별합니다.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

* 접속 IP 주소 실시간 로그 모니터링
* 접속 IP 주소 위협 스코어링
* 접속 IP 주소 위치 정보
* Blacklist IP 식별
* VPN IP 식별
* 클라우드 IP 식별
* 서버 IP 식별
* Tor, Proxy IP 식별



{% embed url="https://www.nhncloud.com/jp/marketplace/security/criminal-ip-for-fds?lang=ko" %}
