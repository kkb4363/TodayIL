# URI (Uniform Resource Identifier, 통합 자원 식별자)

- 인터넷에 있는 자원을 나타내는 유일한 주소.
- 하위개념으로 URL , URN이 있다.

# URL (Uniform Resource Locator)

- 네트워크 파일의 위치를 알려주는 것
- 흔히 웹사이트 주소로 알고 있지만, URL은 웹사이트 주소 뿐만 아니라 컴퓨터 네트워크상의 자원을 모두 나타낼 수 있다.

# URN (Uniform Resource Name, 통합 자원 이름)

- 그냥 이름이라고 생각하면 됨.
- urn:scheme을 사용하는 URI를 위한 역사적인 이름이다. URN은 영속적이고, 위치에 독립적인 자원을 위한 지시자로 사용하기 위해 1997년도 RFC 2141문서에서 정의됨.

## URL,URI

- www.hanbat.ac.kr 이 부분을 URL은 HOST라고 부르고 , URI는 authority,scheme이라고 부른다.
- URI는 책 , 이 책이 몇층에 있는지 알려주는 것을 URL

## URL 구조

- URL의 구조는 http: (프로토콜 식별자) 와 자원 이름(www.naver.com)으로 나뉜다.
- 자원 이름은 다시 www.myhom.net/index.html:8080 다음과 같은 형식으로 구성되는데
- 여기서 www.myhome.net은 호스트 이름 , index.html은 파일 이름 , :8080은 포트번호로 나뉜다.

## URL 클래스의 주요 메소드

- getFile() : 이 URL의 파일 이름 리턴
- getHost() : 이 URL의 호스트 이름 리턴
- getPath() : 이 URL의 경로 부분 리턴
- getPort() : 이 URL의 포트 번호 리턴
- InputStream OpenStream() : url 주소와 연결한 뒤 , 연결로부터 입력받을 수 있는 inputstream 객체 리턴 => URL 클래스를 이용해 연결된 상대편으로부터 데이터를 읽을 때는 그 전에 먼제 OpenStream() 메소드를 통해 입력 스트림을 연다. 그러고 나면 일반적인 입력 스트림에서 읽듯이 데이터를 읽어온다.
- URLConnection openConnection() : URL 주소의 원격 객체에 접속한 뒤 통신할 수 있는 URLConnection 객체 리턴

# apachi webserver 더 공부하자
