---
layout: post
title: "WAY 32. 지연 속성에는 __getattr__, __getattribute__, setattr__을 사용하자"
date: 2018-10-17 13:08:31
tagline: "이펙티브 파이썬 코딩의 기술 책 스터디 정리"
categories:
- 이펙티브 파이썬 스터디
tags:
- python
image: /thumbnail-mobile.png
author: "Hyungcheol Noh"
permalink: /2018-10-17-effective-python-way32
---

## __getattr__ 메서드
- 파이썬이 동적 동작 기능 제공이 가능하게끔 하는 메서드
- 클래스에 `__getattr__` 메서드를 정의하면 객체의 인스턴스 딕셔너리에서 속성을 찾을 수 없을 때마다 이 메서드가 호출

```python
class LazyDB(object):
    def __init__(self):
        self.exists = 5
        
    def __getattr__(self, name):
        value = "Value for %s" % name
        setattr(self, name, value)
        return value
```

- 존재하지 않는 속성인 `foo`에 접근하는 경우:
    - 파이썬이 `__getattr__` 메서드를 호출 => 인스턴스 딕셔너리 `__dict__`를 변경
    
```python
data = LazyDB()
print("Before:", data.__dict__)
print("foo:", data.foo)
print("After:", data.__dict__)

>>>
Before: {"exists": 5}
foo: Value for foo
After: {"exists": 5, "foo": "Value for foo"}
```

- `__getattr__`이 실제 호출되는 시점을 보여주기 위하여 `LazyDB`에 로깅을 추가
    - 또한 무한 반복을 피하기 위하여 `super().__getattr__()`로 실제 프로퍼티 값을 얻어오는 부분을 추가

```python
class LoggingLazyDB(LazyDB):
    def __getattr__(self, name):
        print("Called __getattr__(%s)" % name)
        return super().__getattr__(name)

data = LoggingLazyDB()
print("exists:", data.exists)
print("foo:", data.foo)
print("foo:", data.foo)

>>>
exists: 5
Called __getattr__(foo)
foo: Value for foo
foo: Value for foo
```

- `exists` 속성은 원래 인스턴스 딕셔너리에 존재:
    - `__getattr__`이 절대 호출되지 않음
- `foo` 속성은 원래 인스턴스 딕셔너리에 존재하지 않음:
    - 처음에는 `__getattr__`이 호출
    - `foo`에 대응하는 `__getattr__` 호출은 `__setattr__`을 호출 => 인스턴스 딕셔너리에 `foo`를 저장
    - 따라서 두 번째로 접근하는 경우에는 `__getattr__`이 호출되지 않음

## 스키마리스 데이터
- 스키마리스 데이터(`schemaless data`): 구조가 정해지지 않은 데이터
- 스키마리스 데이터에 지연 접근하는 경우 위의 동작이 특히 도움이 됨
    - `__getattr__`이 프로퍼티 로딩이라는 어려운 작업을 한 번만 실행하면 다음 접근부터는 기존 결과를 가져옴

## __getattribute__ 메서드
- 데이터베이스 시스템에서의 트랜잭션
    - 사용자가 다음 번에 속성에 접근할 때는 대응하는 데이터베이스의 로우가 여전히 유효한지, 트랜잭션이 여전히 열려 있는지 알고 싶은 경우
    - `__getattr__` 후크는 기존 속성에 빠르게 접근하기 위하여 객체의 인스턴스 딕셔너리를 사용 => 이 작업에 믿고 쓸 수 없음
    - 파이썬에서 이러한 쓰임새를 고려하여 `__getattribute__`라는 또 다른 후크를 제공