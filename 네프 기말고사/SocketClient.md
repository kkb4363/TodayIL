# Socket Client

- 이 클래스를 사용해서 서버와 연결 , 데이터 전송, 데이터 리딩을 할 수 있다.
- 일반적인 통신의 단계는

1. client가 호스트이름 / IP 주소 및 포트 번호로 지정된 서버에 연결 시작
2. OutputStream을 사용해 서버에 데이터 전송
3. InputStream을 사용해 서버에서 데이터 읽음
4. 연결 종료

## 1. 서버에 대한 연결 시작

- 서버에 연결하려면 아래 생성자 중 하나를 사용해 새 Socket 객체를 만든다.
- 생성자1 : Socket(InetAddress address , int port)
- 생성자2 : Socket(String host , int port)
- 생성자3 : Socket(InetAddress address , int port , InetAddress local Addr, int LocalPort)
- 생성자 1과 2를 사용하면 , 시스템은 client 컴퓨터에 사용 가능한 포트 번호와 로컬 주소를 자동으로 할당한다.
- 위의 세 소켓 생성자는 소켓 작성 중에 입출력 에러가 발생 할 경우가 있는데, 이를 대비해 Exception 처리를 해야 한다.
- 네이버에 포트 8000번으로 연결하려는 클라이언트 소켓을 만드는 코드 예시

```
Socket socket = new Socket("naver.com" , 8000);
```

## 2. 서버에 데이터 보내기

- 서버에 데이터를 보내려면 먼저 소켓에서 OutputStream 객체를 가져와야 한다.

```
OutputStream output = socket.getOutputStream();
```

- 객체를 가져 온 후에, OutputStream의 write() 메서드를 사용해 보낼 바이트 배열을 쓸 수 있다.

```
String realStr = "This is woolbro dev Note";
byte[] data = realStr.getBytes();  // getBytes()메서드를 사용해 문자열을 byte로 바꿔준다.
output.write(data);
```

- PrintWriter에 OutputStream을 래핑하여 다음과 같이 데이터를 텍스트 형식으로 보낼 수 있다.

```
PrintWriter writer = new PrintWriter(output, true);
// true 인수는 메소드 호출 후에 데이터 자동 비우기 설정이다.
writer.println("This is a Message");
```

## 3. 서버에서 데이터 읽기

- 서버에서 데이터를 읽으려면 client 소켓에서 InputStream 객체를 가져와야 한다.

```
InputStream input = socket.getInputStream();
```

- 그런다음 InputStream에서 read() 메서드를 활용해 데이터를 읽는다.

```
input.read(data);
```

- InputStreamReader와 BufferedReader 또한 사용 할 수 있다.

```
//InputStreamReader사용시
InputStreamReader reader = new InputStreamReader(input);
int character = reader.read();

//BufferedReader 사용시
BufferedReader reader = new BufferedReader(new InputStreamReader(input));
String line = reader.readLine();
```

## 4. 연결 종료

- 소켓에서 close() 메서드를 호출하여 client와 server간의 연결을 종료함.

```
socket.close();
```
