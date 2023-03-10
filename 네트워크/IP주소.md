# IP 주소
인터넷 계층에서 쓰는 IP 주소

### ARP
***
IP 주소에서 ARP를 통해 MAC 주소를 찾아 MAC 주소를 기반으로 통신을 합니다. ARP(Address Resolution Protocol)란 IP 주소로부터 MAC 주소를 구하는 IP와 MAC 주소의 다리 역할을 하는 프로토콜입니다. ARP를 통해 가상 주소인 IP 주소를 실제 주소인 MAC 주소로 변환합니다. 반대과정은 RARP라고 합니다. ARP Request를 브로드캐스팅하여 주소에 맞는 대상의 주소를 유니캐스트로 받아 옵니다. 

### 홉바이홉 통신
***
IP 주소를 통해 통신하는 과정을 홉바이홉 통신이라고 합니다. 라우팅 테이블의 IP를 통해 시작 주소부터 시작하여 다음 IP로 계속해서 최종 목적지까지 도착하는 것을 의미합니다.

### 라우팅 테이블
***
송신지에서 수신지 까지 도달하기 위해 사용되며 라우터에 들어가 있는 목적지 정보들과 그 목적지로 가기 위한 방법이 들어 있는 리스트를 뜻합니다. 게이트웨이와 모든 목적지에 대해 해당 목적지에 도달하기 위해 거쳐야 할 다음 라우터의 정보를 가지고 있습니다.

### 게이트웨이 
*** 
게이트웨이는 서로 다른 통신망, 프로토콜을 사용하는 네트워크 간의 통신을 가능하게 하는 관문 역할을 하는 컴퓨터나 소프트웨어를 두루 일컫는 용어입니다. 서로 다른 네트워크상의 통신 프로토콜을 변환해주는 역할을 하기도 합니다.

### IP 주소 체계
***
IP 주소는 IPv4와 IPv6로 나뉩니다. IPv4는 32비트를 8비트 단위로 점을 찍어 표기합니다. IPv6는 64비트를 16비트 단위로 점을 찍어 표기합니다.

### 클래스 기반 할당 방식
***
A, B, C, D, E 다섯 개의 클래스로 구분하는 클래스 기반 할당 방식을 사용하고 있습니다. 앞에 있는 부분을 네트워크 주소, 뒤에 있는 부분을 컴퓨터에 부여하는 주소인 호스트 주소로 놓아서 사용합니다. A, B, C는 일대일 통신으로 사용되고 D는 멀티캐스트 통신, E는 앞으로 사용할 예비용으로 쓰는 방식입니다. 이 방식은 사용하는 주소보다 버리는 주소가 많은 단점이 있습니다. 이를 해소하기 위해 DHCP와 IPv6, NAT 방법이 있습니다.

### DHCP(Dynamic Host Configuration Protocol)
***
IP 주소 및 기타 통신 매개변수를 자동으로 할당하기 위한 네트워크 관리 프로토콜입니다. 인터넷에 접속할 때마다 자동으로 IP 주소를 할당할 수 있습니다. 많은 라우터와 게이트웨이 장비에 DHCP 기능이 있으며 이를 통해 대부분 가정용 네트워크에서 IP 주소를 할당합니다.

### NAT(Network Address Translation)
***
패킷이 라우팅 장비를 통해 전송되는 동안 패킷의 IP 주소 정보를 수정하여 IP 주소를 다른 주소로 매핑하는 방법입니다. IPv4 주소 체계만으로는 많은 주소들을 모두 감당하지 못하는 단점이 있는데 이를 해결할 수 있습니다. 공인 IP와 사설 IP를 나누어서 주소를 처리합니다.
* 공유기와 NAT : 여러 대의 호스트가 하나의 공인 IP 주소를 사용하여 인터넷에 접속할 수 있습니다.
* NAT를 이용한 보안 : 내부 네트워크에서 사용하는 IP 주소와 외부에 드러나는 IP 주소를 다르게 유지할 수 있기 때문에 내부 네트워크에 대한 어느 정도의 보안이 가능합니다.
* NAT 의 단점 : 실제로 접속하는 호스트 숫자의 따라 접속 속도가 느려질 수 있습니다.

### IP 주소를 이용한 위치 정보
***
IP 주소는 인터넷에서 사용하는 네트워크 주소이기 때문에 동 또는 구 까지 위치 추적이 가능합니다.