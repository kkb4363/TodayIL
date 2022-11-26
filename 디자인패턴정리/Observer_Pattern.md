# Observer Pattern

- 정의: 객체 사이에 일 대 다의 의존 관계를 정의해 두어, 어떤 객체의 상태가 변할 때 그 객체에 의존성을 가진 다른 객체들이 그 변화를 통지받고 자동으로 갱신될 수 있게 만드는 것.
- 어떤 객체의 상태가 변할 때 그와 연관된 객체들에게 알림을 보내는 디자인 패턴
- 학생들은 선생님이 하는 일들을 모두 알림을 받아야 함.
  즉, 선생님이 '밥을 먹으면' 모든 학생들은 선생님이 밥을 먹었다는 것을 알아야함.

## 코드 예시

```
public interface Observer{
    public void update(Subject theChangedSubject);
}
//subject는 observer들을 알고 있는 객체이다.(여러 observer가 subject에 붙을 수 있다.)

public interface subject{
    public void attach(Observer o);
    public void detach(Observer o);
    public void notify();
}
// attach : subject에 observer를 구독자로 등록함.
   detach : subject에 등록한 observer의 구독을 해지함.
   notify : subject에서 모든 observer에 정보를 전달함.
```

## 구현할 때 고려해야 할 점들

- 옵저버는 상태를 갖지 않아도 됨. -> 상태는 subject 담당이므로 subject와 observer의 일대다 관계가 성립함.
- update 메소드 인자 -> 위의 코드에선 theChangedSubject라는 시그니처를 갖고 있다. 하지만 상황에 따라 다른 인자를 함께 넘기는 것도 가능하다.
  예시)void update(Subject theChangedSubject, int changedCount)

## observer pattern의 문제점들

1. 통보체인 : 통보체인이란, 한 관찰자가 통보를 받았을 때 자신이 다시 그 주체가 되어 또 다른 관찰자에게 통보를 하고 , 그 관찰자는 또 다른 관찰자에게 통보하는 식으로 연속적인 통보가 발생하는 것이다.
   이런 식의 통보체인이 불가피한 상황에서 observer패턴을 적용하려면, 설계가 복잡해지고 디버깅도 어려워진다. -> 이럴때 Mediator 패턴을 도입하면 도움이 됨.
2. 메모리 누수 : 관찰자 객체가 제떄에 쓰레기 수집되지 않는 현상으로, 통보 주체가 관찰자 객체의 참조를 갖고 있기 때문에 발생한다. 통보주체가 이것을 제때 삭제해 준다면, 메모리 누수를 피할 수 있다.
