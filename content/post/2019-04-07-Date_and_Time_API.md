---
layout:     post

title:       "날짜 / 시각 API"
subtitle:    ""
description: "날짜 / 시각 API에 대한 메모"
date:        2019-04-07
author:      "Junhwan Kim"
image:       "https://img.zhaohuabing.com/in-post/2018-06-02-istio08/background.jpg"
tags:        ["Java", "API"]
categories:  ["Tech" ]
URL: "/post/2019-04-07-Date_and_Time_API/"
published: true
---

## Date and Time API의 패키지
```
java.time
java.time.chrono
java.time.format
java.time.temporal
java.time.zone
```

## java.time 패키지
날짜와 시각을 표시하는 코어 API를 제공한다.(ISO 8601의 표준 달력 시스템에 기초한)
Local time method
```
LocalDate(날짜만)
LocalTime(시각만)
LocalDateTime(날짜와 시각)
```
시차정보를 표시하는 Offset Time
```
OffsetTime(시각만)
OffsetTime(날짜와 시간)
```
지역정보까지 표시하는 ZonedDateTime
```
ZonedDateTime(지역정보를 포함)
```
월, 일의 개별정보
```
Year(년)
YearMonth(월)
MonthDay(월일)
```

now method
```
System.out.println(LocalDate.now()); // -> 2019-04-07
System.out.println(LocalTime.now()); // -> 12:10:30.888
System.out.println(LocalDateTime.now()); // -> 2019-04-07T12:10:30.888
```

문자열형식에서 LocalDate 인스턴스를 생성하기
LocalDate 클래스의 parse method 사용
```
LocalDate.parse("2016-04-01");
```

LocalDateTime 클래스의 isXxx method
```
boolean isAfter(ChronoLocalDateTime<?> other)
boolean isBefore(ChronoLocalDateTime<?> other)
boolean isEqual(ChoronoLocalDateTIme<?> other)
```

TimeZone을 얻기
java.time.ZoneId
```
System.out.println(ZoneId.systemDefault()); // -> Asia/Seoul
```

java.time.Duration과 java.time.Period 클래스
Duration : 시간의 간격
```
int getNano();
int getSeconds();
```
Perioid : 날짜의 간격
```
int getDays();
int getMonths();
int getYears();
```
## java.time.temporal 패키지
일시를 표현하는 클래스가 구현되어있는 패키지.

TemporalAccessor 인터페이스에 선언되어있는 method
```
default int get(temporalField field)
long getLong(TemporalField field)
boolean isSupported(TemporalField field)
default <R> R query(TemporalQuery<R> query)
default ValueRange range(TemporalField field)
```

Temporal 인터페이스에 선언되어있는 method
```
boolean isSupported(TemporalUnit unit)
default Temporal minus(long amountToSubtract, TemporalUnit unit)
default Temporal minus(TemporalAmount amount)
Temporal plus(long amountToAdd, TemporalUnit unit)
default Temporal plus(TemporalAmount amount)
long until(Temporal endExclusive, TemporalUnit unit)
default Temporal with(TemporalAdjuster adjuster)
Temporal with(TemporalField field, long newValue)
```

