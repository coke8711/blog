---
date: 2019-04-02T16:07:11+09:00
title:       "ArrayList, Set, TreeSet, TreeMap, Deque, ArrayDeque"
authors: ["junhwankim"]
categories:
  -
tags:
  -
---

## ArrayList

java.util.List<E>인터페이스의 대표적인 클래스입니다.
ArrayList<E>클래스는 이름대로, 내부에서 배열을 이용한 List<E> 인터페이스를 구현합니다.
List구조로 구현하고 있기 때문에 내부요소에 대한 람다접근의 퍼포먼스가 빠릅니다.
하지만 리스트에 요소를 추가하는데는, 새로운 배열을 작성해서 모든 요소를 하나씩 인덱스의 위치에 복사할 필요가 있어
인덱스의 추가되는 요소가 선두에 가까울 수록, 요소수가 늘면 늘수록 퍼포먼스가 저하됩니다.
동기화를 하지 않기 때문에, Thread-safe가 아닙니다.

## Set, TreeSet

java.util.Set<E>인터페이스의 대표적인 클래스입니다.
java.util.Set<E>는 요소의 중복을 허용하지 않습니다.
여기서 말하는 중복하는 요소란, equals메소드에 따라 같다고 판단되는 복수의 요소를 말합니다.
Set<E>에서는 null도 유일한 요소로 인정되어 추가 가능합니다.
하지만, java.util.concurrent.ConcurrentSkipListSet<E>클래스와 같은 null을 허용하지않는 클래스도 있습니다.

java.util.TreeSet<E>는 트리구조로 구현되어, 요소 정렬을 지원합니다.
동기화를 하지 않기 때문에, Thread-safe가 아닙니다.
Thread-Safe 한 Set<E>오브젝트가 필요할 경우에는 Collections.synchronizedSet메소드에 따른 동기화 Set이나
Concurrent Collection의 java.util.concurrent패키지의 CopyOnWriteArraySet<E>클래스,
ConcurrentSkipListSet<E>클래스 등의 사용할 수 있습니다.
  
## TreeMap

java.util.Map<K, V>인터페이스의 대표적인 클래스입니다.
TreeMap은 key 관리를 위해서 TreeSet<K>클래스를 사용합니다.
  
## Duque, ArrayDeque

java.util.Deque<E>인터페이스는 Queue<E>인터페이스의 서브 인터페이스입니다.
양쪽으로 요소의 추가, 삭제가 가능한 데이터 구조입니다.

```
꺼내기 : getLast 또는 removeLast                       getFirst 또는 removeFirst
             앞  ○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○○ 뒤
삽입 : addFirst                                        addLast
```

ArrayDeque<E>클래스는 내부에 배열을 사용한 Deque인터페이스로 구현됩니다.
FIFO(Queue)로 사용되는 경우에는, LinkedList<E>클래스를 사용하는 것 보다 빠릅니다.
FILO(Stack)로 사용되는 경우에는, java.util.Stack<E>클래스를 사용하는 것 보다 빠릅니다.
하지만, Thread-safe하지 않습니다.
