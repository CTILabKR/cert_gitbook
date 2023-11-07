# 수집서버고도화작업



개요

수집된 데이터를 원하는 형태로 가공 및 분석(GPU)서버로 전달하기 위함

파일형식은 Json, XML, CSV 등 형식으로 함



### JSON (JavaScript Object Notation) <a href="#json-javascript-object-notation" id="json-javascript-object-notation"></a>

* 데이터 교환 포맷
* JavaScript에서 객체를 만들 때 표현하는 사용식을 의미
* 사람과 기계 모두 이해하기 쉽고 용량이 작음
* key-value 형태 or array, list 형태

### XML (eXtensible Markup Language) <a href="#xml-extensible-markup-language" id="xml-extensible-markup-language"></a>

* html과 비슷한 마크업 언어
* 데이터를 보여주기보다는 전송, 배포할 목적으로 사용\
  사용자가 태그명을 임의로 만들어서 사용



pcap 파서 개발 (오프소스 활용)



Fleunt Bit 설치 및 셋팅

Fleunt Bitdmf 찾게 된 이유는 모니터링 오프소스 중 리얼타임 로그를 얻기 위한 수집기를 찾던중에 Fleunt Bit을 찾게 되었으며, 시스템 정보들이나 로그들을 리얼타임으로 얼마나 가볍게 빠르고 정확하게 모아서 쌓는가가 초점임. 또한 pcap, Tcpdump 파일형태의 패킷을 실시간 로그를 얻기 위함이다.

공식사이트 : [https://fluentbit.io/](https://fluentbit.io/)

공식메뉴얼 : [https://docs.fluentbit.io/manual/](https://docs.fluentbit.io/manual/)



<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

지원플랫폼

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

CentOS 패키지 설치





