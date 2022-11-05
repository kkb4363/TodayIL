# Builder Pattern 
- 정의 : 복잡한 객체를 생성하는 방법을 정의하는 클래스와 표현하는 방법을 정의하는 클래스를 별도로 분리하여, 서로 다른 표현이라도 이를 생성할 수 있는 동일한 절차를 제공하는 패턴이다.

- 많은 Optional한 멤버 변수나 지속성 없는 상태 값들에 대해 처리해야 하는 문제들을 해결한다.

- 예를 들어, 팩토리 패턴이나 추상 팩토리 패턴에선 생성해야하는 클래스에 대한 속성값이 많을 때 아래와 같은 이슈들이 있다.
1. 클라이언트 프로그램으로부터 팩토리 클래스로 많은 파라미터를 넘겨줄 때 타입, 순서 등에 대한 관리가 어려워져 에러가 발생할 확률이 높아진다.
2. 경우에 따라 필요 없는 파라미터들에 대해 팩토리 클래스에 일일이 null값을 넘겨줘야 합니다.
3. 생성해야 하는 sub class가 무거워지고 복잡해짐에 따라 팩토리 클래스 또한 복잡해진다.

- 빌더 패턴은 이러한 문제들을 해결하기 위해 별도의 Builder 클래스를 만들어 필수 값에 대해서는 생성자를 통해, 선택적인 값들에 대해서는 메소드를 통해 step-by-step으로 값을 입력받은 후에 build() 메소드를 통해 최종적으로 하나의 인스턴스를 리턴하는 방식이다.

## 코드 예시
```
public class Computer {
	
    //required parameters
    private String HDD;
    private String RAM;
	
    //optional parameters
    private boolean isGraphicsCardEnabled;
    private boolean isBluetoothEnabled;
	
 
    public String getHDD() {
        return HDD;
    }
 
    public String getRAM() {
        return RAM;
    }
 
    public boolean isGraphicsCardEnabled() {
        return isGraphicsCardEnabled;
    }
 
    public boolean isBluetoothEnabled() {
        return isBluetoothEnabled;
    }
	
    private Computer(ComputerBuilder builder) {
        this.HDD=builder.HDD;
        this.RAM=builder.RAM;
        this.isGraphicsCardEnabled=builder.isGraphicsCardEnabled;
        this.isBluetoothEnabled=builder.isBluetoothEnabled;
    }
	
    //Builder Class
    public static class ComputerBuilder{
 
        // required parameters
        private String HDD;
        private String RAM;
 
        // optional parameters
        private boolean isGraphicsCardEnabled;
        private boolean isBluetoothEnabled;
		
        public ComputerBuilder(String hdd, String ram){
            this.HDD=hdd;
            this.RAM=ram;
        }
 
        public ComputerBuilder setGraphicsCardEnabled(boolean isGraphicsCardEnabled) {
            this.isGraphicsCardEnabled = isGraphicsCardEnabled;
            return this;
        }
 
        public ComputerBuilder setBluetoothEnabled(boolean isBluetoothEnabled) {
            this.isBluetoothEnabled = isBluetoothEnabled;
            return this;
        }
		
        public Computer build(){
            return new Computer(this);
        }
 
    }
 
}
```

- 여기서 살펴볼 것은 Computer 클래스가 setter 메소드 없이 getter 메소드만 가진다는 것과 public 생성자가 없다는 것입니다. 그렇기 때문에 Computer 객체를 얻기 위해서는 오직 ComputerBuilder 클래스를 통해서만 가능하다.

```
public class TestBuilderPattern{
    public static void main(String[ args]){
        Computer comp = new Computer.ComputerBuilder("500GB", "2GB")
        .setBluetoothEnabled(true)
        .setGraphicsCardEnabled(true)
        .build();
    }
}
```
- 보시는 것처럼 Computer 객체를 얻기 위해 ComputerBuilder 클래스를 사용하고 있으며 필수 값인 HDD와 RAM속성에 대해서는 생성자로 받고 Optional한 값인 BluetoothEnabled 와 GraphicsCardEnabled에 대해서는 메소드를 통해 선택적으로 입력 받고 있다.
즉 BluetoothEnabled 값이 필요 없는 객체라면 setBluetoothEnabled() 메소드를 사용하지 않으면 된다.
