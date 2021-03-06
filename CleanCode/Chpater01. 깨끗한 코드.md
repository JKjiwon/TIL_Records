# Chpater01. 깨끗한 코드

## 코드가 존재하리라.

- 프로그래밍 : 기계가 실행할 정도로 `상세하게 요구사항을 명시`하는 작업

- 코드 : 요구사항을 표현하는 언어

<br>

## 나쁜 코드

- 시간이 급박해 기능에만 우선시한 코드

- 자신이 짠 쓰레기 코드를 바라보며 `나중에 손보겠다`고 생각

- 르블랑의 법칙: 나중은 결코 오지 않는다.

<br>

## 나쁜 코드로 치르는 대가

- 코드가 엉망이라 프로젝트 진도가 나가지 않는다.

- 나쁜 코드는 얽히고 설켜 있어 `변경이 어렵다.`

- 나쁜 코드는 생산성을 떨어뜨린다. -> 결국 0에 수렴한다.

### 원대한 재설계의 꿈

- `재설계를 위해 새로운 타이거` 팀이 구성된다.

- 타이거 팀은 기존 시스템의 기능을 모두 제공하고, 기존 시스템에 가해지는 변경도 모두 따라잡아야 한다. -> 너무 오랜 시간이 걸린다.

- 타이거 팀도 결국 낡은 팀이 된다.

### 태도

- 프로그래머의 변명 : 촉박한 일정, 요구사항의 잦은 변경. 이를 닦달하는 관리자와 고객때문에...

- 관리자가 일정과 요구사항을 강력하게 밀어 붙이는 것은 그들의 책임이다.

- `좋은 코드를 사수하는 일은 프로그래머의 책임`이다. 프로그래머가가 전문가답지 못했다.

### 원초적 난제

- 기한을 맞추는 유일한 방법, 즉 빨리 가는 유일한 방법은, `언제나 코드를 최대한 깨끗하게 유지하는 습관`이다.

### 깨끗한 코드라는 예술?

- `코드 감각`: 좋은 코드를 구분하는 능력 + 절제와 규율을 적용해 나쁜코드를 좋은 코드로 바꾸는 전략을 파악하는 능력

### 깨끗한 코드란?

#### 비야네 스트롭스트룹

- 깨끗한 코드는 `보기에 즐거운` 코드

- 효율적인 코드 = 속도 + 자원 낭비X

- `의존성을 최대한 줄여야` 유지보수가 쉬워진다.

- 오류처리, 메모리누수, 경쟁상태, 일관성 없는 명명법 등 `세세한 사항까지 꼼꼼하게 처리`하는 코드

- `한가지 일`에 집중하는 코드

#### 그래디 부치

- `가독성`을 중시

- `명쾌한 추상화`와 단순한 제어문 = 프로그래머가 단호하다는 인상

#### 큰(big) 데이브 토마스

- 작성자가 아닌 사람도 `읽기 쉽고 고치기 쉽다.`

- `테스트 케이스`가 없는 코드는 깨끗한 코드가 아니다.

- 최소 = 큰코드 보다 `작은 코드`에 가치를 둔다.

- 문학적 = 인간이 읽기 좋은 코드

#### 마이클 페더스

- 누군가가 `주의깊게 짰다`는 느낌을 준다.

- 작성자가 이미 `모든 사항을 고려했다.`

#### 론 제프리스

- 모든 테스트를 통과한다.

- 중복을 피하라.

- 시스템 내 모든 설계 아이디어를 표현한다.

- 클래스, 메서드, 함수 등을 최대한 줄인다.
    - 객체 나누기 : 하나의 객체가 여러 기능을 수행한다면
    - 메서드 추출 : 기능을 명확히 기술하는 메서드 하나 + 기능을 실제로 수행하는 메서드 여러개

- 집합에서 항목찾기: 집합을 추상메서드나 추상 클래스를 만들어 실제 구현을 감싼다.
    - 진짜 문제에만 신경을 쓴다.
    - 집합 기능을 구현하는데 시간과 노력을 낭비하지 않는다.

#### 워드 커닝햄

- 코드를 읽으면서 `짐작했던 기능을 각 루틴이 그대로 수행한다면` 깨끗한 코드 = 명백하고 단순하다.

- 코드가 그 문제를 풀기 위한 언어처럼 보인다면 아름다운 코드
    - 언어를 단순하게 보이도록 만드는 책임 = 프로그래의 책임

<br>

## 우리들의 생각 & 우리는 저자다

- 깨끗한 변수 이름, 깨끗한 함수, 깨끗한 클래스를 만드는 방법을 소개하겠다.

- 프로그래머는 일종의 저자다. 저자에게는 독자와 잘 소통할 책임이 있다.

- 읽는시간 : 짜는 시간 = 10 : 1

- 새 코드를 짜면서 우리는 끊임없이 기존코드를 읽는다.

- 쉽게 짜려면, 읽기 쉽게 만들면 된다.

<br>

## 보이스카우트 규칙

> 캠프장은 처음 왔을 때보다 더 깨끗하게 해 놓고 떠나라.

- 시간이 지나도 언제나 깨끗하게 유지해야 한다.

- 체크아웃할 때보다 더 깨끗한 코드를 체크인한다면 코드는 절대 나빠지지 않는다.?

- 한꺼번에 많은 코드를 정리 할 필요가 없다. 지속적으로 개선해라.

<br>

## SOLID - 객체 지향 설계의 다섯가지 원칙

- `SRP` (The Single Responsibility Principle) : 클래스에는 단 한가지 변경 이유만 존재해야 한다.

- `OCP` (The Open Closed Principle) : 클래스는 확장에 열려 있어야 하며 변경에는 닫혀 있어야 한다.

- `LIP` (The Liskov Substitution Principle) : 상속받은 클래스는 기초 클래스를 대체할 수 있어야 한다.

- `DIP` (The Dependency Inversion Principle) : 추상화에 의존해야 하며, 구체화에 의존하면 안된다.

- `ISP` (The Interface Segregation Principle) : 클라이언트에 밀접하게 작게 쪼개진 인터페이스를 유지한다.

<br>

## 결론

- 깨끗한 코드에 대한 정보를 제공해주겠다.

- 단 좋은 코드를 짜기위해서는 `연습`을 해야한다. 