---
layout:     post

title:       "함수형 인터페이스"
subtitle:    ""
description: "함수형 인터페이스에 대한 메모"
date:        2019-04-07
author:      "Junhwan Kim"
image:       "https://img.zhaohuabing.com/in-post/2018-06-02-istio08/background.jpg"
tags:        ["Java", "Funtional"]
categories:  ["Tech" ]
URL: "/post/2019-04-07-function/"
published: true
---

## 함수형 인터페이스

- 인터페이스에 선언되어있는 추상메소드가 하나만 있을 경우 그 인터페이스를 함수형 인터페이스(Functional Interface)라고 부른다.

- SAM(Single Abstract Method)라고 부르기도 한다.

- java.lang.Runnable : void run()

- java.util.Comparator<T> : int compare(T o1, T o2)

- java.nio.file.PathMatcher : boolean matches(Path path)

- java.util.cuncurrent.Callable<V> : V Call()

- 인터페이스에 있는 default, static 메소드는 추상클래스가 아니다.

- 함수형 인터페이스로서 타당한지를 컴파일시 체크 하기위한 어노테이션 java.lang.@FunctionalInterface가 추가되었다.

3)java.util.function 패키지



4)Supplier, Predicate, Consumer, Function 인터페이스

- Supplier<T> : 입력을 받지않고 T를 반환한다. T get()을 선언하는 함수형 인터페이스

- Predicate<T> : T를 입력받아 boolean을 출력으로 반환 boolean test(T t)을 선언하는 함수형 인터페이스

- Consumer<T> : T를 입력받아 아무것도 반환하지 않는다. 입력받은 데이터 처리시 사용. void accept(T t)

- Function<T, R> : T를 입력으로 R을 출력하여 반환. R apply(T t)로 선언하는 함수형 인터페이스 

- BiFunction<T, U, R> : R apply(T t, U u)

- BiConsumer<T, U> : void accept(T t, U u)

- BiPredicate<T, U> : boolean test(T t, U u)

- UnaryOperation<T> : T apply(T t) 매개변수 1개로 반환타입과 동일

- BinaryOperation<T> : T apply(T t, T t) 매개변수 2개로 반환타입과 동일



5)메소드참조

- 람다식이 어떠한 이유로 메소드만 호출하고 끝나며, 함수형 인터페이스의 SAM인 추상메소드와, 람다식이 호출하는 메소드가 시그니쳐가 동일한 경우 메소드 참조를 사용할 수 있다.

- 클래스명::메소드명

- 인스턴스변수명::메소드명

