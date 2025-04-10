# 경계

### 목표

- 외부 코드를 우리 코드에 깔끔하게 통합해야만 한다.
- 소프트웨어 경계를 깔끔하게 처리하는 기법과 기교를 살펴본다.

## 경계 인터페이스란?

어떠한 메서드에서 Map, List와 같은 자료구조를 반환하거나 공개 API 인수로 넘겨서 클라이언트에서 해당 인터페이스를 사용하는 경우를 의미합니다.

### 문제점

- 사용자가 너무 많은 인터페이스에 노출될 수 있습니다.
    - 이는 사용자가 예상치 못한 기능을 작동시킬 수 있다는 말이 됩니다.
- 자료구조 인터페이스의 변경이 발생한다면, 수정할 코드가 많아집니다.
    - 여러 자료구조를 자유롭게 변경하지 못하면서 자료구조에 종속되게 됩니다.

### 해결방법

- 래퍼 클래스로 감싸 원하는 메서드만을 노출시키기
    - 사용자에게 한정적인 기능만을 주어 올바르게 사용할 책임을 사용자에게 주지 않습니다.
    - 제네릭을 사용하지 않아도 데이터 타입을 고정시킬 수 있습니다.

```java
public class Sensors {
  private Map sensors = new HashMap();
  public Sensor getById(String id) {
    return (Sensor) sensors.get(id);
  }
  // 이하 생략
}
```

### 정리

- 경계 인터페이스를 항상 클래스로 감싸줄 필요는 없지만, 클래스나 클래스 배열 밖으로 나가지 않도록 주의해야합니다.
    - 특히, 공개 API 인수로 넘기거나 반환값으로 사용되지 않도록 주의해야 합니다.

### 확장된 개념 일급 컬렉션

컬렉션을 래핑하여, 이외의 멤버 변수가 없는 상태를 말합니다.

- 상태와 행위를 각각 관리할 수 있습니다.
- 컬렉션의 불변성을 보장해주어야 합니다.
    - final 만으로는 부족합니다!
    - 단순한 getter 메서드를 통해 컬렉션을 응답해주게 되면 외부에서 수정할 수 있어 불변성이 보장되지 않습니다.
    - 새로운 객체로 만들어주는 방법은 컬렉션의 요소 값들이 수정될 수 있는 문제가 있습니다.
    - 불변 객체를 생성할 수 있는 방법을 사용해서 응답하도록 합시다! (ex. Collections.unmodifiableList())

## 경계 살피고 익히기

- 학습 테스트
    - 외부 코드를 사용하는 우리쪽 코드를 먼저 작성하고 간단한 테스트 케이스를 작성해서 외부 코드를 익히는 방법입니다.
    - API를 사용하려는 목적에 초점을 맞춥니다.
    - 필요한 지식만을 확보하는 손쉬운 방법입니다.
    - 외부 API가 새로운 버전으로 바뀌었을 때에도 예상대로 로직이 수행되는지 검증할 수 있습니다.

### 아직 존재하지 않는 코드를 사용하기

- 우리가 바라는 인터페이스를 구현하고 사용함으로써 우리의 코드는 깔끔하고 깨끗해집니다.
- Adapter 패턴을 통해 API 사용을 캡슐화해 API가 바뀔 때 수정할 코드를 구현체로 모을 수 있습니다.
- 적절한 구현체를 만들어 우리의 코드를 쉽게 테스트할 수 있습니다.

## 깨끗한 경계

- 경계에 위치하는 코드는 깔끔하게 분리합시다.
    - 새로운 클래스로 감싸거나 Adapter 패턴을 사용해 우리가 원하는 인터페이스를 패키지가 제공하는 인터페이스로 변환합시다.
- 통제가 불가능한 외부 패키지에 의존하지 말고,
통제가 가능한 우리 코드에 의존하는 것이 훨씬 좋습니다.
    - 코드 가독성이 높아지고, 경계 인터페이스를 사용하는 일관성도 높아지며, 외부 패키지가 변했을 때 변경할 코드도 줄어듭니다.

### REFERENCE

- https://medium.com/webeveloper/%EA%B2%BD%EA%B3%84-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EB%A5%BC-%ED%81%B4%EB%9E%98%EC%8A%A4%EB%A1%9C-%EA%B0%90%EC%8B%B8%EA%B8%B0-ac6838e1adae
- https://jojoldu.tistory.com/412
- https://tecoble.techcourse.co.kr/post/2020-05-08-First-Class-Collection/