# Chpater12. 멀티 스레드

## 멀티 스레드 개념

### 프로세스와 스레드

#### 멀티 테스킹

- 두가지 이상의 작업을 동시에 처리하는 것.

- 운영체제는 CPU 및 메모리 자원을 프로세스마다 적절히 할당하고, 병렬로 실행

- 멀티 프로세스 : 프로세스 마다 독립된 메모리를 가지고 있다.

- 멀티 스레드 : 하나의 프로세스 내 메모리를 공유한다.


### 메인 스레드

- main() 메소드를 실행하면서 시작하고 첫 코드부터 순차적으로 실행

- 필요에 따라 작업 스레드를 만들어서 병렬로 코드를 실행 가능

- 프로세스는 모든 스레드가 종료되어야 종료된다.

<br>

## 작업 스레드 생성과 실행

- java.lang.Thread 클래스를 직접 객체화해서 생성

- Thread를 상속해서 하위 클래스를 만들어 생성


### Thread 클래스로부터 직접 생성

```java
// Runnable을 매개값으로 갖는 생성자 호출
Thread thread = new Thread(Runnable target);

// Runnable은 인터페이스 타입이기 대문에 구현 객체를 만들어 대입
class Task implements Runnable {
    public void run() {
        스레드가 실행할 코드;
    }
}

// Runnable 객체를 매개값으로 갖는 Thread 생성자 호출
// 비로소 작업 스레드가 생성됨 
Runnalbe task = new Task();
Thread thread = new Thread(task);

// 스레드의 실행
thread.start();

// 람다식 이용
Thread thread = new Thread(
    () -> {
        스레드가 실행할 코드;
    }
);
thread.start();
```

### Thread 하위 클래스로부터 생성

- Thread 클래스를 상속한 후 run 메소드를 overriding 해서 스레드가 실행할 코드를 작성

```java
public class WorkerThread extends Thread {
    @Override
    public void run() {
        // 스레드가 실행할 코드
    }
}
Thread thread = new WorkerThread();

// 익명 객체로 생성
Thread thread = new Thread() {
    public void run() {
        스레드가 샐행할 코드;
    }
}
```

### Thread의 이름

- 스레드의 이름은 디버깅 할때 유용

```java
// 스레드 객체의 참조를 가지고 있을 때.
thread1.setName("스레드 이름");
thread1.getname();
// 가지고 있지 않다면
Thread thread2 = Thread.currentThread(); // 스레드 객체의 참조를 얻을 수 있다.
```

<br>

## 스레드 우선순위

- **동시성(Concurrency)** : `하나의 코어`에서 멀티 스레드가 번갈아가며 실행하는 성질

- **병렬성(Parallelism)** : `멀티 코어`에서 개별 스레드를 동시에 실행하는 성질

    ![동시성vs병렬성](/ThisIsJava/images/thread01.png)

### 스레드 스케쥴링

- 스레드의 개수가 코어의 수보다 많을 경우

- 스레드를 어떤 순서에 의해 동시성으로 실행할 것인가를 결정하는 것

**우선순위(Priority) 방식**

- 우선순위가 높은 스레드가 실행 상태(CPU 자원)를 더 많이 가지도록 하는 스케쥴링

- 스레드 객체에 우선 순위 번호를 부여할 수 있어, 개발자가 코드로 제어 가능

```java
thread.setPriority(우선순위); // 1 ~ 10 까지 설정 가능, 10이 가장 높다.

// 코드의 가독성을 위해 스레드 상수를 이용
thread.setPriority(Thread.MAX_PRIORITY); // 10
thread.setPriority(Thread.NORM_PRIORITY); // 5
thread.setPriority(Thread.MIN_PRIORITY); // 1
```

**순환 할당(Round-Robin) 방식**

- 시간 할당량(Time Slice)을 정해서 하나의 스레드를 정해진 시간만큼 실행하고 다시 다른 스레드를 실행하는 방식

- 자바 가상 머신(JVM)에 의해서 정해지기 때문에, 개발자가 제어 불능

<br>

## 동기화 메소드와 동기화 블록

### 공유 객체를 사용할 때의 주의할 점

- 두 스레드가 동일한 메모리 필드에 접근하고자 할 때

    ![공유객체](images/shared_object.png)

    user1의 결과가 100이 아니라 50이 나온다.


### 동기화 메소드 및 동기화 블록

- 스레드가 사용중인 객체를 다른 스레드가 변경할 수 없도록 하려면

- 스레드 작업이 끝날 때까지 `객체에 잠금을 걸어서` 다른 스레드가 사용할 수 없도록 해야한다.

- 임계영역(critical section) : 멀티 스레드 프로그램에서 `단 하나의 스레드만 실행할 수 있는 코드 영역`

- 임계 영역을 지정하기 위해 동기화(synchronized) 메소드와 동기화 블럭을 제공

- 스레드가 객체 내부의 동기화 메소드 또는 블록에 들어가면 `즉시 잠금을 걸어` 다른 스레드가 임계 영역의 코드를 실행하지 못하도록 한다.

#### 동기화 메소드

- 메소드 선언 앞에 synchronized 키워드를 붙인다.

- 메소드 전체에 잠금이 일어난다.

```java
public synchronized void method() {
    임계 영역; // 단 하나의 스레드만 실행 가능
}
```

#### 동기화 블럭

- 메소드 일부 영역에 잠금이 일어난다.

```java
public void method() {
    // 여러 스레드가 실행 가능 영역
    synchronized(공유객체) {
        // 임계영역 = 단 하나의 스레드만 실행 가능
    }
    // 여러 스레드가 실행 가능 역역
}
```

![동기화](images/synchronized.png)

**주의점**
- 동기화 블럭과 동기화 메소드가 여러개 있을 경우, 스레드가 이들 중 하나를 실행할 때 다른 스레드는 해당 메소드는 물론 다른 동기화 메소드 및 블록도 샐행 할 수 없다.

<br>

## 스레드 상태

1. start() 메소드를 호출하면 스레드가 실행 대기 상태가 된다.
    - 실행 대기 상태 : 아직 스케쥴링이 되지 않아서 실행을 기다리고 있는 상태    

2. 실행 대기 상태에 있는 스레드 중에서 스레드 스케쥴링으로 선택된 스레드가 비로소 CPU를 점유하고 run() 메소드를 실행




