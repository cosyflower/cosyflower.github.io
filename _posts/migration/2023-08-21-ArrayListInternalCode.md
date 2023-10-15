---
layout: single
title: "[23.08.21] Arrays.asList() 내부 코드"
categories:
    - beartoblog # category 일치했는지 확인하기 
tags:
    - 'Off The Record' # tag도 마찬가지로 같이 띄울 수 있다 
    - 'Arrays'
    - 'asList()'
toc: "true"
toc_sticky: "true"

date: 2023-08-21
last_modified_at: 2023-08-21
published: true # true로 변경하면 노출할 수 있음 

#toc: 목차 보이기 
#toc_sticky: 자동 스크롤 가능 
#date: 포스팅한 날자 
#last_modified_at: 마지막 수정 일자 

#bundle exec jekyll serve - test 하는 방법 
#published: true
#br : 개행하기 
#hr : 개행 줄이 같이 출력되는 상황 
---


# [Day 22 - 참고] Arrays.asList() 의 내부 코드 
#우테코  #4기 #3주차 #Collection #23.08.21

## 방어적 복사를 구현하려고 하던 중 
자판기 문제에서 CoinUnits() 라는 Util 성격을 지닌 정적 메서드를 정의하는 상황에서 고민이 생겼다 
기존에 아무런 생각없이 Arrays.asList() 메서드를 활용해서 여러 Coin Enum 인스턴스들을 그대로 넣어주기만 했는데, 이게 과연 올바른 방법일지 궁금했다 


[참고 사이트- tecoble](https://tecoble.techcourse.co.kr/post/2020-05-18-ArrayList-vs-Arrays.asList/)

## 사실 구현된 코드를 보면 ..? 
ArrayList<>() 의 생성자를 호출하는 상황이다. 
```java
@SafeVarargs
@SuppressWarnings("varargs")
public static <T> List<T> asList(T... a) {
    return new ArrayList<>(a);
}
```

그래서 머릿속에 문득 떠오른 생각은 new ArrayList<>() 로 List<> 를 구현하려고 할 때 Arrays.asList() 로 호출하면 결과적으로 같은 과정일까? 라는 생각이 들었다 

### 1. Return type
패키지가 서로 다르다
- Java.util.ArrayList
- Java.util.Arrays.ArrayList

### 2. 원소의 추가 그리고 삭제 
new ArrayList<>() 는 가능하지만, Arrays.asList()는 불가능하다 

-> Arrays.asList()는 해당 크기가 고정되어 있는 형태이다. 따라서 add/delete가 불가능하다
-> 다만, asList() 로 형성되어 있는 경우 내부 구성 인스턴스를 변경하는 것은 가능하다 
*Arrays.asList()*는 ***String[] str****(특정한 배열)를 백업할 때 주소값을 가져온다.

따라서* ***String[] str****가 변경되면* ***list****도 변경된다. (new ArrayList<>()를 사용하면 새로운 주소값를 할당)*
-> 원본의 영향을 그대로 받는다고 할 수 있겠다 ( 이는 Collections.unmodifiable 과 같은 구간이다 ) 

### 직접 눈으로 확인해보는 코드
```java
void checkList() {
    //given
    String[] names = new String[]{"Samsung", "Apple"};
    //when
    List<String> strings = Arrays.asList(names);
    List<String> unmodiList = Collections.unmodifiableList(strings);
    names[1] = new String("Openhimer");

    //then
    for (String name : strings) {
        System.out.println("name = " + name);
    }

    for (String s : unmodiList) {
        System.out.println("s = " + s);
    }
}
```

### Arrays.asList() 그리고 Collections.unmodifiable_Series()
-> asList() - 방어적 복사가 이뤄진다(구성 요소돌의 레퍼런스는 그대로 유지하되, List<> 의 레퍼런스는 새로운 값을 참조하는 형태가 되겠다). 대신 add/Delete가 불가능한 상황하다. 
==원본과의 연결 관계가 그대로 유지되는 상황이다== 

-> unmodifiable_Series() - 원본을 그대로 가리키는 상황, 다만 Wrapping 한다고 생각하자. 
==당연히, 원본과의 연결 관계가 그대로 유지되는 상황이다 (Read-only 하게 끔만 변경해준다고 생각하면 되겠다)==

-> new ArrayList<>() 인자로 전달되는 형태와 유사하다, 
==다만 이와 같은 상황에서는 원본과 연결 관계를 유지하지 않는 상황이다==
(원본과 연결 관계를 유지하지 않기 때문에 불변 객체를 만들 때, 특히 생성자 내에서 많이 사용한다고 생각할 수 있겠다)

### 사용법은?
생성자를 호출하거나 getter 관련 메서드 정의할 때는 무난하게 new ArrayList<>() 를 활용하는게 더 좋은 방법이다. 원본의 영향을 받지 않기 때문에 불변 객체의 특성을 그대로 유지할 수 있다는 특성을 지닌다

Arrays.asList - 테스트 코드 작성시, 불변하는 크기의 List를 형성해야 하는 상황이라면!


<br>
***
    
    진정한 경쟁력은 자신의 가치를 공유하는 것


[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}