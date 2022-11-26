# Abstract Factory Pattern

- 정의 : Factory Pattern과 유사한 패턴으로, 팩토리 of 팩토리 라고 볼 수 있다.
  , Factory Pattern에서는 하나의 팩토리 클래스가 인풋으로 들어오는 값에 따라 if-else나 switch를 사용해 다양한 서브클래스를 리턴하는 형식 이었지만,
  Abstract Factory Pattern은 인풋으로 서브클래스에 대한 식별 데이터를 받는 것이 아니라, 또 하나의 팩토리 클래스를 받는다.

## 코드 살펴보기

```
public abstract class Computer { // super class

    public abstract String getRAM();
    public abstract String getHDD();
    public abstract String getCPU();

    @Override
    public String toString(){
        return "RAM= "+this.getRAM()+", HDD="+this.getHDD()+", CPU="+this.getCPU();
    }
}

public class PC extends Computer { // sub class 1

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

}

public class Server extends Computer { // sub class 2

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

}
// 여기까지는 Factory pattern 과 같다. 하지만 아래부턴 차이가 난다.

public interface ComputerAbstractFactory{
    public Computer createComputer();
}
// 여기서 중요한 점은 위에서 작성한 팩토리 인터페이스의 createComputer() 메소드의 리턴 타입이 super class인 Computer 라는 것이다.
이제 이 팩토리 인터페이스를 구현하는 클래스에서 createComputer를 오버라이딩하여 각각의 서브 클래스를 리턴해줄 것이다. (이는 자바의 다형성을 아주 잘 활용한 방식이다.)
* 다형성이란 : 하나의 타입에 여러 객체를 대입할 수 있는 성질, 이것을 구현하기 위해서는 여러 객체들 중 공통 특성으로 타입을 추상화 하고 그것을 상속해야함.

public class PCFactory implements ComputerAbstractFactory { // PC Factory

	private String ram;
	private String hdd;
	private String cpu;

	public PCFactory(String ram, String hdd, String cpu){
		this.ram=ram;
		this.hdd=hdd;
		this.cpu=cpu;
	}
	@Override
	public Computer createComputer() {
		return new PC(ram,hdd,cpu);
	}

}

public class ServerFactory implements ComputerAbstractFactory{
    // Server Factory
    private String ram;
    private String hdd;
    private String cpu;

    public ServerFactory(String ram , String hdd , String cpu){
        this.ram = ram;
        this.hdd = hdd;
        this.cpu = cpu;
    }

    @Override
    public Computer createComputer(){
        return new Server(ram, hdd, cpu);
    }
}

public class ComputerFactory{
    public static Computer getComputer(ComputerAbstractFactory factory){
        return factory.createComputer();
    }
}

public class AbstractFactoryTest {

	public static void main(String[] args) {
		Computer pc = ComputerFactory.getComputer(new PCFactory("2 GB","500 GB","2.4 GHz"));
		Computer server = ComputerFactory.getComputer(new ServerFactory("16 GB","1 TB","2.9 GHz"));
		System.out.println("AbstractFactory PC Config::"+pc);
		System.out.println("AbstractFactory Server Config::"+server);
	}

}
```

## 장점

- 구현보다 인터페이스를 위한 코드 접근법을 제공한다. 위 코드에서 getComputer() 메소드는 파라미터로 인터페이스를 받아 처리하기 때문에 getComputer()에서 구현할 것이 복잡하지 않다.
- 추후에 sub class를 확장하는 데 있어 굉장히 쉽게 할 수 있다.
  위 코드에서 만약 Laptop 클래스를 추가하고자 하면 getComputer()의 수정 없이 LaptopFactory만 작성해주면 된다.
- 팩토리 패턴의 if-else, switch등 으로부터 벗어난다.
