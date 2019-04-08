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


```
public static void main(String[] args){
    try{
        x();
    }catch(Throwable e){
        while(e != null)
        {
            System.out.println(e.getMessage());
            e = e.getCause();
        }
    }
}

static void x() throws Exception{
    try{
        y();
    } catch(Exception e){
        throw new Exception("exception in x()", e);
    }
}

static void y() throws Exception{
    try{
        z();
    } catch(Exception e){
        throw new Exception("exception in y()", e);
    }
}

static void z() throws Exception{
    throw new Exception("exception in z()");
}
```

## try-catch문과 throw문

- 보통의 catch문

```
try {
    //예외가 발생할 가능성이 있는 처리
} catch (IOException e)
{
    //예외 처리
} catch (NumberFormatException e)
{
    //예외 처리
} catch (ParseException e)
{
    //예외 처리
}
```

## multi-catch 문

- 복수의 catch 블록을 하나로 모아서 처리할 수 있다.

- 주의 사항: 사용된 예외들은 예외의 상속관계에서 부모 자식관계에 있으면 안된다.

```
try {
    // 예외가 발생할 가능성이 있는 처리
} catch(IOException | NumberFormatException | ParseException e){
    // 예외 처리
}
```
복수의 multi-catch문과 보통 catch 문 
```
try {
    // 예외가 발생할 가능성이 있는 처리
} catch (NumberFormatException | ParseException e) { // multi-catch 1
    // 예외 처리
} catch (SQLException | IOException e) { // multi-catch 2
    // 예외 처리
} catch (Exception e) { // 보통의 catch
    // 예외 처리
}
```

## 독자 예외 클래스

- 독자 예외클래스와 에러 클래스를 사용하기 위해서는 java.lang.Throwable 클래스 또는 서브클래스를 상속받을 필요가 있다.

- 일반적으로는 java.lang.Exception 클래스를 사용한다.

```
public class MyException extends Exception {
    // 구현
}
```

- 작성한 예외 클래스는 try-catch 문의 catch 블록의 인수로 지정이 가능하다.

```
try {
    doIt();
} catch (MyException e){
    .. 예외 처리
}

void doIt(int value){
    if(value < 0){
        throw new MyException();
    }
}
```

## try-with-resource 문

- 파일이나 데이터베이스등 외부 리소스를 이용할 때 오픈한 리소스를 자동적으로 클로즈 하는 구조를 제공한다.

보통의 try-catch 구문(java SE 6 이전)

```
FileReader in = null;
FileWriter out = null;

try{
    in = new FileReader("in.txt");
    out = new FileReader("out.txt");
    // 파일의 읽기, 쓰기
} catch (IOException e){
    // 파일 열기, 읽기 쓰기에 대한 예외 처리
} finally {
    try {
        if (in != null){
            in.close(); // FileReader의 close() 처리
        }
        if (out != null){
            out.close(); // FileWriter의 close() 처리
        }
    }catch (IOException e){
        // close method 에 대한 예외 처리
    }
}
```

java SE 7부터 도입된 try-with-resources 문

```
try (FileReader in = new FileReader("in.txt");
    FileWriter out = new FileReader("out.txt")) {
        // 파일의 읽기, 쓰기
    } catch (IOException e){
        // 예외 처리
    }
```

- 꼭, catch 블록, finally 블록이 필요한 것은 아니다.

## 리소스의 close(), AutoCloseable 인터페이스

- try-with-resources 문의 try블록에 인수로 이용가능한 클래스는 java.lang.AutoCloseable 인터페이스를 implements 하거나 그의 서브클래스가 아니면 안된다.

```
class MyResource implements AutoCloseable {
    public void close(){
        // close 처리
        System.out.println("closing");
    }
}

public class Example {
    public static void main(String[] args) {
        try (MyResource resource = new MyResource()) {
            System.out.println("OK");
        } // 여기서 MyResource 클래스의 close메소드가 자동적으로 실행된다.
    }
}
```

## Assertion

```
assert 조건식;
```

조건식이 false 일 경우 java.lang.AsesertionError 가 발생한다.

```
assert(x ==1); // 공백 없음
assert (x == 1); //공백 있음, 둘 다 가능.

assert 조건식 : 인수  
assert x ==1 : "Error Message";
```

- 프로그램 실행시 -ea옵션을 추가하면 assertion기능을 사용할  수 있다. 