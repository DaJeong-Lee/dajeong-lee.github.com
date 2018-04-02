---
layout: post
title: Java Annotation이란
date: 2018-03-23
description: Java annotation에 대해 알아보기
img: java-annotation.png
tags:
---

## Java annotation 설명

Java에서 **@어노테이션은** **코드 메타테이터**로 사용됨
> 메타데이터 저장을 위해 속성(멤버)를 가질 수 있음

**@어노테이션**  컴파일러에게 어노테이션명 을 알려줌

**@어노테이션**은 **속성**을 가질 수 있음
> @Entity(tableName = "vehicles", primaryKey = "id")

**@어노테이션**은 **클래스, 인터페이스, 메소드, 메소드 파라미터, 필드, 지역변수** 위에 위치 할 수 있음

## Annotation 예제
> **@Override**는 오버라이딩 메소드 위에 위치하여 이 메소드가 오버라이딩된 메소드라고 표시
>
> 굳이 @Override를 안붙여도 되지만 붙이는 이유는 나중에 부모클래스의 메소드명이 변경되었을 때
>
> @Override를 안 쓴 오버라이딩함수는 해당 클래스의 멤버메소드로 인식이되어버리는 문제가 발생함.
>
> 문제가 발생했는데도 에러를 안날려주니까 모를 수 있음

## 사용자 정의 어노테이션 만들기
### java 파일 3개 생성
* MyAnnotation.java: 사용자 어노테이션 인터페이스
<pre>
<code>
package test;

/**
 * Created by ldj on 2018. 3. 23..
 */

import java.lang.annotation.Documented;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;

@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface MyAnnotation {
    String value();
    String name();
    int age();
    String[] newNames();
}

</code>
</pre>


* MyClass.java: MyAnnotation을 사용한 Class
<pre>
<code>
package test;

/**
 * Created by ldj on 2018. 3. 23..
 */
@MyAnnotation( value="123", name="Jakob", age=37, newNames={"Jenkov", "Peterson"} )
public class MyClass {
    public void printResult(){
        System.out.println("MyClass 실행됨");
    }
}
</code>
</pre>

* Main.java: 코드를 실행할 Main Class
<pre>
<code>
package test;

import java.lang.annotation.Annotation;

/**
 * Created by ldj on 2018. 3. 23..
 */
public class Main {
    public static void main(String[] args) {
        System.out.println("run main function");

        Class aClass = MyClass.class;
        Annotation annotation = aClass.getAnnotation(MyAnnotation.class);
        if(annotation instanceof MyAnnotation){ MyAnnotation myAnnotation = (MyAnnotation) annotation;
        System.out.println("MyClass에서 정의한 MyAnnotation 속성");
        System.out.println("name: " + myAnnotation.name()); System.out.println("value: " + myAnnotation.value()); }
    }
}
</code>
</pre>


## Reference
<http://hamait.tistory.com/314?category=79137>

<http://hamait.tistory.com/317?category=79137>










