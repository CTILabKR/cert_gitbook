# 국가보안기술연구소

## 01) [화면설계서](https://docs.google.com/presentation/d/1-K1-ukUFHOR9UJDNIJKomVX3K8SXQTF6/edit?usp=drive\_link\&ouid=101332176627069382597\&rtpof=true\&sd=true)

## 02) [화면설계시\_보안검토의견 작성](https://docs.google.com/presentation/d/1-LOFPzaLq0i2-inhTFxheiz1cYi6NXw76U3mULkrWrw/edit?usp=drive\_link)



## 03) 수집기 하드웨어 구매

11/10일 수집기 하드웨어 구매신청서 결재완료

11/13일 경영전략팀에 발주관련 자료요청/회신

&#x20;           ktnf 김상헌 부장님에게 발주요청 (딜리버리 3\~4주 소요/ 11월말, 12월 초)

12월 8일

* GPU 서버(1), AI모델과 에어플로 등이 탑재된 분석장비 납품 //dmz영역내
* 수집  서버(1), 수집데이터 전처리용, 국보연 제공서버   //dmz영역내
* 수집기하드웨어(1),  수집소프트웨어가 설치된 수집장비 납품   //dmz영역내

12월 15일

* 웹산출물(대시보드포함) 납품
* 관리웹서버(국보연 제공서버)  //관리영역내

12월 21일 납기(조달계약)

*



## 04) 위협스코어링 계산과정 (세부 로직 추가(수정), 11/13)

{% embed url="https://docs.google.com/spreadsheets/d/1qoJcORCunPk8XXx0UqF8Ci6jp5OAqMg-jYXuVAFKPoU/edit?usp=drive_link" %}

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>



## 05) SMTP 보안



허니팟 구성 : 메일서버 구축 (Docker 기반) 하기  + 그누보드, 라이믹스, 워드프레스 연결하기  [CTILAB ORG](http://127.0.0.1:5000/u/arkk37VbsDMtxxYU6SwCiDTyjrC2 "mention")

{% embed url="https://www.wsgvet.com/home/677" %}

{% embed url="https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/07-Input_Validation_Testing/10-Testing_for_IMAP_SMTP_Injection" %}

{% embed url="https://net123.tistory.com/518" %}

{% embed url="https://www.hahwul.com/cullinan/email-injection/" %}



이메일 주소 구조는 로컬파트와 @(At), 도메인으로 구성되어 있다.

```
이메일 주소 : foobar@gmail.com
로컬 파트 : foobar
도메인 : gmail.com
```

SMTP는 인터넷을 통해 이메일을 발송하고 수신하기 위한 프로토콜(Protocol)이다. \
SMTP는 텍스트 기반의 프로토콜이기 때문에 구조가 간단하며 읽기 쉽다.\
아래 통신예시에서 발송 서버는 'C', 수신 서버는 'S'이다.

```
C: telnet www.example.com 25
S: 220 smtp.example.com ESMTP Postfix
C: HELO relay.example.com
S: 250 smtp.example.com, I am glad to meet you
C: MAIL FROM:<bob@example.com>              <-- (1)
S: 250 Ok
C: RCPT TO:<alice@example.com>
S: 250 Ok
C: DATA                                     <-- (2)
S: 354 End data with <CR><LF>.<CR><LF>
C: From: "Bob" <bob@example.com>    <-- (3)
C: To: Alice <alice@example.com>
C: Date: Tue, 15 January 2008 16:02:43 -0500
C: Subject: Test message
C: 
C: Hello Alice.
C: This is a test message with 5 header fields and 4 lines in the message body.
C: Your friend,
C: Bob
C: .
S: 250 Ok: queued as 12345
C: QUIT                                     <-- (4)
S: 221 Bye
```

편지를 봉투에 넣어 보내는 것처럼 SMTP에도 편지와 봉투로 구성된다. (편지: Letter, 봉투: Envelope)

* 위의 통신에서 (1)에서 (2)까지 봉투, (3)에서 (4)까지가 편지 부분이라 볼 수 있다.
* 봉투는 메일을 읽는 수신자에게 전달되지 않는다. 따라서 **수신자는 봉투의 내용을 확인할 수 없다.**
* 위에서 발신자 주소는 두번등장한다. \
  `MAIL FROM`, `FROM` 두 발신자 주소는 수신 서버에서 각기 다르게 사용된다.
  * `MAIL FROM`는 **SPF 인증에서 사용된다.** \
    일반적으로 편지의 헤더인 Return-Path 주소로 추가되어 반송 메일을 수신하는 주소로 사용된다.
  * `FROM`은 수신자가 메일을 읽을 때 볼 수 있는 주소이다. \
    **DKIM 인증에서 사용된다.**
* `MAIL FROM`, `FROM`는 일치하지 않아도 된다. \
  예를 들면, 실제 발신자 주소와 다른 반송 메일만 수신하는 이메일 주소를 MAIL FROM에 설정해 모든 반송 메일을 하나의 이메일로 수집하고 처리할 수 있다.
* 편지(Letter)에 적혀있는 `To`와 봉투(Envelope)에 적혀있는 `To`는 다를 수 있다. \
  예를 들어 cc 혹은 bcc인 사람에게 메일을 보내야 할 때 편지의 `To`는 모두 동일하지만 봉투에 적혀 있는 `To`는 cc혹은 bcc의 메일 주소가 적혀있을 수 있다는 것이다.

## 공격유형\_이메일 스푸핑

```
이메일 스푸핑은 피해자가 신뢰할 수 있는 인물, 웹 사이트, IP, 이메일 주소 등으로 위장하는 것이다.

C: telnet www.example.com 25
S: 220 smtp.example.com ESMTP Postfix
C: HELO relay.example.com
S: 250 smtp.example.com, I am glad to meet you
C: MAIL FROM:<bob@trust.com>    <-- 실제로는 'spoofing.com'이지만, 'trust.com'이라고해서 수신 서버를 속임
S: 250 Ok
C: RCPT TO:<alice@example.com>
S: 250 Ok
C: DATA
S: 354 End data with <CR><LF>.<CR><LF>
C: From: "Bob" <bob@trust.com>  <-- 같은 방법으로 수신자를 속임
C: To: Alice <alice@example.com>
...
```

## 공격유형\_이메일 발송 SMTP 서버 위조

```
MAIL FROM에 실제와 다른 신뢰할만한 발신자 주소를 입력해 
이메일 수신 SMTP 서버를 속이는 공격이다.

수신 서버가 속아 스푸핑 된 이메일을 수신자에게 전달하면, 
수신자는 속아 피싱이나 파밍, 바이러스에 감염될 수 있다. 
SPF로 예방을 할 수 있지만 완벽하지 않아 DKIM, DMARC까지 적용해야 안전하다.
```

## 공격유형\_발신자 주소 위조

```
FROM에 실제와 다른 수신자가 신뢰할만한 발신자 주소를 입력해 수신자를 속이는 공격방법이다. 
SPF로 막을 수 없으며, DKIM과 DMARC까지 적용해야 안전하다.
```



## SPF (Sender Policy Framework)

SPF 레코드라고 부르는 이메일 발송 SMTP서버 정보를 \
**이메일 발송 도메인 DNS(Domain Name Server)에 등록하고** \
**이메일 수신 SMTP서버가 DNS에 공개된 IP정보에 실제 메일을 발송한 SMTP 서버의 IP가 속한지 확인하는 인증 기술이다.** 즉 메일을 실제로 보내는 발송서버의 IP와 DNS에 등록되어 있는 해당 도메인의 공개 IP와 비교하여 검증하는 인증방법이다.



SMTP 송신 서버에서 수신서버로 보낼 때 흐름은 아래와 같다.\
\
![](<../../.gitbook/assets/image (3).png>)

1. 먼저 발신 서버의 SPF 레코드를 DNS에 등록을 합니다.
2. 발신 서버에서 메일을 수신서버로 전송을 합니다.
3. 수신서버는 `MAIL FROM`의 SPF 레코드를 DNS서버를 통해 조회 합니다.
4. 조회된 결과와 발신 서버의 IP와 비교하여 이 후 처리를 하게 됩니다.

SPF의 한계

```
SPF를 이용해 발송 서버 스푸핑을 막을 수 있었다. 
하지만 공격자가 SPF 레코드가 등록된 도메인을으로 MAIL FROM을 변조하면 
수신 서버는 SPF 레코드를 확인해보고 발송 서버를 신뢰하게 된다.

C: telnet www.example.com 25
S: 220 smtp.example.com ESMTP Postfix
C: HELO relay.example.com
S: 250 smtp.example.com, I am glad to meet you
C: MAIL FROM:<bob@spoofing.com>    <-- SPF 레코드가 등록된 From과 다른 도메인을 사용
S: 250 Ok
C: RCPT TO:<alice@example.com>
S: 250 Ok
C: DATA
S: 354 End data with <CR><LF>.<CR><LF>
C: From: "Bob Example" <bob@trust.com>  <-- 수신자는 MAIL FROM이 아닌 From을 보기때문에 속을 수 있음
C: To: Alice Example <alice@example.com>
...

공격을 막기 위해서는 MAIL FROM과 From을 비교하고 
이메일 내용이 위조 되지 않았는지 확인하는 인증 방법이 필요하기에 등장을 하게 되는 것이 DKIM 및 DMARC이다.
```



## DKIM

DKIM은 이메일 인증 방법 중 하나로 \
**수신 서버에서 수신된 이메일이 위변조 되지 않았는지 디지털 서명을 이용해 검증하는 기술이다.**

발신 서버는 이메일 발송 시 이메일 발송자, 수신자, 제목, 내용 등을 **비밀 키로 서명한 후** \
**이 서명 값을 DKIM-Signature 헤더에 추가한다.**

수신 서버는 DKIM-Signature헤더 내 도메인 (d=) **DNS에 공개된 공개 키와** \
**서명 알고리즘 정보 등이 담긴 DKIM 레코드를 조회한 후 이 값들을 이용해** \
**수신된 이메일 DKIM-Signature 헤더의 디지털 서명을 검증한다.**\


![](<../../.gitbook/assets/image (1) (1).png>)

1. 발신서버에서 메일을 보낼 때 발신자, 수신자, 제목, 내용 등을 비밀 키로 서명을 한다.
2. 서명 값을 DKIM-Signature 헤더에 추가하여 메일을 발송
3. 수신 서버는 DKIM-Signature 헤더 안에 있는 도메인을 가지고 DNS서버에 공개된 공개 키와 서명 알고리즘을 통해 DKIM 레코드를 조회하고 이 값들을 이용하여 DKIM-Signature 서명을 검증.

## DKIM의 인증 한계 <a href="#dkim" id="dkim"></a>

DKIM 인증 시 DKIM-Signature의 도메인을 사용하기 때문에 \
여전히 `From`를 위조한 이메일 스프핑 공격을 막기에는 부족하다.

DKIM은 **이메일 내용의 위변조 여부를 인증할 뿐 DKIM-Signature 도메인과** \
**`MAIL FROM`의 관계는 검증하지 않는다.**

DKIM의 인증 한계에 대한 예제이다.

```
C: telnet www.example.com 25
S: 220 smtp.example.com ESMTP Postfix
C: HELO relay.example.com
S: 250 smtp.example.com, I am glad to meet you
C: MAIL FROM:<bob@spoofing.com>    <-- SPF 레코드가 등록된 From과 다른 공격자 도메인을 사용
S: 250 Ok
C: RCPT TO:<alice@example.com>
S: 250 Ok
C: DATA
S: 354 End data with <CR><LF>.<CR><LF>
C: DKIM-Signature: v=1; a=rsa-sha256; d=spoofing.com; s=brisbane; <-- 공격자 도메인과 지정자
      c=simple; q=dns/txt; i=@eng.example.net;
      t=1117574938; x=1118006938;
      h=from:to:subject:date;
      bh=MTIzNDU2Nzg5MDEyMzQ1Njc4OTAxMjM0NTY3ODkwMTI=;
      b=dzdVyOfAKCdLXdJOc9G2q8LoXSlEniSbav+yuU4zGeeruD00lszZVoG4ZHRNiYzR
C: From: "Bob Example" <bob@trust.com>  <-- 수신자는 MAIL FROM이 아닌 From을 보기때문에 속을 수 있음
C: To: Alice Example <alice@example.com>
...
```

이러한 공격을 막기 위해 DMARC를 이용하며 DMARC는 \
SPF, DKIM 얼라인먼트(Alignment)라는 기능을 사용한다. \
DMARC는 **DKIM-Signature의 도메인과 MAIL FROM, From의 관계를 검증하기 때문에** \
**위와 같은 공격을 막을 수 있다.**



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

