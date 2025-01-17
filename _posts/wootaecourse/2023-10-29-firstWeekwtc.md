---
layout: single
title: "우아한테크코스 - 1주차 회고"
categories:
    - wootaecourse # category 일치했는지 확인하기 
tags:
    - ['1주차 과제 회고'] # tag도 마찬가지로 같이 띄울 수 있다 
toc: "true"
toc_sticky: "true"

date: 2023-10-29
last_modified_at: 2023-10-29
published: true # true로 변경하면 노출할 수 있음 

#toc: 목차 보이기 
#toc_sticky: 자동 스크롤 가능 
#date: 포스팅한 날자 
#last_modified_at: 마지막 수정 일자 
# [] 안에는 링크에 띄는 내용 ()안에는 링크 작성하기 [22.12.19 - 23.10.13](https://debonair-nigella-a88.notion.site/f71d32c1d1ef4cafbcd9fc77076b36a8?pvs=4)
#bundle exec jekyll serve - test 하는 방법 
#published: true
#br : 개행하기 
#hr : 개행 줄이 같이 출력되는 상황 

#<mark style='background-color: #f6f8fa'>우아한테크코스 프리코스가 드디어 시작했다!! 1주차 과제는 바로 숫자 야구 게임이였다</mark>
#<br>

# 이전에 김영한님 강의를 들었던 기억도 있었고 MVC 패턴을 검색하다가
# ```java
---
# 우아한테크코스 프리코스
> 1주차 과제를 마치고 난 이후 회고하며 정리한 글입니다 

## 분명 공부했었던 내용이었다
<mark style='background-color: #f6f8fa'>우아한테크코스 프리코스가 드디어 시작했다!! 1주차 과제는 바로 숫자 야구 게임이였다</mark>
<br>
우테코를 알게 되면서 자연스럽게 프리코스가 어떤 형태로 나오는지 궁금해서 서치를 하면서 자연스럽게 숫자 야구 게임도 스스로 연습해봤었다.
<br>구현하는 과정이 엄청 어렵지 않을거라 생각했지만, 아직도 많이 부족한 내 자신을 마주할 수 있었다 

## 항상 Controller에서 무너지는 나의 코드 
<mark style='background-color: #f6f8fa'>Model은 TDD 방향을 최대한 활용하려고 했다. 근데 Controller는 ??</mark>
<br>
Ball -> TripleBalls 기존의 모델에 포함될 기본 Ball 부터 일급 컬렉션 TripleBalls 까지는 테스트 코드를 활용해서 원만하게 해결이 가능했다.
<br>문제는 Model을 다 만들고 난 이후 Controller에서 어떤 흐름으로 작성해야 할지 감이 잘 오지 못했다. 마치 요리 재료는 다 준비했는데, 요리 할 줄 모른달까??
<br>README에서 기능 명세 사항을 읽은 다음 어느정도 Model에 포함된 클래스 유형 그리고 필드를 구분할 수 있었지만 나 자신이 어느 순간 Controller의 흐름에 정확하게 분석하지 않았지 않나라는 반성을 했다.
<br><br>막상 전체를 가지고 흐름을 스스로 제어할 줄 알아야 했는데 그러지를 못했다. 
<br>Controller 구간을 작성하면서 자연스럽게 테스트 작성 - 성공 - 리팩토링의 과정도 무너지기 시작했다. 너무 처절하게 무너지는 코드들을 보며 멘붕까지 오는 과정은 그리 오래 걸리지도 않았다 

## 막상 Controller를 구현했다고 치자! 테스트 코드를 어떻게 작성할건지?
<mark style='background-color: #f6f8fa'>각각의 역할이 존재하는 Controller의 테스트 코드는 어떻게 작성해야 할까</mark>
<br>어찌어찌 해서 Controller를 구성했고 클린 코드를 유지하지는 못했지만 돌아가는 쓰레기 프로그램을 만들었다고 가정하자.
막상 구현한 Controller를 구현하고 테스트 하려니 다시 머리가 복잡해졌다. 결국 해당 Controller가 View를 통해 입력 혹은 출력을 받아 Model 내 클래스의 객체를 형성하는 과정을 테스트하려고 하는데, 도통 감이 오지 않았다

특히 미리 정보가 들어가야 확인이 가능한 Controller는 더욱이 어떻게 해야 할 지를 몰랐었다 
입력을 담당하는 역할이라면 readLine()을 활용해서 asserThat().isEqualTo()로 비교라도 가능할 텐데, 입력하지 않고 기존의 정보를 활용해서 출력을 하는 과정에서 기존의 정보를 해당 Controller 테스트 코드에 어떻게 주입할 지 감이 오지 않았다. 구현할 수 없었다 

## 테스트 코드를 통해 확인한 메서드를 중복해서 테스트하려 하지 말자 
<mark style='background-color: #f6f8fa'>이미 테스트 하셨잖아요?</mark>
<br>
전체적인 설계 flow를 제대로 정리하지 않은 상태에서 테스트 코드를 작성하려고 하니 기존에 테스트 했던 코드 혹은 구간들을 또 다시 테스트 하려는 경향도 많았다. 
개인적으로 테스트를 진행한 메서드를 구현하는 동안이라도 주석을 이용해서 표기하는 습관을 가져보자는 생각도 들었다 

## V2 버전을 만들어보자 - MVC Adapter를 활용해보자 
<mark style='background-color: #f6f8fa'>Controller를 어떤 flow로 진행해야 할지를 고민하면서 접근한 MVC Adapter 패턴이였다</mark>
<br>
이전에 김영한님 강의를 들었던 기억도 있었고 MVC 패턴을 검색하다가 Adpater 패턴을 생각했다. 그림을 그리면서 이해하려 했다 

내가 생각한 전체적인 구조는 다음과 같다 
1. 먼저 기능 명세 사항 그리고 출력 결과를 확인해서 기능들을 분류한다 (InputBallsController)..
    - 출력 결과를 하면서 구획화를 하려 했다. 
    - 특정 Controller는 OutputView, InputView를 필드로 유지하는 것으로 구현했다
    - 입력을 받기 위해 출력해야 하는 문장도 존재하고, 출력한 이후에는 String 문자열을 입력 받는 방향
    - InputView에서 입력받은 문자열은 Controller에서 받고, 원하는 객체로 변환해서 저장하는 것으로 생각했다 


2. 각각의 Controller를 형성했다면 mainApplication에 Controller들을 모두 put() 하자
    - Map 자료구조를 활용해서 String을 Key로 잡은 다음 Controller을 put() 하는 방향으로 구현
    - 원하는 Controller를 조회하기 위해서 Map을 적용했다.
    - 기능을 호출하게 되면 Controller를 호출하고 담당한 역할을 수행하게 된다 

### 테스트를 위한 Custom IOTest 구현

```java
private final ByteArrayOutputStream captor = new ByteArrayOutputStream();

@BeforeEach
void init() {
    System.setOut(new PrintStream(captor));
}

@AfterEach
void printOutput() {
    System.setOut(System.out);
    System.out.println(output());
    captor.reset();
	Console.readLine(); // Scanner 사용이 끝나면 close() 해야 테스트 코드 실행 시에도 문제가 생기지 않는다! 
}
```

<br>
이런 구조를 생각하게 된 결정적 이유는 Controller의 flow를 좀 더 명확하게 전달하고 싶었고, 나 역시 명확하게 인지한 상태에서 코드를 작성하고 싶었다 
OutputView, InputView로 명확하게 역할을 구분해서 작성하다 보니 flow가 눈에 확 들어와서 가독성이 높아진 모습을 확인할 수 있다
<br>

**물론 반복되는 코드는 많았지만**<br>
V1 버전의 구현을 진행하면서 Controller의 역할을 좀 더 명확하게 인지하고 싶었던 나의 니즈를 충족할 수 있었다.

<br>

## 코드리뷰로 확인한 보완해야 할 점들

<mark style='background-color: #f6f8fa'>+보단 -를 메꾸는 것이 더 중요하다</mark><br>

- README : Controller flow 작성하기 + Skeleton code 작성하려 할 때 Class 위주로 더 명확하게 구분하고, 기능 더 세분화하는 작업하기
- Objects 패키지가 제공하는 메서드 적용하기 ex) .isNull(), equals()
- Exception 메세지 관련해서 Enum 클래스를 활용하는 연습
- Coding Convention은 지속적으로 지키기


## 1주차 숫자 야구 게임 구현을 마무리하며
<mark style='background-color: #f6f8fa'>Controller에 대해서 더 생각해보자</mark>
TDD를 바탕으로 테스트를 작성하면서 Model 클래스를 어떻게 구현해 나갈지는 Good! 
<br>하지만 막상 Contoller에서 흐름을 제어하지 못하면서 자연스럽게 멘붕이 왔다… 리팩토링 하기 전에 프로그램의 전체적인 구현에서 막힌 상황이였다 
2주차로 넘어가기 전에 공통 템플릿을 만들고 싶었다. 내가 가져가면 좋은 코드들? 그런걸 미리 정리하면
구현할 때 덜 혼란스럽지 않을까 하는 생각이 들었다 

<br>
***
    
    진정한 경쟁력은 자신의 가치를 공유하는 것


[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}






