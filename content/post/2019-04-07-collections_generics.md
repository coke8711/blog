---
date: 2019-04-07T16:07:11+09:00
title:       "collections와 generics"
authors: ["junhwankim"]
categories:
  -
tags:
  -
---

## 컬렉션과 제네릭스

컬렉션 API(프레임워크) : 복수의 데이터를 하나로 모아서 다루기 위한 데이터 구조, 유틸리티 기능

1)제네릭 클래스, 제네릭 인터페이스

- 제네릭 : 클래스에서 사용할 타입을 클래스 외부에서 설정

- 객체의 타입 범용성, 실행시 형변환의 안정성을 높여준다.

- 제네릭 클래스 구현시 되지 않는 것.

- static 키워드를 사용한 형변수

- 형변수에 따른 인스턴스 생성

- 형변수를 요소에 지정하는 배열의 생성

- instanceof 연산자에 따른 형의 판정

- 형변수에 대한.class의 참조

2)type 파라미터, 형변수, 형인수

- <? extends 자료형> : 명시된 type을 상속한 하위객체, <T super 자료형> : 명시된 type의 상위객체 T도 들어감

3)제네릭 메소드

- 제네릭 메소드 : 메소드 선언에 있는 반환값의 앞에 형 type 파라메터를 선언할 필요가 있다.

4)형경계

5)java.util.List

- 인덱스로 순서를 붙일 수 있는 데이터 구성

- ArrayList<E>, LinkedList<E>, Vector<E>, CopyOnWriteArrayList<E>

6)java.util.Arrays

- 배열을 다루기 위한 다양한 메소드가 포함되어 있다. 객체를 생성하지 않고도 바로 사용가능

- binarySearch() : 배열에서 특정 객체의 위치를 이진 검색 알고리즘을 사용하여 검색 후 위치 반환

- copyOf() : 전달 받은 배열의 특정 길이만큼을 새로운 배열로 복사하여 반환

- copyOfRange() : 전달 받은 배열의 특정 범위에 해당하는 요소만을 새로운 배열로 복사하여 반환

- fill() : 전달받은 배열의 모든 요소를 특정값으로 초기화

- sort() : 배열의 모든 요소를 오름차순으로 정렬합니다.

- asList : 배열에서 list로 생성

7)java.util.Queue, java.util.Deque

- Queue는 FIFO(선입선출)의 자료구조

- Deque는 양쪽에서 요소를 투입, 삭제 가능한 데이터 구조

- ArrayDeque<E>는 FIFO(선입선출)을 사용할 때는 LinkedList<E>클래스를 사용하는 것 보다 빠르다.

- ArrayDeque<E>는 FILO(후입선출)을 사용할때는 java.util.Stack<E> 클래스를 사용하는 것 보다 빠르다.

- null을 넣을 수 없다.

- ArrayDeque<E>는 thread에서 안전하지 않기 때문에 멀티 스레드 일 경우에는 stack<E>를 사용하는 것이 안전하다. 

8)java.util.Set, java.util.HashSet, java.util.TreeSet

- Set은 중복허용하지 않는다.

- Set은 저장 순서를 유지하지 않는다.

9)java.util.Map, java.util.HashMap, java.util.TreeMap

- Map은 키와 값을 하나로 저장하는 방식이다.

- Hash맵은 검색속도 가 빠르다.

- TreeMap은 데이터의 추가 제거 시간이 빠르다.

10)java.lang.Comparable, java.util.Comparator

- 오브잭트의 비교와 순서에 관련 한 인터페이스로 제공된다. 

- Comparable<T> : 객체를 비교하는데 사용되는 메소드인 compareTo()메소드 정의., set

- public int compareTo(Product p){

return this.id - p.id;

}

- boolean을 제외한 인스턴스 정렬 가능. 오름차순

- ComParator<T> : 오름차순 이외의 내림차순이나 다른 기준으로 정렬할 수 있다. 

- public int compare(Product p1, Product p2){

return p1.id - p2.id;

}
