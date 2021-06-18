# Chpater02. 의미 있는 이름

## 1. 의도를 분명히 밝혀라.

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
int daysSinceCreatino;
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

## 2. 그릇된 정보를 피하라.

> 프로그래머는 코드에 그릇된 단서를 남겨서는 안된다.

나름대로 널리 쓰이는 의미가 있는 단아를 다른 의미로 사용하지 마라.

- 예를들어 빗변(hypotenuse)를 hp라는 변수로 사용할 때, 훌륭한 약어처럼 보이지만 hp는 유닉스 플렛폼의 한 종류로 널리 사용되는 단어이므로 hp라는 변수는 독자에게 그릇된 정보를 제공한다.

여러계정을 그룹으로 묶을 때, 실제 List가 아니라면, acccountList라 명명하지 마라.
- 대신 accountGroup, bunchOfAccounts, Accounts를 사용하라.

일관성이 떨어지는 모듈 간에 서로 흡사한 이름을 사용하지 마라.

- XYZControllerForEfficientHandlingOfStrings 와  XYZControllerForEfficientStorageOfStrings

소문자 l 은 숫자 1 처럼 보이고 대문자 O 는 숫자 0 처럼 보이므로 사용하지 마라.



## 3. 의미 있게 구분하라.

> 이름이 달라야 한다면 의미도 달라져야 한다.
> 읽는 사람이 차이를 알도록 이름을 지어라.

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


