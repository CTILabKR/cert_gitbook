# 국가보안기술연구소

## 01) [화면설계서](https://docs.google.com/presentation/d/1-K1-ukUFHOR9UJDNIJKomVX3K8SXQTF6/edit?usp=drive\_link\&ouid=101332176627069382597\&rtpof=true\&sd=true)

## 02) [화면설계시\_보안검토의견 작성](https://docs.google.com/presentation/d/1-LOFPzaLq0i2-inhTFxheiz1cYi6NXw76U3mULkrWrw/edit?usp=drive\_link)



## 03) 수집기 하드웨어 구매

11/10일 수집기 하드웨어 구매신청서 결재완료

11/13일 경영전략팀에 발주관련 자료요청/회신

&#x20;           ktnf 김상헌 부장님에게 발주요청 (딜리버리 3\~4주 소요/ 11월말, 12월 초)



## 04) 위협스코어링 계산과정 (세부 로직 추가(수정), 11/13)

{% embed url="https://docs.google.com/spreadsheets/d/1qoJcORCunPk8XXx0UqF8Ci6jp5OAqMg-jYXuVAFKPoU/edit?usp=drive_link" %}

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>



## 05) SMTP 프로토콜 공격유형

{% embed url="https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/07-Input_Validation_Testing/10-Testing_for_IMAP_SMTP_Injection" %}

### 시스템이 악의 있거나 요청하지 않은 메일(스팸)의 공격을 받지 않도록 방지하려면 SMTP(Simple Mail Transfer Protocol) 액세스를 제어해야 합니다.

SMTP 클라이언트가 시스템에 액세스할 수 있도록 허용하려면 아래의 태스크를 수행하여 시스템을 공격으로부터 보호해야 합니다.

* 가능한 경우, 시스템 분배 디렉토리에서 \*ANY \*ANY 항목을 사용하지 마십시오. 시스템에 \*ANY \*ANY 항목이 없으면 누군가가 SMTP를 사용하여 시스템 또는 네트워크를 압도하는 시도를 하기가 더 어렵습니다. 사용자의 보조 기억장치가 사용자의 시스템을 통해 다른 시스템으로 라우트되는 원하지 않는 메일로 채워지면 사용자의 시스템 또는 네트워크가 압도됩니다.
* 보조 기억장치 풀(ASP)에 적절한 임계 제한을 설정하여 원하지 않는 오브젝트로 시스템이 압도되지 않도록 사용자를 보호하십시오. 시스템 서비스 툴(SST) 또는 전용 서비스 툴(DST)을 사용하여 ASP의 임계값을 표시하고 설정할 수 있습니다.
* \*SDD 디렉토리 유형에 대해 사전시작 작업 항목 변경(CHGPJE) 명령을 사용하여 작성할 수 있는 사전시작 작업의 최대 수를 조정하십시오. 이에 따라 서비스 공격 거부 중에 작성되는 작업의 수가 제한됩니다. 최대 임계값의 디폴트는 256입니다.
* \*SMTP 및 \*SMTPMSF 디렉토리 유형에 대해 SMTP 등록정보 패널의 옵션을 통해 송신할 수 있는 전자 우편의 최대 수를 조정하십시오.
* 릴레이와 연결을 제한하면 외부인이 사용자의 연결을 사용하여 요청하지 않은 전자 우편(스팸)을 송신하지 못하도록 방지할 수 있습니다.
* i 6.1 이상을 실행하는 시스템에서는 인증이 전자 우편을 송신하도록 요구하여 스팸을 방지할 수 있습니다. 리모트 서버에서 인증을 요구하는 경우, 사용자는 사용자의 로컬 서버에 인증을 설정할 수 있습니다.
* i 7.2 이상을 실행 중인 시스템에서는 SSL/TLS가 인증을 사용하도록 요구할 수 있습니다. 더 이전의 릴리스에서는 인증 없이 SSL/TLS를 허용하지 않습니다. 또한 SSL/TLS 전용 포트를 작동 불가능으로 만들 수도 있습니다.



SMTP 동작

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

SMTP is one of the most commonly used protocols in delivering email messages over the Internet. Clients use it to send messages to servers, and servers utilize it to forward messages to recipients.

For example, when you send an email to a client, it gets sent to your mail server via SMTP. Your [SMTP relay server](https://www.techslang.com/what-is-smtp-relay-is-it-important/) forwards the email to the recipient’s mail server, again using SMTP. The recipient’s mail server would then forward the message to your client’s email address. This process is visualized by the image below



SMTP 공격

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

An SMTP attack is any exploitation of your SMTP server that enables attackers to gain unauthorized access to it. When an SMTP hack occurs, attackers can see the email addresses stored on your server and send messages to them while pretending to be you. The recipients, which can be clients or friends, will think that the email is from you since the hackers used your email address.

Aside from sending phishing and [spam emails](https://www.techslang.com/definition/what-is-spam/), an SMTP hack can also give way to denial-of-service (DoS) attacks. Hackers can use your SMTP server to send a massive number of emails to other servers, effectively drowning the targets until they crash.



SMTP 취약점

* 피싱 & 멀웨어
* **Physical access**
* **Lack of encryption**

SMTP 해킹에 대해 보호 방법

Adding security layers to your SMTP server helps keep it safe from unauthorized access. Secure Sockets Layer (SSL) and Transport Layer Security (TLS), more commonly known as SSL/TLS, is a standard method of encrypting data sent through SMTP.

For utmost security, continuous education about phishing and malware should be advocated in organizations. Users should be aware of the current phishing methods that attackers employ. Bring Your Own Device (BYOD) policies must be implemented with caution and clear guidelines to avoid risks associated with lost or stolen devices.



{% embed url="https://www.datanet.co.kr/news/articleView.html?idxno=160226" %}

