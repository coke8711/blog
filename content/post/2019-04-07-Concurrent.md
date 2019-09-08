---
date: 2019-04-07T16:07:11+09:00
title:       "Concurrent"
authors: ["junhwankim"]
categories:
  -
tags:
  -
---


병행성
======

# 병행처리 유틸리티

java.util.concurrent 패키지에 있는 java.util.concurrent.atomic과 java.util.concurrent.locks에 따라 구성된다.  
병행처리 유틸리티에서 제공하는 기능은 Thread Pool, 병행컬렉션, atomic 변수, 카운팅, 세마포어등이 있다.  
- Thread Pool 
  - 어플리케이션에서 필요한 스레드를 먼저 생성하여 Pool에 두어 오버헤드를 줄이고, 스레드관리성을 향상한다.  
  - Executor 프레임워크가 스레드 풀 기능을 제공한다.  

# 병행 컬랙션

- 상태에대한 접근을 직렬화 하는 것으로 thread-safe를 실현한다.  
- 병행 처리는 오히려 성능이 떨어질 수도 있다.  
- 스레드로 부터 안전하고 잘 조정된 데이터 구조를 활용하여 동시 프로그래밍을 쉽게 할 수 있다.  

# java.util.concurrent 패키지
- ConcurrentHashMap  
  - Lock Striping이라고 불리는 방식을 채용하고 있다. HashMap을 thread-safe하게 만듦  
  - 엄밀성 요건이 약화되어 있어 size메소드와 isEmpty 메소드의 반환값이 정확하지 않다.  
- CopyOnWriteArrayList
  - list 요소의 변경처리 중에 다른 스레드가 list를 읽을 경우, 복사하기 전의 리스트 요소가 전달된다.  
  - ConcurrentModificationException 을 발생시키지 않는다. 

# 세마포어(Semaphore)
- 유한의 리소스에 대한 병렬적 접근하는 프로세스와 스레드 간의 동기와 끼어들기 제어  
- 바이너리 세마포어와 카운팅 세마포어가 있다.  
- 제공되는 병행 컬렉션 : BlockingDeque, BlockingQueue, ConcurrentMap, ConcurrentNavigableMap, TransferQueue  

# CopyOnWriteArrayList, CyclicBarrier 클래스

- CopyOnWriteArraylist : 스레드에 안전하게 설계. 내용을 복사해서 전달한다.  
- CyclicBarrier : 큰 작업을 작은작업으로 분리(개별 구현) . 작업의 실행을 완료한 뒤에 흐름을 진행하도록 동기화  
- 다른 스레드가 도착하면 배리어를 삭제하고 스레드를 재개한다.  
- 처리속도가 드른 복수의 스레드가 프로그램의 실행에 있어 특정 시점까지 계산한 데이터를 교환하는데 유용함.  

# java.util.concurrent.atomic 패키지

# 아토믹 변수

- 여러 처리가 나눠지지 않고 한번에 이루어 져야 한다는 것.  
- 예를 들면 읽어드린 스테이트의 값을 변경해서 저장후 반환하는 Read-modify-write 처리는 다음과 같이 구성된다.  
```
1. state 읽기(Read)
2. 값의 변경(modify)
3. state 쓰기(write)
```
- 아토믹처리로 다루어지는 일련의 처리는 완전히 종료하거나 미실시 상태여야 한다.  
- 병렬처리 유틸리티에서, 스레드 세이프 스테이트를 선언하기 위한 클래스  
- 주요 클래스 : AtomicBoolean, AtomicInteger, AtomicLong, AtomicReference등  
- 약한 정합성으로 인해, 병행접근에 따른 요소변경을 허용한다. 아토믹조작을 서포트 한다.  
- ConcurrentLinkedDeque,  등  

# java.util.concurrent.locks 패키지

# Executor 프레임 워크

- 태스크 실행 시 라이프사이클 관리  
- 스레드 풀 구현  
- 태스크의 지연개시와 주기적 실행(스케줄링)  
- 인터페이스 : ExecutorSerive, ScheduledExecutorService  
- 메소드 : void execute(Runnable command)  
- ExecutorService 인터페이스는 Executor의 종료에 관한 기능을 제공한다.  
- boolean awaitTermination(long timeout, TimeUnit unit), boolean isShutdown(), boolean isTerminated(), void shutdown()  
- List<Runnable> shutdownNow()  

# Runnable 태스크와 Callable 태스크
Runnable 태스크  
```
public class MyTask implements Runnable {
    public void run() {
        System.out.println("OK");
    }
}
```
기존의 Thread 클래스를 사용한 태스크의 실행  
```
Runnable task = new MyTask(); // 태스크의 생성
Thread thread = new Thread(task); // 스레드의 생성
thread.start(); // 스레드 실행
```
Executor 를 사용한 태스크의 실행  
```
Runnable task = new MyTask(); // 태스크의 생성
Executor executor = // 구체적 Executor를 생성하는 코드
executor.execute(task); // 태스크의 실행
```
- Runnable 태스크는 반환값을 전달하는 것이 되지 않지만, Callable 태스크는 가능하다.  
- Runnable 태스크는 예외를 던지는 것이 되지 않지만, Callable 태스크는 가능하다.  

# Fork/Join 프레임 워크

- 멀티코어 CPU를 효율적으로 이용하는 것이 최대의 목적이다  
- Work-stealing 알고리즘을 채용하고 있다.  
- 큰 태스크를 작은 태스트로 나눠 나눈 태스크를 복수의 스레드에서 동시처리, 퍼포먼스 상승  
- java.util.concurrent.ForkJoinPool 클래스에서 제공된다.  
- ForkJoinPool, ForkJoinTask  
- ForkJoinPool 이 제공하는 메소드 : execute, invoke, submit  
- ForkJoinTaks<V> 의 서브클래스 : RecursiveTask, RecursiveAction  

# Stream의 병렬처리

- 스트림의 처리는 순차처리나 병렬처리 어느쪽이든 가능하다.  
- java.util.Collection 인터페이스의 stream 메소드를 사용할 것인가, parallelStream메소드를 사용하느냐에 따라 결정되지만  
- 스트림 처리도중에 실행모드를 변경하는 것도 가능하다.  
- 순차처리 -> 병렬처리 변경시 parallel 메소드를, 병렬처리 -> 순차처리 변경시 sequential 메소드 사용  
- 요소수나 처리내용에 따라 달라지지만 병렬처리가 꼭 뛰어나지는 않다.  
- findAny() : 스트림에서 순서에 상관없이 일치하는 값 하나를 반환  

# 쓰레드 클래스의 문제점

- 스레드 수의 상한을 설정하는 것이 되지않아, 메모리 관리에 실패해, 정지하는 경우  
- 스레드의 생성에 따른 오버헤드와 리소스를 무의미하게 소비.  

# Future<V> 인터페이스
- 비동기로 태스크를 실행했을 때 필요로 하는 여러가지 기능을 정의 하고있다.  
- 태스크 취소시행, 태스크 완료 판정  