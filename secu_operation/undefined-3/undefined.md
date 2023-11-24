# 수집서버 고도화작업

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

**pcap 파서 개발 (오프소스 활용)**

{% embed url="https://github.com/fluent/fluent-bit" %}

{% embed url="https://github.com/enukane/fluent-plugin-pcapng" %}

{% embed url="https://github.com/topics/pcap-parser" %}

Fleunt Bit 설치 및 셋팅

Fleunt Bitdmf 찾게 된 이유는 모니터링 오프소스 중 리얼타임 로그를 얻기 위한 수집기를 찾던중에 Fleunt Bit을 찾게 되었으며, 시스템 정보들이나 로그들을 리얼타임으로 얼마나 가볍게 빠르고 정확하게 모아서 쌓는가가 초점임. 또한 pcap, Tcpdump 파일형태의 패킷을 실시간 로그를 얻기 위함이다.

fluentbit은 내부적으로 input, filter, output, router 등 다양한 설정이 존재하고 이를 조정하여 다양한 기능을 수행할 수 있음.

공식사이트 : [https://fluentbit.io/](https://fluentbit.io/)

공식메뉴얼 : [https://docs.fluentbit.io/manual/](https://docs.fluentbit.io/manual/)

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

지원플랫폼

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

CentOS 패키지 설치 참조

```
//** /etc/yum.repos.d/td-agent-bit.repo 추가

# cat<< EOF >/etc/yum.repos.d/td.repo
[treasuredata]
name=TreasureData
baseurl=http://packages.treasuredata.com/3/redhat/\$releasever/\$basearch
gpgcheck=1
gpgkey=https://packages.treasuredata.com/GPG-KEY-td-agent
EOF
```

소스빌드 참조

```
//** 소스다운로드

$ git clone https://github.com/fluent/fluent-bit


빌드 방법 참조)
https://github.com/fluent/fluent-bit-docs/blob/master/installation/build_install.md


* 에러
Could NOT find GTest (missing: GTEST_LIBRARY GTEST_MAIN_LIBRARY)Could NOT find Journald (missing: JOURNALD_LIBRARY JOURNALD_INCLUDE_DIR)
 
--> yum install -y libsystemd-dev 

CMake Error at /usr/share/cmake/Modules/FindFLEX.cmake:116
--> cmake3 설치로 해결

centos Could NOT find ZLIB
--> libzlib-devel 설치

Could NOT find GTest (missing: GTEST_LIBRARY GTEST_INCLUDE_DIR GTEST_MAIN_LIBRARY)
--> 우분투는 libgtest-dev 설치, Cent는 다음 글을 참조

$ wget http://www.cmake.org/files/v3.6/cmake-3.6.1.tar.gz
$ tar -zxvf cmake-3.6.1.tar.gz
$ cd cmake-3.6.1
$ ./bootstrap
$ make
$ make install
# \cp를 한 이유는 -f 가 먹히지 않아서 그렇다.
# cp에 대한 alias를 확인해 보면 -i가 붙어 있는것을 알 수 있다.
# $alias | grep cp
# alias cp='cp -i'
# 이런 경우 \cp를 하면 alias값이 무시된다.
$ \cp -f ./bin/cmake ./bin/cpack ./bin/ctest /bin
$ cmake -version
cmake version 3.6.1

CMake suite maintained and supported by Kitware (kitware.com/cmake).
```

테스트 환경 구축 및 테스트 진행

* 업무용 노트북에 가상 환경 구축하여 테스트 진행 예정
