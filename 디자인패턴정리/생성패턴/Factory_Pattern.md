# Factory Pattern

- 정의 : 객체를 생성하는 인터페이스는 미리 정의하되, 인스턴스를 만들 클래스의 결정은 서브 클래스쪽에서 내리는 패턴이다. 즉, 여러개의 서브 클래스를 가진 슈퍼 클래스가 있을때 인풋에 따라 하나의 자식 클래스의 인스턴스를 리턴해주는 방식이다.
- 활용성 : 어떤 클래스가 자신이 생성해야 하는 객체의 클래스를 예측할 수 없을때
  , 생성할 객체를 기술하는 책임을 자신의 서브클래스가 지정했으면 할 때

# 코드 예시

```
public abstract class Computer {
    public abstract String getRAM();
    public abstract String getHDD();
    public abstract String getCPU();

    @Override
    public String toString(){
        return "Ram=" + this.getRAM() + ",HDD=" + this.getHDD() + ",CPU=" + this.getCPU();
    }
}
// 슈퍼 클래스

public class PC extends Computer {

    private String ram;
    private String hdd;
    private String cpu;

    public PC(String ram, String hdd, String cpu){
        this.ram=ram;
        this.hdd=hdd;
        this.cpu=cpu;
    }
    @Override
    public String getRAM() {
        return this.ram;
    }

    @Override
    public String getHDD() {
    return this.hdd;
    }

    @Override
    public String getCPU() {
        return this.cpu;
    }

} // 서브 클래스 1

public class Server extends Computer {

    private String ram;
    private String hdd;
    private String cpu;

    public Server(String ram, String hdd, String cpu){
        this.ram=ram;
        this.hdd=hdd;
        this.cpu=cpu;
    }
    @Override
    public String getRAM() {
        return this.ram;
    }

    @Override
    public String getHDD() {
        return this.hdd;
    }

    @Override
    public String getCPU() {
        return this.cpu;
    }

} // 서브 클래스 2

-> 여기서 주의할 점은 pc 클래스와 server 클래스 모두 Computer를 상속한다는 것이다.

public class ComputerFactory{
    public static Computer getComputer(String type, String ram, String hdd, String cpu){
        if("PC".equalsIgnoreCase(type))
        return new PC(ram,hdd,cpu);
        else if("Server".equalsIgnoreCase(type))
        return new Server(ram,hdd,cpu);

        return null;
    }
} // Factory Class

public class TestFactory{
    public static void main(String[] args){
        Computer pc = computerFactory.getComputer("PC", "2GB", "500GB", "2.4GHz");
        Computer server = ComputerFactory.getComputer("server", "16GB", "1TB", "2.9GHz");
        System.out.println("Factory PC Config:" + pc);
        System.out.println("Factory Server Config:" + server);

    }
} // main 함수
```

## 코드 살펴보기

- ComputerFactory 클래스의 getComputer 메소드를 보면 static 메소드로 구현되어있다.
- 메소드 내부 코드를 보면 type값이 'PC'일경우 PC 클래스의 인스턴스를, 'SERVER'일 경우 SERVER 클래스의 인스턴스를 리턴함.
- 이렇듯 팩토리 패턴을 사용하게 되면 인스턴스를 필요로 하는 Application에서 Computer의 sub클래스에 대한 정보는 모른 채 인스턴스를 생성할 수 있다.
- 이렇게 구현한다면 앞으로 computer 클래스에 더 많은 sub클래스가 추가 된다해도 getcomputer()를 통해 인스턴스를 제공받던 application의 코드는 수정할 필요가 없게 된다.

- 팩토리 패턴을 구현하는데 중요한 점은

1. Factory class를 singleton으로 구현해도 되고, 서브 클래스를 리턴하는 static 메소드로 구현해도 된다.
2. 팩토리 메소드는 위 코드의 getComputer()와 같이 입력된 파라미터에 따라 다른 서브 클래스의 인스턴스를 생성하고 리턴한다.

## 장점

1. 팩토리 패턴은 클라이언트 코드로부터 서브 클래스의 인스턴스화를 제거하여 서로 간의 종속성을 낮추고, 결합도를 느슨하게 하며 확장을 쉽게 한다 -> 예를 들어 위 코드에서 Pc class에 대해 수정or삭제가 일어나더라도 클라이언트는 알 수 없기 때문에 코드를 변경할 필요가 없다.
2. 팩토리 패턴은 클라이언트와 구현 객체들 사이에 추상화를 제공한다.
