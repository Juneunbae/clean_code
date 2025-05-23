# 창발적 설계의 네가지 원칙

## 1. 모든 테스트를 실행한다.

설계는 의도한 대로 돌아가는 시스템을 내놓아야 한다.

테스트가 불가능한 시스템은 검증도 불가능하기 때문에 테스트 가능한 시스템을 만드는 것이 중요하다.

테스트가 가능한 시스템은 설계 품질을 높일 수 있다.

- 크기가 작고 목적 하나만 수행하는 클래스가 나온다.(SRP 준수)
- 테스트 케이스를 많이 작성할수록 DIP, 인터페이스, 추상화 등과 같은 도구를 사용해 결합도를 낮춘다.

## 2. 중복을 없앤다.

중복은 추가 작업, 추가 위험, 불필요한 복잡도를 뜻한다.

- 똑같은 코드
    - 공통적인 코드를 새 메서드로 재정의
- 구현 중복
    - TEMPLATE METHOD 패턴을 적용해 구현 중복을 개선

## 3. 프로그래머 의도를 표현한다.

소프트웨어 프로젝트 비용 중 대다수는 장기적인 유지보수에 들어간다.

개발자가 코드를 명핵하게 짤수록(의도를 분명히 할수록) 다른 사람이 그 코드를 이해하기 쉬워진다.

- 좋은 이름을 선택한다.(메서드명, 변수명, 클래스명, 패키지명)
- 함수와 클래스 크기를 가능한 줄인다.
- 표준 명칭을 사용한다.(COMMAND, VISITOR와 같은 표준패턴 사용시 명칭에 포함하기)
- 단위 테스트 케이스를 꼼꼼히 작성한다.(예제를 통해 더 잘 이해하게 하기)

## 4. 클래스와 메서드 수를 최소로 줄인다.

위 원칙들을 극단적으로 사용하면 득보다 실이 많아질 수 있다.

함수와 클래스 크기를 작게 유지하면서 동시에 시스템 크기도 작게 유지하는 것을 목표로하지만 위 세 규칙보다는 우선순위가 낮다는 것을 인지해야 한다.