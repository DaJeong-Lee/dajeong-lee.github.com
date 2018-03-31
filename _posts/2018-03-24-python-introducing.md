---
layout: post
title: Python 문법 (Java와 비교해서 다른점 위주로..)
date: 2018-03-23
description: Python 문법 (Java와 비교해서 다른점 위주로..)
tags:
---

# Python 문법 (Java와 비교해서 다른점 위주로..)

## 1. 튜플은 for에서 각각 k, v 따로 얻을 수 있음
<pre>
<code>
def test():
    data = {'key1': 'value1', 'key2': 'value2'}
    for k, v in data.items(): #dictionary를 튜플로 묶어서 리턴해줌
        print('key: {}, value: {}'.format(k, v))
</code>
</pre>

## 2. 여러 시퀀스 순회하기: zip()
##### zip(): 여러 시퀀스를 병렬로 순회(각 리스트별 순서대로 순회), 가장 짧은 시퀀스가 완료되면 멈춤.
<pre>
<code>
def test():
    days = ['Mon', 'Tues', 'Wednes']
    drinks = ['coffee', 'tea', 'beer']
    fruits = ['banana', 'orange', 'peach']

    for day, drink, fruit in zip(days, drinks, fruits):
        print('{}, {}, {}'.format(day, drink, fruit))
</code>
</pre>

## 3. 숫자 시퀀스 생성하기: range()
#### range(start, end, step)
<pre>
<code>
def test():
    for x in range(0, 5):
        print(x)

    nlist = []
    nlist = list(range(0,6))
    print(nlist)
</code>
</pre>

## 4. 컴프리헨션
### 컴프리헨션: 하나 이상의 이터레이터로부터 파이썬의 자료구조를 만드는 방법. 간단하게 반복문, 조건문 결합해서 자료구조 생성

#### 리스트 컴프리헨션: 대괄호[]안에 루프가 있음
##### [표현식 for 황목 in 순회가능객체]
##### if문, 이중 for문 가능
<pre>
<code>
def test():
    nlist = []
    nlist = [n*2 for n in range(1,6)]
    print(nlist)

# if 추가
def test2():
    alist = []
    alist = [n for n in range(1,6) if n%2 == 1]
    print(alist)

# 이중 for문
def test3():
    rows = range(1,4)
    cols = range(1,3)
    cells = [(r, c) for r in rows for c in cols]
    for cell in cells:
        print(cell)
</code>
</pre>

#### 딕셔너리 컴프리헨션: {}안에 루프가 있음
###### {키: 값 for 표현식 in 순회가능객체}
<pre>
<code>
def test():
    word = 'letters'
    count = {w: word.count(w) for w in word}
    print(count)
</code>
</pre>

## 5.함수
#### 기본 매개변수값 지정
<pre>
<code>
    # 기본 매개변수 설정
    def menu(wine, entree, dessert='pudding')
</code>
</pre>

#### 위치 인자 모으기: *
#### 키워드 인자 모으기: **
<pre>
<code>
def test(*args):
    print('argument tuple:{}'.format(args))

def test2(**kargs):
    print('argument tuple:{}'.format(kargs))

test('abc','123')
test2(a='abc', n='123')
</code>
</pre>

## 클로져
#### 클로저: 다른함수에 의해 동적으로 생성되고, 바깥함수로부터 생성된 값을 변경하고 저장할 수 있는 함수(함수를 리턴하는 함수).
<pre>
<code>
def knights(saying):
    def inner():
        return 'we are the kngihts who say {} saying'.format(saying)
    return inner

a = knights('Duck')
b = knights('Hasenpfeffer')
print(a())
print(b())
</code>
</pre>

## 익명함수: lambda
<pre>
<code>
def edit_story(words, func):
    for w in words:
        print(func(w))

stairs = ['thud', 'meow', 'thud', 'hiss']
result = edit_story(stairs, lambda w: w.capitalize()+'!')
</code>
</pre>

## 이름에 _와 __ 사용
#### _이름은 주로 한 모듈내에서 사용하는 이름에 붙인다
#### __이름__은 파이썬 내의 예약된 이름이다

## Array
<pre>
<code>
nums = range(1,5)
print(nums[2:4])
print(nums[2:]) #index 2부터 끝까지
print(nums[:4]) # 처음부터 index 4까지
print(nums[:-1]) # 마지막 1개를 빼고 다 가져옴 (-는 뒤에서부터 index)
</code>
### numpy: 배열을 다루는데 여러 기능이 있는 파이썬 패키지

</pre>

