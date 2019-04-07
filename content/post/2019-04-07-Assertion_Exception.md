---
layout:     post
title:       "Assertion And Exception"
subtitle:    ""
description: "Assertion And Exception에 대한 메모"
date:        2019-04-07
author:      "Junhwan Kim"
image:       "https://img.zhaohuabing.com/in-post/2018-06-02-istio08/background.jpg"
tags:        ["Java", "Assertion", "Exception"]
categories:  ["Tech" ]
URL: "/post/2019-04-02-assertion_and_exception/"
published: true
---

## 예외와 Assertion

- 메소드 내에서 예외를 던질 때는 throw문을 사용한다.

- throw new Exception();

- Throwable getCause() : Exception을 발생 시킨 Throwable object 를 반환

1)try-catch문과 throw문

- 

2)multi-catch 문

- 복수의 catch 블록을 하나로 모아서 처리할 수 있다.

- 주의 사항: 사용된 예외들은 예외의 상속관계에서 부모 자식관계에 있으면 안된다.

3)독자 예외 클래스

- 독자 예외클래스와 에러 클래스를 사용하기 위해서는 java.lang.Throwable 클래스 또는 서브클래스를 상속받을 필요가 있다.

- 일반적으로는 java.lang.Exception 클래스를 사용한다.

4)try-with-resource 문

- 파일이나 데이터베이스등 외부 리소스를 이용할 때 오픈한 리소스를 자동적으로 클로즈 하는 구조를 제공한다.

- 꼭, catch 블록, finally 블록이 필요한 것은 아니다.

5)리소스의 클로즈, AutoCloseable 인터페이스

- java.lang.AutoCloseable 인터페이스를 implements 해야, try-with-resource문을 사용 할 수 있다.

6)Assertion

- assert(x ==1);

- assert (x == 1); 둘 다 가능.

- assert 조건식 : 인수  ex) assert x ==1 : "Error Message";

- 프로그램 실행시 -ea옵션을 추가하면 assertion기능을 사용할  수 있다. 