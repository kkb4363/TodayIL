# ip address

## InetAddress 클래스

- InetAddress 의 주요 메서드
- getAddress만 byte단위로 받고 나머지는 string으로 받는다.

1. getAddress() => InetAddress 객체의 ip 주소를 반환
2. getHostAdress() => IP 주소를 반환
3. getHostName() => 호스트 이름을 문자열로 반환
4. getCanonicalHostName() => fully qualified domain name을 반환

## Unicast(1:1)

- 1:1 통신을 말하며 Lan 통신에서 송신자의 mac과 수신자의 mac주소를 알 때 메시지를 전달함.
- 개인적이거나 고유한 리소스가 필요한 모든 네트워크 프로세스에서 사용될 수 있다.
- 단점은 대량으로 배포되는 특정 네트워크 응용 프로그램에서 유니캐스트로 데이터 전송을 할 경우, 각각의 네트워크 연결바마 호스트의 컴퓨터 리소스를 소비할 뿐만 아니라 각각 다른 네트워크 대역폭을 필요로 하기 떄문에 전송비용이 매우 높다.

## Broadcast(1:아무나)

- 정보 전달 과정에서 송신자는 누군지 확실하나 수신자를 특정하지 않았을 때, 네트워크에 모든 서버에게 정보를 알려야 할 때, 라우터 끼리 정보를 교환하거나 새로운 라우터를 찾을때 이 방식을 사용함.

## Multicast(1:n)

- 한번의 송신으로 메시지나 정보를 목표한 여러 컴퓨터에 전송하는 것
- 수신자를 그룹화하여 해당 그룹에 해당하는 수신지만 유니캐스트+브로드캐스트한다고 보면 된다.

## link local address란?

- 링크 로컬 주소는 이름 그대로 해당 링크 에서만 사용되는 주소이다.
- 내부 network에서 서로 통신하기 위해 사용하며, 주로 제어 메시지 교환 용도로 많이 사용됨.(나만 쓸 수 있는거, 외부는 모름)

### link란?

- server1과 server2가 네트워크로 연결되어 있으면 해당 server는 link되어있다라고 호칭하기도 함.
- 여러대의 server가 서로 연결되어 링크를 형성하고 있을 수도 있는데 이런 구조를 network라고 부르기도 하는 것.
- 즉 link란 network 개념의 일부로 서로 연결되어 있다는 것을 의미함.

### global address란?

- link address , site local address가 아닌 것들이다.
- 공유기가 갖고 있는 ip address가 global이다(외부에서 쓸 수 있는거)
- 공유기 내부용은 192.168.0.1 이런거임.

## 용어

- eth : 이더넷
- wlan : 무선랜
- ppp : 1대1 통신 point to point
- spemcheck : ip주소가 스팸인지 확인하는 것

## spemcheck 원리

1. 192.168.0.1이 스팸주소인지 확인하려면
2. 1.0.168.192이런식으로 거꾸로 뒤집음
3. ip주소 뒤에 zen.spem~.org주소를 붙힘.
4. getbyname으로 서버한테 물어봄.
5. 스팸이 아닐 시 unknown 호스트가 나옴(주소가 없어서)
6. 스팸일 시 리턴 주소가 옴.
