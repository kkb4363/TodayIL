# SocketServer

- ServerSocket 클래스는 서버 프로그램을 구현하는데 사용된다. 일반적인 서버 프로그램 과정은 6단계이다.

1. 서버 소켓 생성, 포트 바인딩
2. client로부터 연결을 기다리고 요청이 오면 수락
3. client 소켓에서 가져온 InputStream(client 입장에선 OutputStream)을 읽음
4. 응답이 있다면 OutputStream을 통해 클라이언트에 데이터 보냄
5. client와 연결을 닫음
6. 서버 종료

## 1. 서버 소켓 생성

- 아래 생성사 중 하나를 사용해 ServerSocket 클래스의 새 객체를 만든다.

1. ServerSocket(int port) : 지정된 포트 번호에 바인딩 된 서버 소켓을 만듬
2. ServerSocket(int port , int backlog) : 지정된 포트 번호에 바인드 된 서버 소켓을 만들고 대기중인 최대 연결 수를 backlog 매개변수로 지정
3. ServerSocket(int port , int backlog , InetAddress bind Addr) : 서버 소켓을 만들고 지정된 포트 번호와 로컬 IP 주소에 바인딩

- 간단한 사용 예시 , 서버 소켓을 포트번호 8000에 바인딩 하는 예

```
ServerSocket serverSocket = new ServerSocket(8000);
// 이러한 생성자는 소켓을 열 때 I/O Exception이 일어 날 수 있다.
```

## 2. 연결 기다리기

```
// 연결 수신의 예시
Socket socket = serverSocket.accept();
```

## 3. client로부터 온 데이터 읽기

- Socket 객체가 연결 되면 InputStream을 사용해 client로부터 온 데이터를 읽을 수 있다.

```
InputStream input = socket.getInputStream();
```

- InputStream은 데이터를 byte 배열로 읽기 떄문에, 상위 레벨의 데이터를 읽으려면 InputStreamReader로 읽어야 한다.

```
InputStreamReader reader = new InputStreamReader(input);
int character = reader.read();
```

- 또한 BufferedReader에 InputStream을 매핑하여 데이터를 String으로 읽어온다.

```
BufferedReader reader = new BufferedReader(new InputStreamReader(input));
String line = reader.readLine();
```

## 4. client에 데이터 전송

- Socket과 연결 된 client에게 OutputStream을 사용해 데이터를 보낸다.

```
OutputStream output = socket.getOutputStream();
```

- PrintWriter를 사용해 텍스트 형식으로 데이터를 보냄.

```
PrintWriter writer = new PrintWriter(output, true);
writer.println("This is a message to the server");
```

## 5. client와 연결 종료

- Socket 통신이 완료 되면 , close() 메서드를 사용해 client와 연결을 종료함.

```
socket.close();
// close()메서드는 소켓의 InputStream과 OutputStream을 닫아 주는 역할을 함.
```

## 6. server 종료

- 서버는 client에서 들어오는 요청을 기다리며 항상 실행되어 있어야 함.
- 서버를 중지해야 하는 경우에는 ServerSocket의 인스턴스의 close()메서드를 호출하여 서버를 종료 해준다.
- client Connection을 종료하는 메서드와 명칭이 같지만, client와의 연결을 끊는 것이 아니라 server를 중지하는 역할을 함.

```
serverSocket.close();
```
