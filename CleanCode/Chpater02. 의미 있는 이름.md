# Chpater02. 의미 있는 이름

## 의도를 분명히 밝혀라.

변수, 함수, 클래스의 이름은 다음과 같은 질문에 모두 답해야 한다.
- 존재 이유?

- 수행 기능?

- 사용 방법?

의도가 들어가는 이름을 사용하라.

```java
// Bad
int d; // 경과시간(단위: 날짜)

// Good
int elapsedTimeInDays;
int daysSinceCreation;
int daysSinceModification;
int fileAgeInDays;
```

`코드의 함축성` = 코드 맥락이 코드 자체에 명시적으로 드러나야 한다.

```java
// Bad
public List<int[]> getThem(){
    List<int[]> list1 = new ArrayList<int[]>();
    for(int[] x : theList)
        if (x[0] == 4)
            list1.add(x);
    return list1;
}

// Not Bad
// 각 개념에 이름을 붙임
// theList = gameBoard
// 배열의 0번째 값은 칸 상태, 값 4는 깃발이 꽂힌 상태
public List<int[]> getFlaggedCells(){
    List<int[]> flaggedCells = new ArrayList<int[]>();
    for(int[] cell : gameBoard)
        if (cell[STATUS_VALUE] == FLAGGED)
            flaggedCells.add(cell);
    return flaggedCells;
}

// Good
// int[]을 사용하는 대신, 칸을 Cell클래스로 만든다.
// isFlagged라는 좀 더 명시적인 함수를 사용해서 FLAGGED라는 상수를 감추겠다.
public List<Cell> getFlaggedCells(){
    List<Cell> flaggedCells = new ArrayList<Cell>();
    for(Cell cell : gameBoard)
        if (cell.isFlagged())
            flaggedCells.add(cell);
    return flaggedCells;
}
```

<br>

## 그릇된 정보를 피하라.

> 프로그래머는 코드에 그릇된 단서를 남겨서는 안된다.

나름대로 널리 쓰이는 의미가 있는 단어를 다른 의미로 사용하지 마라.

- 예를 들어 빗변(hypotenuse)을 hp라는 변수로 사용할 때, 훌륭한 약어처럼 보이지만 hp는 유닉스 플렛폼의 한 종류로 널리 사용되는 단어이므로 hp라는 변수는 독자에게 그릇된 정보를 제공한다.

여러 계정을 그룹으로 묶을 때, 실제 List가 아니라면, acccountList라 명명하지 마라.

- 대신 accountGroup, bunchOfAccounts, Accounts를 사용하라.

일관성이 떨어지는 모듈 간에 서로 흡사한 이름을 사용하지 마라.

- XYZControllerForEfficientHandlingOfStrings 와  XYZControllerForEfficientStorageOfStrings

소문자 l 은 숫자 1 처럼 보이고 대문자 O 는 숫자 0 처럼 보이므로 사용하지 마라.

<br>

## 의미 있게 구분하라.

> 읽는 사람이 차이를 알도록 이름을 지어라.  
> 이름이 달라야 한다면 의미도 달라져야 한다.


연속적인 숫자를 덧붙인 이름은 아무런 정보를 제공하지 못하는 이름이다.

```java
public static void copyChars(char a1[], char a2[]){ 
    // a1 -> source, a2-> destination
  for (int i =0; i < a1.length; i++){
    a2[i] = a1[i];
  }
}
```

불용어를 추가한 이름 역시 아무런 정보도 제공하지 못한다.

- Product : ProductInfo, ProductData

- Name : NameString

- getActiveAccount(), getActiveAccounts(), getActiveAccountInfo()

<br>

## 발음하기 쉬운 이름을 사용하라.

> 프로그래밍은 사회 활동이다.   
> 발음하기 어려운 이름은 대화하기도 어렵다.

```java
// Bad
class DtaRcrd102{
    private Date genymdhms;
    private Date modymdhms;
    private final String pszqint = "102"
}

// Good
class Customer{
    private Date createdAt;
    private Date modifiedAt;
    private final String recordId = "102"
}
```

<br>

## 검색하기 쉬운 이름을 사용하라.

이름 길이는 범위 크기에 비례해야 한다.  
변수나 상수를 코드 여러곳에서 사용한다면 길어도 검색하기 쉬운 이름이 바람직하다.

```java
// Bad
for(int j = 0; i < 34; j++){
    s += (t[j]*4)/5;
}

// Good
// 한 주에 일하는 날짜가 4일로 추정해서 잡은 일의 일정이 한 주에 5일 일한다면
// 일을 끝마치는데 몇 주가 걸리는지 계산하는 프로그램
int realDaysPerIdealDay = 4;
const int WORK_DAYS_PER_WEEK = 5;
int sum = 0;
for(int j = 0; j < NUMBER_OF_TASKS; j++){
    int reaTaskDays = taskEstimate[j] * realDaysPerIdealDay;
    int realTaskWeeks = (realTaskDays / WORK_DAYS_PER_WEEK);
    sum += realTaskWeeks;
}
```

<br>

## 인코딩을 피하라.

> 유형이나 범위 정보까지 인코딩에 넣으면 그만큼 이름을 해독하기 어려워진다.

**헝가리식 표기법**

```java
PhoneNumber phoneString; // 타입이 바뀌어도 이름은 바뀌지 않는다.
```

- 자바 프로그래머는 변수 이름에 타입을 인코딩할 필요가 없다.

- 자바는 언어에서 타입 오류가 항상 탐지될 수 있는  강한 타입(strongly-typed)의 언어이다.

- IDE는 코드를 컴파일 하지 않고도 타입 오류를 감지할 정도로 발전했다.

**멤버 변수 접두어**

- 멤버 변수에 m_이라는 접두어를 붙일 필요 없다.

- 클래스와 함수는 접두어가 필요없을 정도로 작아야 마땅하다.

- 멤버 변수를 다른 색상으로 표시하거나 눈에 띄게 보여주는 IDE를 사용해야 마땅하다.

- 접두어는 옛날에 작성한 구닥다리 코드라는 징표가 된다.

```java
// Bad
public class Part {
    private String m_dsc; // 설명 문자열
    void setName(String name){
        m_dsc = name;
    }
}

// Good
public class Part {
    private String description;
    void setDescription(String description){
        this.description = description;
    }
}
```

**인터페이스 클래스와 구현 클래**

- 인터페이스 클래스 이름과 구현 클래스를 인코딩 해야한다면 구현 클래스의 이름을 택하라.

```java
public interface ShapeFactory {}

public class ShapeFactoryImpl implements ShapeFactory {}
```

<br>

## 자신의 기억력을 자랑하지 마라.

> 독자가 코드를 읽으면서 변수 이름을 실제 개념으로 변환해야 한다면 그 변수 이름은 바람직하지 못하다.

- 예를 들어 url을 변수 r로 설정

- 전문가 프로그래머는 `명료함이 최고`라는 사실을 이해한다.

- 전문가 프로그래머는 `남들이 이해하는 코드`를 내놓는다.

<br>

## 클래스와 메서드 이름

**클래스 이름과 객체 이름**

- 명사나 명사구가 적합하다.

-  Customer, WikiPage, Account, AddressParser 등이 좋은 예

- Manager, Processor, Data, Info 등과 같은 단어는 피한다.

- 동사는 사용하지 않는다.


**메서드 이름**

- 동사나 동사구가 적합하다.

- pstPayments, deletePage, save 등이 좋은 예

- 접근자(Accessor), 변경자(Mutator), 조건자(Predicate)는 javabean 표준에 따라 값 앞에 get, set, is를 붙인다.

```java
String name = employee.getName;
customer.setName("mike");
if (paycheck.isPosted()) ...
```

- 생성자를 중복 정의할 때는 정적 팩토리 메서드를 사용한다.

```java
// Bad 
Complex fulcrumPoint = new Complex(23.0);

// Good
Complex fulcrumPoint = Complex.FromRealNumber(23.0);
```

<br>

## 기발한 이름은 피하라.

> 의도를 분명하고 솔직하게 표현하라.

- 재미난 이름보다는 `명료한` 이름을 택하라.

```java
// Bad
void HolyHandGrenade(){} // <몬티 파이썬>에 나오는 수류탄 이름

// Good
void DeleteItems() {}
```

<br>

## 한 개념에 한 단어를 사용하라.

추상적인 개념 하나에 단어 하나를 선택해 이를 고수한다.

- fetch, retrieve, get 등

메서드의 이름은 독자적이고 일관적이어야 주석을 뒤져보지 않고도 올바른 메서드를 선택할 수 있다.

 - ``독자적`` : 다른 것과 구별되는 혼자만의 특유한 것

클래스도 마찬가지로 동일 코드 기반에 controller, manager, driver를 섞어 쓰면 혼란스럽다.

<br>

## 말장난을 하지마라.

> 대충 훑어봐도 이해하기 쉽게 짜야한다. 즉 의도를 밝힐 책임이 저자에에게 있다.

다른 개념에 같은 단어를 사용하지 마라.

- 기존의 add : 두 값을 더해 새로운 값을 만들어내는 함수

- 집합에 값을 더하는 함수도 일관성을 고려해 add를 선택한다면 이는 말장난이다.

    - insert, append를 선택하라.

<br>

## 해법 영역에서 가져온 이름을 사용하라.

- 모든 이름을 문제 영역(domain)에서 가져오는 것은 현명하지 못하다.

- 코드를 읽는 독자는 프로그래머이므로 프로그래머에게 친숙한 언어를 사용하라.

- 기술 개념에는 기술 이름이 가장 적합한 선택이다.

<br>

## 문제 영역에서 가져온 이름을 사용하라.

- 적절한 `프로그래머 용어`가 없다면 문제 영역에서 이름을 가져온다.

- 문제 영역 개념과 관련이 깊은 코드라면 문제 영역에서 이름을 가져와야 한다.

<br>

## 의미 있는 맥락을 추가하라.

- 대다수의 이름은 스스로 의미가 분명하지 않다.

- firstName, lastName, street, houseNumber, city, state, zipcode 중 하나의 단어만으로는 의미가 분명하지 않다.

- 전체 맥락에서 주소라는 `의미`를 가질 수 있다.

- Address라는 클래스를 생성하여 변수들을 관리하면 더 좋다.


```java
// Bad
// 함수가 너무 길며, 메서드만 훑어서는 세 변수의 의미가 불분명하다.
private void printGuessStatistics(char candidate, int count){
    String number;
    String verb;
    String pluralModifier;

    if(count == 0) {
        number = "no";
        verb = "are";
        pluralModifier = "s";
    } else if (count == 1) {
        number = "1";
        verb = "is";
        pluralModifier = "";
    } else {
        number = Integer.toString(count);
        verb = "are";
        pluralModifier = "s";
    }
    
    String guessMessage = String.format(
        "There %s %s %s", verb, number, candidate, pluralModifier);
    )
    print(guessMessage);
}

// Good
// 함수를 작은 조각으로 쪼개고자 GuessStatisticsMessage 라는 클래스를 만들었다.
// GuessStatisticsMessage 안에 세 변수를 넣으니 세 변수의 맥락이 분명해졌다.
public class GuessStatisticsMessage {
    private String number;
    private String verb;
    private String pluralModifier;

    public String make(char candidate, int count) {
        createPluralDependentMessageParts(count);
        return String.format(
            "There %s %s %s",
            verb, number, candidate, pluralModifier);
    }
    
    private void createPluralDependentMessageParts(int count){
        if(count == 0) {
            thereAreNoLetters();
        } else if (count == 1){
            thereIsOneLetter();
        } else {
            thereAreManyLetters(count);
        }
    }
    
    private void thereAreNoLetters() {
        number = "no";
        verb = "are";
        pluralModifier = "s";
    }

    private void thereIsOneLetter() {
        number = "1";
        verb = "is";
        pluralModifier = "";
    }

    private void thereAreManyLetters() {
        number = Integer.toString(count);
        verb = "are";
        pluralModifier = "s";
    }
}
```

<br>

## 불필요한 맥락을 없애라.

고급 휘발유 충전소(Gas Station Deluxe)라는 어플리케이션을 짠다고 가정하자.

- 모든 클래스 이름을 GSD로 시작한다는 생각은 바람직하지 않다.

의미가 분명하다면 실세계의 이름을 그대로 사용해도 좋다.

- accountAddress, custommerAddress 보다는 Address가 적합하다.

- 포트 주소, MAC 주소, 웹 주소는 PostalAddress, MAC, URI 가 적합하다.

<br>

## 마치면서

- 좋은 이름을 선택하려면 설명 능력이 뛰어나야 하고, 문화적 배경이 같아야한다. 이것이 제일 어렵다.

- 우리는 쉽게 읽히는 코드를 짜는데 집중해야한다.