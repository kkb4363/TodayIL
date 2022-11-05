# Singleton Pattern

- 정의 : 어떤 클래스의 인스턴스가 오직 하나임을 보장하며, 이 인스턴스에 접근할 수 있는 전역적인 접촉점을 제공하는 패턴.
  즉, 프로그램 시작부터 종료까지 어떤 클래스의 인스턴스가 메모리 상에 단 하나만 존재할 수 있게하고, 이 인스턴스에 대해 어디에서나 접근할 수 있도록 하는 패턴

## 구현 방법

- 싱글톤 패턴을 구현하는 방법은 굉장히 다양하다. 그러나 각각의 패턴이 공통적으로 갖는 특징이 있는데, 이는 다음과 같다.
  - private 생성자만을 정의해 외부 클래스로부터 인스턴스 생성을 차단한다.
  - 싱글톤을 구현하고자 하는 클래스 내부에 멤버 변수로써 private static 객체 변수를 만든다.
  - public static 메소드를 통해 외부에서 싱글톤 인스턴스에 접근할 수 있도록 접점을 제공한다.

1. Eager Initialization 구현 방법

- 가장 간단한 형태의 구현 방법이다. 이는 싱글톤 클래스의 인스턴스를 클래스 로딩단계에서 생성하는 방법이다. 그러나 어플리케이션에서 해당 인스턴스를 사용하지 않더라도 인스턴스를 생성하기 떄문에 자칫 낭비가 발생할 수 있다.

```
public class Singleton{
    private static final Singleton instance = new Singleton();

    private Singleton(){

    }

    public static Singleton getInstance(){
        return instance;
    }
}
```

- 이 방법을 사용할때는 싱클톤 클래스가 다소 적은 리소스를 다룰 때여야 한다.
- 큰 리소스를 다룰 때는 위와 같은 방식보다는 getInstance() 메소드가 호출될 때 까지 싱글톤 인스턴스를 생성하지 않는 것이 더 좋다.
- 게다가 Eager Initialization은 Exception에 대한 Handling도 제공하지 않는다.

2. Static Block Initialization 구현 방법

- Eager initialization과 유사하지만 static block을 통해서 Exception Handling에 대한 옵션을 제공한다.

```
public class Singleton{
    private static Singleton instance;
    private Singleton(){

    }

    static{
        try{
            instance = new Singleton();
        }catch(Exception e){
            throw new RuntimeException("Exception occured");
        }
    }

    public static Singleton getInstance(){
        return instance;
    }
}
```

- 위와 같이 구현할 경우 싱글톤 클래스의 인스턴스를 생성할 때 발생할 수 있는 예외에 대한 처리를 할 수 있지만, eager initialization과 마찬가지로 클래스 로딩 단계에서 인스턴스를 생성하기 때문에 여전히 큰 리소스를 다루는 경우에는 적합하지 않다.

3. Lazy Initialization 구현 방법

- 앞선 두 방식과는 달리 나중에 초기화하는 방법이다. 이는 global access한 getInstance() 메소드를 호출할 때에 인스턴스가 없다면 생성한다.

```
public class Singleton{
    private static Singleton instance;
    private Singleton(){

    }
    public static Singleton getInstance(){
        if(instance == null){
            instance = new Singleton();
        }
        return instance;
    }
}

```

- 이 방식으로 구현할 경우 1,2번에서 안고 있던 문제에 대해 어느정도 해결책이 된다.
  그러나 이 경우에도 문제점이 있다. 그건 multi-thread 환경에서 동기화 문제이다.
- 만약 인스턴스가 생성되지 않은 시점에서 여러 쓰레드가 동시에 getInstance()를 호출한다면 예상치 못한 결과를 얻을 수 있을 뿐더러, 단 하나의 인스턴스를 생성한다는 싱글톤 패턴에 위반하는 문제점이 야기될 수 있다. 그렇기에 이 방법으로 구현을 해도 괜찮은 경우는 single-thread 환경이 보장되었을 때 이다.

4. Thread Safe Singleton 구현 방법

- lazy initialization 의 문제를 해결하기 위한 방법으로, getInstance()메소드에 synchronized를 걸어두는 방식이다. synchronized 키워드는 임계영역을 형성해 해당 영역에 오직 하나의 쓰레드만 접근 가능하게 해준다.

```
public class Singleton{
    private static Singleton instance;
    private Singleton(){

    }
    public static synchronized Singleton getInstance(){
        if(instance == null){
            instance = new Singleton();
        }
        return instance;
    }
}
```

- 위 방식으로 구현할 경우 getInstance() 메소드 내에 진입하는 쓰레드가 하나로 보장받기 때문에 멀티 쓰레드 환경에서도 잘 작동한다. 그러나 synchronized 키워드 자체에 대한 비용이 크기 떄문에 싱글톤 인스턴스 호출이 잦은 어플리케이션에서는 성능이 떨어지게 된다.
- 그래서 고안된 방식이 double checked locking이다. 즉 getInstance() 메소드 수준에 lock을 걸지 않고 instance가 null일 경우에만 synchronized가 동작하도록 한다. 코드는 아래와 같다.

```
public static Singleton getInstance(){
    if(instance == null){
        synchronized(Singleton.class){
            if(instance == null){
                instance = new Singleton();
            }
        }
    }
    return instance;
}
```

5. Bill Pugh Singleton Implementation 구현 방법

- Bill Pugh가 고안한 방식으로, inner static helper class를 사용하는 방식이다.
  앞선 방식이 안고 있는 문제들을 대부분 해결한 방법으로, 현재 가장 널리 쓰이는 싱글톤 구현 방법이다.

```
public class Singleton{
    private Singleton(){

    }
    private static class SingletonHelper{
        private static final Singleton INSTANCE = new Singleton();
    }
    public static Singleton getInstance(){
        return SingletonHelper.INSTANCE;
    }
}
```

- Inner class로 인해 복잡해 보일 수 있지만 생각보다 간단하다.
- private inner static class 를 두어 싱글톤 인스턴스를 만든다.
- 이때 1번과 2번 구현방식과의 차이점이라면 singletonhelper클래스는 singleton 클래스가 load 될때에도 load되지 않다가 getinstance()가 호출됐을 떄 비로소 JVM 메모리에 로드되고, 인스턴스를 생성하게 된다.
- 아울러 synchronized를 사용하지 않기 때문에 4번 구현방식에서 문제가 되었던 성능저하 또한 해결된다.

6. Enum Singleton

- 앞서 1~5번 구현방식은 사실 완전히 안전할 수 없다. 왜냐하면 Java의 Reflection을 통해서 싱글톤을 파괴할 수 있기 때문이다.
  이에 Java계의 거장 Joshua Bloch는 Enum으로 싱글톤을 구현하는 방법을 제안했다.

```
public enum EnumSingleton{
    INSTANCE;
    public static void doSomething(){
        //do something
    }
}
```

- 그러나 이 방법 또한 1,2번과 같이 사용하지 않았을 경우의 메모리 문제를 해결하지 못한 것과 유연성이 떨어진다는 면에서 한계를 지니고 있다.

## 결론

- 각각의 방식마다 장단점이 있어 무엇이 항상 옳은 구현이라고 할 수 없지만, 5번에서 살펴본 inner static class 방식을 사용하는 것이 대부분의 경우에 최선의 방법이다. 실제로 유명한 자바 오픈소스 프로젝트의 코드를 보면 5번의 방식으로 싱글톤을 사용하고 있다.
