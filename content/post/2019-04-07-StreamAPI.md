---
layout:     post
title:       "Stream API"
subtitle:    ""
description: "Stream API에 대한 메모"
date:        2019-04-07
author:      "Junhwan Kim"
image:       "https://img.zhaohuabing.com/in-post/2018-06-02-istio08/background.jpg"
tags:        ["Java", "Stream"]
categories:  ["Tech" ]
URL: "/post/2019-04-07-stream/"
published: true
---

## Stream API

1)Stream API 기본

- 스트림 API는 데이터 집합조작용API

- 함수형 인터페이스와 람다식을 이용한다.

- 손쉬운 병렬처리를 지원한다.

- 기본적인 동작 스텝

1)데이터 소스에서 스트림 오브젝트를 가져온다.

2)스트림 오브젝트에 대해 중개연산(Intermediate Operation)을 적용한다.

 - 중개연산의 처리가 실행되는 것은 최종연산에서 한다.(지연평가)

3)스트림 오브젝트에 대한 최종연산(Terminal Operation)을 적용한다.

 - 지연되었던 모든 중개연산들이 최종연산 시 모두 수행된다.

- 스트림은 원본 데이터를 변경하지 않는다.

- 스트림은 재사용이 불가능하다.



2)java.util.stream 패키지



3)Stream, IntStream, LongStream, DoubleStream 인터페이스

- Stream<T>

- IntStream : Stream<Integer> Stream = array.stream();, static IntStream stream(int[] array, int startInclusive, int endExclusive)

 1,2,3,4,5 일 경우 start 1 end 4 일 경우 2,3,4가 해당.(1~3 번째)

- LongStream

- DoubleStream

4)stream 메소드

- 데이터소스의 List, Map등의 컬렉션을 스트림 API에서 처리하기 위해, 컬렉션 오브젝트를 스트림 오브젝트로 변환할 필요가 있다.

 그를 위해서 java.util.Collection 인터페이스에 defalut메소드로 stream메소드가 추가되었다.

- default Stream<E> stream()

5)forEach 메소드

- 스트림 API에서 제공하는 반복처리 메소드

- void forEach(Consumer<? super T> action)

- map 인터페이스의 forEach 메소드

 default void forEach(BiConsumer<? super K, ? super V> action)



6)range, rangeClosed메소드

- static IntStream range(int start, int end) -> start는 포함, end 미포함

- static IntStream rangeClosed(int start, int end) -> start는 포함, end 포함

7)of 메소드

- 임의의 참조형 오브잭트집합에서 Stream 오브젝트를 얻기 위해서 Stream 인터페이스의 static 메소드로서 제공되는 of메소드 사용



8)필터링 처리, filter 메소드

- 중간 처리 기능으로 요소를 걸러낸다.

- filter(Predicate) 판정으로 true일 경우 필터를 통과 시킨다.

9)매핑 처리, map 메소드

- 데이터의 집합을 다른 데이터로 교환해서 새 데이터집합을 생성하는 처리.

10)sorted 메소드

- 오름차순(Comparable), 임의의 순서로 하기 위해서는 Comparator 사용

11)comparing 메소드

- 정렬의 키로 사용하는 값을 전달하게 구현된 Function오브젝트를 인수를 전달

- 적절한 Comparator오브젝트를 생성해서 전달하는 기능을 제공한다.

- compare메소드는 인수를 2개 받는 추상메소드.

12)peek 메소드

- Stream<T>peek(Consumer<? super T>action

- 단순히 원본 스트림 오브잭트를 전달하는 중간조작 메소드이지만, 인수로 Consumer오브잭트를 얻어, 부작용을 동반하는 처리를 실행하는 것이 가능하다.

- 스트림 파이프라인에서 디버그목적으로 사용된다.

13)anyMatch, allMatch, noneMatch 메소드

- Predicate오브젝트를 인수로 받아, boolean형의 반환값을 전달하는 조건판정용 죄종연산 메소드

- anyMatch : 스트림의 일부요소가 지정된 조건을 만족할 때 true반환

- allMatch : 스트림의 모든요소가 지정된 조건을 만족할 때 true반환

- allMatch의 처리방법은 &&조건 처리와 비슷하다. 처리중 false 발생시 처리 멈추고 false반환

- noneMatch : 스트림의 모든요소가 지정된 조건을 만족하지 않을 경우에 true반환

14)findAny, findFirst 메소드

- 요소를 검색하는 기능. 첫번째로 찾은 요소를 반환한다.

- findAny : 병렬 작업시 유용.

- findFirst : 

15)flatMap 메소드

- flatMap()은 Array나 Object로 구성되어있는 모든 요소를 단일요소 스트림으로 반환한다.

- 해당 문제에서는 distint() 사용하여 중복 값 제거

16)merge 메소드

- 키가 존재하지 않을 경우 Bifunction오브젝트의 반환값이 키의 값으로 세팅된다.

17)reduction, count, max, min, reduce 메소드

- reduction : 스트림 오브젝트내 요소를 하나로 요약하는 최종연산

- long count() : 스트림 요소 총 개수를 반환

- max() : 스트림 요소 중 가장 큰 값

- min() : 스트림 요소 중 가장 작은 값

- reduce() : 이해는 함.

20)가변reduction 조작, 컬랙터, collect 메소드

- Collectors.cummingInt, Collectors.summingLong, Collectors.summingDouble