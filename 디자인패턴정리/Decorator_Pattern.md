# Decorator Pattern

- 정의 : 객체의 결합을 통해 기능을 동적으로 유연하게 확장할 수 있게 해주는 패턴
  즉, 기본 기능에 추가할 수 있는 기능의 종류가 많은 경우, 각 추가 기능을 decorator 클래스로 정의한 후 필요한 decorator객체를 조합함으로써 추가 기능의 조합을 설계하는 방식임.

## decorator pattern 이 없다면 예시 코드

```
public class RoadDisplay{
    public void draw(){
        System.out.println("기본도로표시");
    } // 기본 도로 표시 클래스
}

public class RoadDisplayWithLane extends RoadDisplay{
    public void draw(){
        super.draw(); // 상위 클래스, 즉 roadDisplay 클래스의 draw메서드 호출
        drawLane(); // 추가적으로 차선 표시
    }
    private void drawLane(){
        System.out.println("차선표시");
    }
}

public class Client{
    public static void main(String[] args){
        RoadDisplay road = new RoadDisplay();
        road.draw(); // 기본도로만 표시

        RoadDisplay roadWithLane = new RoadDisplayWithLane();
        roadWithLane.draw(); // 기본도로 + 차선 표시
    }
}
```

- 위의 코드에서 문제점 : 또 다른 도로 표시 기능을 원래 표시에 추가로 구현하고 싶다면? 불가능 즉, 다양한 기능의 조합을 고려해야하는 경우 상속을 통한 기능의 확장은 각 기능별로 클래스를 추가해야 한다는 단점이 있다.

## 해결책 - decorator pattern 예시 코드

```
public abstract class Display{
    public abstract void draw();
}

public class RoadDisplay extends Display{
    @Override
    public void draw() {
        System.out.println("기본도로표시");
    }
}// 기본 도로 표시 클래스

public abstract class DisplayDecorator extends Display{
    private Display decoratedDisplay;
    public DisplayDecorator(Display decoratedDisplay){
        this.decoratedDisplay = decoratedDisplay;
    } // 다양한 추가 기능에 대한 공통 클래스
    @Override
    public void draw(){
        decoratedDisplay.draw();
    }
}

// 차선표시 추가 클래스
public class LaneDecorator extends DisplayDecorator{
    public LaneDecorator(Display decoratedDisplay){
        super(decoratedDisplay);
    }
    @Override
    public void draw(){
        super.draw(); // 설정된 기존 표시 기능
        drawLane(); // 추가적으로 차선 표시
    }

    private void drawLane(){
        System.out.println("차선표시"); // 차선 표시 기능만 직접 제공
    }
    }

// 교통량 표시 추가 클래스
public class TrafficDecorator extends DisplayDecorator{
    public TrafficDecorator(Display decoratedDisplay){
        super(decoratedDisplay)
    }
    @Override
    public void draw(){
        super.draw(); // 설정된 기존 표시 기능
        drawTraffic(); // 추가적으로 교통량 표시
    }
private void drawTraffic(){
    System.out.println("교통량 표시"); // 교통량 표시만 직접 제공
}
}
}

public class Client{
    public static void main(String[] args){
        Display road = new RoadDisplay();
        road.draw(); // 기본도로 표시
        Display roadWithLane = new LaneDecorator(new RoadDisplay());
        roadWithLane.draw(); // 기본도로 표시 + 차선 표시
        Display roadWithTraffic = new TrafficDecorator(new RoadDisplay());
        roadWithTraffic.draw(); // 기본도로 표시 + 교통량 표시
    }
}
```

- 각 road, roadwithlane, roadwithtraffic 객체의 접근이 모두 display 클래스를 통해 이루어짐.
- 즉, 어떤 기능을 추가하느냐에 관계없이 client 클래스는 동일한 display 클래스만을 통해 일관성 있는 방식으로 도로 정보를 표시할 수 있다.
- 이렇게 decorator 패턴을 이용하면 추가 기능 조합별로 별도의 클래스를 구현하는 대신 , 각 추가기능에 해당하는 클래스의 객체를 조합해 추가기능의 조합을 구현 할 수 있게 된다. -> 이 설계는 추가기능의 수가 많을수록 효과가 크다.
