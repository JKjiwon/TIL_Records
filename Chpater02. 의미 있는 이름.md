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