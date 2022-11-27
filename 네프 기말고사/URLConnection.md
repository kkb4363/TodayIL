# URLConnection , HttpURLConnection
- URLConnection은 자바와 URL간의 연결 관련한 모든 클래스의 슈퍼클래스이다.
- 일반적인 URL에 대한 API를 제공하고, 서브 클래스 HttpURLConnection은 HTTP 고유의 기능에 대한 추가 지원을 제공한다.
- 이 두 클래스는 모두 추상클래스이다. 그러므로 직접 새 인스턴스를 만들 수 없다.
- 대신 URL 객체에서 연결을 통해 URLConnection의 인스턴스를 얻는다.
- URLConnection은 Http request, response에서 header부분과 따로따로 논다. => response도 header, data 따로따로 받는게 아니라 한번에 다 받는다.(url connection의 메소드들이 이걸 구분하는 것임)
- header 쪽은 getheaderfield key 이렇게 데이터 뽑아내고 , 아래쪽은 inputstream으로 데이터를 뽑아냄. 
outputstream은 request의 아래쪽에 있는 부분을 내가 작성하는 것이다.
- header는 response에 있는 부분만 가져오는 것
- options는 가능한 메소드를 알려달라는 것(get,post,delete 등)
- trace는 디버깅 용도(request헤더를 response 데이터에 넣어서 보내는 것)

- 일반적으로 클라이언트 프로그램은 다음 단계를 따른다

## 1. url 객체 생성
- URL url = new URL("http://www.naver.com"); 
- 위와 같이 주어진 url 주소에 대해 새 url 객체를 생성한다.
- 이 생성자는 url 형식이 잘못된 경우 MalformedURLException을 throw한다. 이 예외는 IOException의 하위 클래스다.

## 2. url에서 urlconnection 객체 얻기 
- URLConnection 인스턴스는 url 객체의 openConnection()메소드 호출에 의해 얻어진다.
- URLConnection Urlcon = url.openConnection();
- openConnection() 메소드는 실제 네트워크 연결을 설정하지 않고, 단지 URLConnection 클래스의 인스턴스를 반환한다. 
- 네트워크 연결은 connect() 메소드가 호출 될 떄 명시적으로 이루어지거나, 헤더필드를 읽거나, 입력스트림/출력스트림을 가져올 때 암시적으로 이루어진다.
- url의 openConnection() 메소드는 I/O 에러가 발생하면 IOException 을 발생시킨다.

## 3. 연결 종료
- 연결을 닫으려면 InputStream또는 OutputStream 객체에서 close()메소드를 호출한다.
- 이렇게 하면 URLConnection 인스턴스와 연결된 네트워크 리소스가 해제된다.



### URLConnection 구성요소는 사이트 참고
- https://blueyikim.tistory.com/2199