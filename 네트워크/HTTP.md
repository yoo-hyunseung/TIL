# HTTP
HTTP는 애플리케이션 계층으로서 웹 서비스 통신에 사용됩니다. HTTP/1.0부터 시작해서 지금은 HTTP/3 이다. 

### HTTP/1.0
***
기본적으로 한 연결당 하나의 요청을 처리하도록 설계하였습니다. 이는 RTT 증가를 불러오게 되었습니다. 서버로 부터 파일을 가져올 때마다 TCP 3-way handshake를 계속해서 열어야 하기 때문에 RTT가 증가하는 단점이 있습니다.

> RTT : 패킷이 목적지에 도달하고 나서 다시 출발지로 돌아오기까지 걸리는 시간이며 패킷 왕복 시간
<br>해결 방안 : 이미지 스플리팅, 코드 압축, 이미지 Base64 인코딩을 사용

> 이미지 스플리팅 : 많은 이미지가 합쳐 있는 하나의 이미지를 다운로드받고, 이를 기반으로 background-image의 position을 이용하여 이미지를 표기하는 방법

> 코드 압축 : 코드를 압축해서 개행 문자, 빈칸을 없애서 코드의 크기를 최소화하는 방법

> 이미지 Base64 인코딩 : 이미지 파일을 64진법으로 이루어진 문자열로 인코딩하는 방법입니다. 서버와의 연결을 열고 이미지에 대해 서버에 HTTP 요청을 할 필요가 없다는 장점이 있습니다. 하지만 Base64 문자열로 변경시 37% 정도 크기가 더 커지는 단점이 있습니다.

### HTTP/1.1
***
매번 TCP 연결을 하는 것이 아니라 한 번 TCP 초기화를 한 이후에 keep-alive라는 옵션으로 여러 개의 파일을 송수신 할 수 있습니다. 한 번 TCP 3-way handshake가 발생하면 그다음부터 발생하지 않습니다. 하지만 문서 안에 포함된 다수의 리소스(이미지, css파일, script파일)를 처리하려면 요청할 리소스 개수에 비례해서 대기 시간이 길어지는 단점이 있습니다.

> HOL Blocking : 네트워크에서 같은 큐에 있는 패킷이 그 첫 번째 패킷에 의해 지연될 때 발생하는 성능 저하 현상을 말합니다.

> 무거운 헤더 구조 : HTTP/1.1의 헤더에는 쿠키 등 많은 메타데이터가 들어 있고 압축이 되지 않아 무겁습니다.

### HTTP/2
***
SPDY 프로토콜에서 파생된 HTTP/1.x 보다 지연 시간을 줄이고 응답 시간을 더 빠르게 할 수 있으며 멀티플렉싱, 헤더 압축, 서버 푸시, 요청의 우선순위 처리를 지원합니다.

> 멀티 플랙싱 : 여러 개의 스트림을 사용하여 송수신하다는 것입니다. 이를 통해 특정 스트림이 손실되었다고 하더라도 해당 스트림에만 영향을 미치고 나머지 스트림은 멀쩡하게 동작할 수 있습니다.

> 스트림 : 시간이 지남에 따라 사용할 수 있게 되는 일런의 데이터 요소를 가리키는 데이터 흐름

> 헤더 압축 : 허프만 코딩 압축 알고리즘을 사용하는 HPACK 압축 형식을 가집니다.

> 허프만 코딩 : 문자열을 문자 단위로 쪼개 빈도수를 세어 빈도가 높은 정보는 적은 비트 수를 사용하여 표현하고, 빈도가 낮은 정보는 비트 수를 많이 사용하여 표현해서 전체 데이터의 표현에 필요한 비트양을 줄이는 원리입니다.

> 서버 푸시 : 클라이언트 요청 없이 서버가 바로 리소스를 푸시할 수 있습니다. html에는 css 나 js 파일이 포함되기  마련인데 html을 읽으면서 그 안에 들어 있던 css파일을 서버에 푸시하여 클라이언트에 먼저 줄 수 있습니다.

### HTTPS
***
HTTP/2 는 HTTPS 위에서 동작합니다. HTTPS는 애플리케이션 계층과 전송 계층 사이에 신뢰 계층인 SSL/TLS 계층을 넣은 신뢰할 수 있는 HTTP 요청을 말합니다.

### SSL/TLS
***
전송 계층에서 보안을 제공하는 프로토콜입니다. 클라이언트와 서버가 SSL/TLS를 통해 제3자가 메시지를 도청하거나 변조하지 못하도록 합니다. 보안 세션을 기반으로 데이터를 암호화하며 보안 세션이 만들어질 때 인증 메커니즘, 키 교환 암호화 알고리즘, 해싱 알고리즘이 사용됩니다.
 ### 보안 세션
 ***
 보안이 시작되고 끝나는 동안 유지되는 세션을 말하고, SSL/TLS는 handshake를 통해 보안 세션을 생성합니다. 클라이언트와 서버와 키를 공유하고 이를 기반으로 인증, 인증 확인 등의 작업이 일어나는 단 한 번의 RTT가 생긴 후 데이터를 송수신하는 것을 볼 수 있습니다. 클라이언트에서 사이퍼 슈트를 보내 서버와 해싱 알고리즘 등으로 송수신이  시작됩니다.

 > 사이퍼 슈트 : 프로토콜, AEAD 사이퍼 모드, 해싱 알고리즘이 나열된 규약을 의미합니다.

 > AEAD 사이퍼 모드(Authenticated Encryption with Associated Data) : 데이터 암호화 알고리즘이다. 

 > 인증 메커니즘 : CA(Certificate Authorities)에서 발급한 인증서를 기반으로 이루어집니다.

 > 암호화 알고리즘 : 키 교환 암호화 알고리즘으로는 대수곡선 기반의 ECDHE(Elliptic Curve Diffe-Hellman Ephermeral) 또는 모듈식 기반 DHE(Diffe-Hellman Ephermeral)를 사용 합니다.

 > 디피-헬만 키 교환 알고리즘 : 암호화 알고리즘은 암호키를 교환 하는 하나의 방법입니다.<Br>
 y = g^x mod p<br>
 식에서 g와 x와 p를 안다면 y는 구하기 쉽지만, g와 y와 p만 안다면 x는 구하기 어렵다는 원리에 기반한 알고리즘입니다.
<br>클라이언트와 서버 모두 개인키와 공개키를 생성하고 서로에게 공개키를 보내고 공개키와 개인키을 결합하여 PSK(사전 합의된 비밀키)가 생성된다면, 악의적인 공격자가 개인키 또는 공개키를 가지고도 PSK가 없기 때문에 아무것도 할 수 없게 됩니다.

> 해싱 알고리즘 : 데이터를 추정하기 힘든 더 작고, 섞여 있는 조각으로 만드는 알고리즘입니다. 

> SHA-256 알고리즘 : 해시 함수의 결괏값이 256비트인 알고리즘이며 비트 코인을 비롯한 블록체인 시스템에서도 씁니다. 해싱을 해야 할 메시지에 1을 추가하는 등 전처리를 하고 전처리된 메시지를 기반으로 해시를 반환합니다.

### SEO에도 도움이 되는 HTTPS
***
SEO(Search Engine Optimization)는 검색엔진 최적화를 뜻합니다. 검색엔진으로 웹 사이트를 검색했을때 그 결과를 페이지 상단에 노출시켜 많은 사용자가 볼 수 있도록 최적화 하는 방법을 의미합니다.

* 캐노니컬 설정 
```html
<link rel="canonical" .....>
```
사이트 link에 캐노니컬 설정을 해야합니다.

* 메타 설정 
```html
<meta .....>
<meta .....>
<meta .....>
```
html 파일의 가장 윗부분인 메타를 잘 설정해야 합니다.

* 페이지 속도 개선
구글의 PageSpeedInsight로 가서 자신의 서비스의 리포팅을 주기적으로 받으며 관리할 수 있습니다.

* 사이트맵 관리 
사이트맵(sitemap.xml)을 정기적으로 관리하는 것은 필수 입니다.

### HTTPS 구축 방법
***
크게 3가지 방법이 있습니다.
* 직접 CA에서 구매한 인증키를 기반으로 HTTPS 서비스를 구축
* 서버 앞단의 HTTPS를 제공하는 로드밸런서를 둬서 구축
* 서버 앞단에 HTTPS를 제공하느 CDN을 둬서 구축

### HTTPS/3
***
QUIC이라는 게층 위에서 작동합니다. UDP 기반으로 작동됩니다. 멀티 플랙싱을 지원하며 초기 연결 설정 시 지연 시간 감소라는 장점이 있습니다.

> 초기 연결 설정 시 지연 시간 감소 : UDP 기반이기 때문에 3-way handshake과정은 거치지 않습니다. QUIC은 첫 연결 설정에 1-RTT만 소요됩니다. 또한 순방향 오류 수정 메커니즘(FEC, Forword Error Correction)이 적용되었습니다. 전송한 패킷이 손실되었다면 수신 측에서 에러를 검출하고 수정하는 방식이며 열악한 네트워크 환경에서도 낮은 패킷 손실률을 자랑합니다.
