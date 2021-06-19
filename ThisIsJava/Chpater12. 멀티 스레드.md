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

- 모든 스레드가 종료되어야 프로세스가 종료된다.


### 작업 스레드 생성과 실행

- java.lang.Thread 클래스를 직접 객체화해서 생성

- Thread를 상속해서 하위 클래스를 만들어 생성


#### Thread 클래스로부터 직접 생성

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

#### Thread 하위 클래스로부터 생성

- Thread 클래스를 상속한 후 run 메소드를 overriding 해서 스레드가 실행 코드를 작성

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

#### Thread의 이름

- 스레드의 이름은 디버깅 할때 유용

```java
// 스레드 객체의 참조를 가지고 있을 때.
thread.setName("스레드 이름");
thread.getname();
// 가지고 있지 않다면
Thread.currentThread(); // 스레드 참조를 얻을 수 있다.
```

### 스레드 우선순위

**동시성(Concurrency)**

- 하나의 코어에서 멀티 스레드가 번갈아가며 실행하는 성질

**병렬성(Parallelism)**

- 멀티 코어에서 개별 스레드를 동시에 실행하는 성질



### 스레드 우선순위

#### 동시성(Concurrency)

- 하나의 코어에서 멀티 스레드가 번갈아가며 실행하는 성질

#### 병렬성(Parallelism)

- 멀티 코어에서 개별 스레드를 동시에 실행하는 성질














