---
layout: single
title: "우아한테크코스 - 2주차 회고"
categories:
    - wootaecourse # category 일치했는지 확인하기 
tags:
    - ['2주차 과제 회고'] # tag도 마찬가지로 같이 띄울 수 있다 
toc: "true"
toc_sticky: "true"

date: 2023-10-28
last_modified_at: 2023-10-28
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
> 2주차 과제를 마치고 난 이후 회고하며 정리한 글입니다 

## 1주차 V2 과정을 적용했다??!
<mark style='background-color: #f6f8fa'>1주차 리뷰 때 좋은 평가를 받은 V2 코드의 구조를 활용했다</mark>
<br>
1주차 미션을 마무리 짓고 들었던 생각은 내가 필수적으로 들고 가야하는 구조를 정리해두자! 라는 생각이 강했다

~~사실 지금 생각해보면 학습하려고 하는게 아니라 코테를 준비하는 사람인 것 마냥 행동했다~~

숫자 야구 게임을 진행하면서 "이건 계속해서 유지하고 있으면서 더 발전할 수 있는 코드다!" 하는 애들을 그대로 가져가는 방향을 선택했다
<br>예로 view의 출력 내용 그리고 input을 실제로 검증하기 위한 IOTest를 계속 가지고 가려고 했다 
<br>또한 V2 MVC 패턴을 활용하면서 인터페이스(추상화)를 활용해서 확장성 높은 코드를 만들었고 한 눈에 잘 들어온다라는 리뷰가
<br>나를 행복하게 만들었던 기억이 있어 다시 한번 적용해보자는 생각이 들었다.

~~이 역시 나의 생각과 틀을 부시려는 계기 중 하나가 되었다!~~

### 2주차 미션을 들어가기 전 
이번 주차 미션에서 내가 필수로 해야하는 것들을 리스트로 작성했다

- [ ] 이메일 내용 철저히 확인하기 (구현 전 미리 파악한다)
    - [ ] 1주차 공통 피드백 확인하기 
- [ ] Controller, Model, View 관련 인터페이스 및 로직들을 가지고 가기 (구현)
- [ ] TDD 반영하는 연습 진행하기 (구현)
- [ ] IOTest 계속해서 연습하기 (구현)
- [ ] Technical Writing VS 내가 보완할 점 정리해서 블로그 관리하기 (블로그)
- [ ] README.md 파일을 어떻게 하면 더 명확하게 작성할 수 있을지도 고민해보기 (구현) 
- [ ] GIT revert, rebase, reset 관련해서 더 파헤쳐보기 (GIT 활용법)


#### 이메일 내용 with 1주차 공통 피드백
<hr>
<mark style='background-color: #f6f8fa'>이메일 워딩 그대로 가지고 작성했다</mark>
<br>
다음은 메일로 온 내용들, 워딩들을 직접 가지고 왔다 

- 앞으로 미션을 진행하면서 어려운 부분이 있다면 테코톡을 통해 학습하고 구현하면 좋겠어요.
- 요구사항을 이해하는 게 어려울 수 있지만 주어진 요구사항을 잘 파악하는 것도 좋은 개발자의 역량 중 하나라고 생각합니다. 
- 고민 없이 무작정 질문하거나 다른 사람의 도움을 받기 전에 스스로 고민하고 문제를 해결해 보는 것을 추천합니다
- <mark style='background-color: #f6f8fa'>함수를 분리하고, 각 함수별로 테스트를 작성하는 것에 익숙해지는 것을 목표로 하고 있어요></mark>

과제 제출 관련 유의사항

- 이번 주 차 목표를 중심으로 학습하면서 느낀 점을 소감문으로 작성해 주세요
- 학습한 '과정’을 잘 드러내 주세요.

우테코는 원합니다

- 고통에 좌절하지 말고 고통을 즐기면서 더 성장하는 여러분이 되기를 기대합니다

<br>
1주차 공통 피드백을 간략하게 정리하자면

1. 요구사항을 정확히 준수한다
2. 커밋 메세지 의미있게 작성한다
3. git을 통해서 관리할 자원을 고민한다
4. PR 하기 전 브랜치 확인하기
5. PR 작성했다면 닫지 말고 추가 커밋하기
6. 네이밍 신경쓰기, 축약하지 말기
7. 공백 라인도 의미가 존재한다, 공백 컨벤션 지키기
8. 의미없는 주석 달지 말기 
9. 최대한 JAVA API를 활용하기 
10. Collection 활용하기 

다행히도 1주차 공통 피드백 사항을 확인하면서 컨벤션에 맞추려 한 모습, 공백 라인도 철저하게 의미를 부여하려 했던 모습
<br> Collection을 활용하는 것도 잘 지켰지만 의미없는 주석 달지 말기와 Objects 관련 메서드를 활용하지 못했던 모습
<br> 이러한 부분들은 내가 더 신경써야 한다는 것도 느낄 수 있었다 

## 미션을 수행하며 (Controller, Model, View의 인터페이스 활용)
최대한 생생하게(?) 작성하기 위해서 코드를 구현하면서 생긴 고민은 바로바로 작성할 수 있도록 베어에 정리해두었다

1. Constructor에 변동이 생긴 상황
- 테스트 코드를 작성할 때 Car의 인자 구성에 변동이 생긴 상황
- 테스트 할 때는 distance 까지 모두 배정하는 방식이 진행하기 수월하다 
- Car 객체를 형성할 때 기본적으로 distance가 0 인 생성자도 필요한데?!

<br>

Car의 생성자를 2개로 둬도 되나? 라는 생각을 하게 되었다 
```java
public static final int DISTANCE_INIT_VALUE = 0;
private final String carName;
private int distance;

public Car(String carName) {
    validateName(carName);
    this.carName = carName;
    this.distance = DISTANCE_INIT_VALUE;
}

public Car(String carName, int mockedDistance) {
    this.carName = carName;
    this.distance = mockedDistance;
}
```

2. Random 수의 주입은 어떤 방식으로 진행해야 될 까??
1번 고민과도 연관된 2번쨰 고민이다. 생성자를 2개로 구분해서 현재 있는 위치를 직접 지정할 수 있게 되었다
<br>위치를 직접 지정하고 Random 수는 클래스 내 static 클래스를 또 지정해서 내가 랜덤 수를 지정할 수 있도록 구성했다 

```java
private static class MockedGenerator {
    private int generateMockedNumber(int mockedNumber) {
        return mockedNumber;
    }
}
// mockedNumber는 Car의 move() 인자로 전달되는 방향으로 설정했다 
```
(회고하면서 작성하는 글) 굳이 이 nested static class가 필요했을까??
나의 의도 - 랜덤 수 대신 내가 지정한 수를 인자로 전달하고 싶었던 상황 
인자에 전달될 수를 지정하고 싶었던 거라면, 테스트 코드를 작성하는 구간에서 그냥 인자를 전달하면 되는거 아니였나?? 
실제로 코드를 보니 사용하지 않았다.... 할 말이 없다;

3. REAME를 진행 방향에 대해서 (Controller flow에 대해서)
특히 Controller 구간 생각할 때 Flow에 따라 좀 더 명확하고 세세하게 작성하는 방향으로 작성하면 좋겠다 라는 생각이 들었다
1주차 미션의 경우에도 모델 관련 구현까지는 문제가 없었다가 Controller 구간에서 확 죽는 경향이 있었다 
Controller 구간은 model 관련 구현이 어느정도 진행된 이후에 더 구체화하는 것이 좋겠다! 어떤 흐름으로 진행되는지를 명시만 해줘도 코드를 구현하는 과정에 있어서 한결 수월해진 것을 느낄 수 있었다 

4. Validate 위치에 대해서
1주차 과제를 했을 때도 정말 많은 고민을 했던 부분 중 하나이다. 검증을 단순히 View or Model의 생성 과정 중 한 구간에서만 검증을 진행할 것인지, 따로따로 검증 구간을 만들어서 검증할 지를 고민했다. 

나의 선택은 Domain 그리고 InputView 각각 검증하는 방향으로 진행하는 것이었다 
- 뷰에서 검증하는 것은 isNullOrEmpty
- 정규표현식에 맞지 않는 문자열이 입력된 경우로 생각했고

도메인의 경우
- 이름이 5글자 이하여야 한다
- 이름 중복이 존재해서는 안 된다(내가 추가적으로 생각한 예외 상황) 
<br>항상 올바른 데이터가 넘어온다는 100프로의 확신도 없었고, 한 쪽에만 책임을 부여한다고 명확한 검증이 이뤄진다고 생각하지 않았다.
그래서 그 책임을 분배하기로 결정했다 

5. IOTest가 필요한 시점 - Controller flow를 작성한 이후에 진행하기 
모델 관련 구현이 어느정도 진행이 되었고 Controller flow를 미리 작성한 다음 IOTest를 만드는게 좋다고 생각했다
<br>나의 의도는 View에 올바른 내용이 출력되는지와 원하는 값이 readLine() 했을 때 원하는 객체의 데이터로 변환이 되는지였다 


6. private 메서드는 어떻게 테스트 할지
생각보다 이 고민의 해결 방안은 간단했다. 
private 메서드를 테스트 하려 하지 말고 public으로 선언한 메서드로 테스트가 가능하게끔 구성하자! 라는 생각을 했다 

**또한!! test code를 위해서 production code를 추가해서는 안 된다는 엄청난 깨달음을 얻었다**


## 첫 번째 구현을 마치고  
<mark style='background-color: #f6f8fa'></mark>
<br>

```markdown
racingcar                                 
├─ controller                             
│  ├─ AbstractController.java             
│  ├─ Controller.java                     
│  ├─ DisplayRoundController.java         
│  ├─ RacingResultController.java         
│  ├─ RegisterCarNamesController.java     
│  └─ RegisterRoundController.java        
├─ exception                              
│  └─ ErrorException.java                 
├─ model                                  
│  ├─ Car.java                            
│  ├─ RacingCars.java                     
│  └─ Round.java                          
├─ system                                 
│  ├─ converter                           
│  │  ├─ StringToCarList.java             
│  │  └─ StringToRound.java               
│  └─ RacingCarApplication.java           
├─ view                                   
│  ├─ inputview                           
│  │  ├─ InputView.java                   
│  │  ├─ RegisterCarNamesInputView.java   
│  │  └─ RegisterRoundInputView.java      
│  └─ outputview                          
│     ├─ DisplayRoundOutputView.java      
│     ├─ ErrorOutputView.java             
│     ├─ OutputView.java                  
│     ├─ RacingResultOutputView.java      
│     ├─ RegisterCarNamesOutputView.java  
│     └─ RegisterRoundOutputView.java     
└─ Application.java                       
```

이전 숫자 야구게임에서 활용한 구조를 그대로 가지고 와봤다. Controller, View 를 인터페이스 형태로 구성했다
<br> Controller는 View에게 모델 관련 데이터를 주기도 하고, View로 부터 전달받은 데이터를 모델로 변환해서 저장하기도 한다 
<br> View는 출력하기도 원하고 콘솔로부터 데이터를 입력받기도 한다

**이번 2주차 미션을 처음 진행하는 동안에는 Controller Test, 그리고 Validation을 어떻게 반영할지가 과제를 진행하는데 앞서 나의 큰 고민거리였다**

- 이전 1주차 회고에서 언급했던 Controller를 어떻게 테스트 해야 하는지
- Validate 검증의 과정을 Model에 국한 할 것인지 InputView에서도 검증 과정을 분배하여 구현할 것인지 
- Controller를 어떻게 테스트 할 지 고민해봤다 

<br> 테스트 코드를 통해서 검증하는 것은 두려운 것을 편안하게 만들어준다고 생각했기에 꼭 접목하고 싶었다 
<br> 특히 모델 구간을 TDD 방식으로 구현하고 확인하면서 자연스럽게 코드에 신뢰가 갔다는 점, 다시 돌아볼 필요 없이 내가 원하는 메서드를
호출하는 것은 엄청난 장점이라고 생각했다 
```

### 나의 코드를 다시 읽어보았다
<mark style='background-color: #f6f8fa'>Map을 굳이 사용해야 하는 이유와 과설계</mark>
<br>

Controller의 코드를 확인해보자
<br>

```java
@Override
    void doProcess(Map<String, Object> model) {
        outputView.print(model);
        String input = (String) inputView.input(model);
        RacingCars racingCars = new RacingCars(StringToCarList.convert(input));

        model.put(RACING_CARS_KEY, racingCars);
}
```

1. OutputView 에서는 문장을 출력하고
2. InputView에서는 Console로 부터 읽은 문자열을 반환한다
3. Controller 에서는 모델 생성자를 활용해서 원하는 객체를 형성한다 
4. model(타입이 Map<String, Object>)에 String 키 그리고 형성한 객체를 넣는다 

<br>
<u>이 코드를 보고 "너무 깡패같은 코드를 만들었구나" 라는 생각을 단번에 할 수 있었다</u>
<br> Value에 Object를 넣는 Map<> 을 형성했다는 것은 어떠한 형태의 모든 값들을 넣을 수 있다는 것이다. 
<br> 지금과 같은 작은 프로그램에서는 적용할 수 있겠지만 확장성을 고려한다면 이는 결코 옳지 못한 방식이다 
<br> <u>모든 값을 Object 라는 부모 타입으로 받게만 한다면 사실 고수준, 저수준의 구현이 애초에 존재하지 않았을 뿐더러</u>
<br> <u>이후 나의 코드에도 나와 있듯, 강제 형 변환을 해야만 해당 데이터를 올바르게 인식할 수 있다</u>
<br> 그리고 강제 형변환은 좋은 방식도 아니다! 

추가로 Application 내부에서 Controller들을 Map<>에 넣고, 매번 조회하는 방식으로 진행되고 있는데, 반복되는 코드가 발생하다 보니
이 부분을 어떻게 고칠 수 있을까 라는 생각이 들었다. 
Map<>에 넣고 호출하기만 하면 되는 부분이기도 했는데, 굳이 Map<>을 활용하지 않고 new ...Controller() 하면 되지 않나? 라는 생각도 들었다 


#### 자연스럽게 DTO로.. 또 다른 고민
<mark style='background-color: #f6f8fa'>Model 내 DTO 그리고 VO에 대해서</mark>
<br>
1주차 미션을 진행하고 나서 오픈 커뮤니티 내용을 확인하던 중 DTO VO 관련 내용을 확인할 수 있었다
<br> 레이어간 교환해야 할 데이터를 Data Transfer Object, DTO를 활용한다는 내용을 보면서 어쩌면 Map<String, Object> model에
그동안 지속적으로 넣어준 값들이 DTO 라는 생각이 들었다. Controller에서 View 를 통해 받은 데이터를 변환 혹은 인자로 활용하여 원하는 객체로 형성하고
이 데이터들을 추후에 다른 Controller 에서도 사용되기에 DTO를 사용해야 하지 않을까 하는 생각이 들었다 

<br> 이 부분도 분명 이전에 공부하면서 자연스럽게 접했던 개념이었는데 그렇게 크게(?) 신경을 쓰지 않은 구간이었다.
<br> 개념이 미숙해서 먼저 테코블에서 정리된 내용을 확인했다 

#### 테코블에서 정리한 DTO를 참고해보자
<mark style='background-color: #f6f8fa'>Model 내 DTO 그리고 다시 제자리로</mark>
<hr>
<img width="693" alt="image" src="https://github.com/cosyflower/MyStrategy/assets/128453459/a1f4f08c-37ee-4cd6-b2fa-8c7e8b90e5bd">

[참고- 테코블(DTO의 사용 범위에 대해서)](https://tecoble.techcourse.co.kr/post/2021-04-25-dto-layer-scope/)

<img width="725" alt="image" src="https://github.com/cosyflower/MyStrategy/assets/128453459/19e02424-fa4e-46d3-bb71-3cd2358050bc">

[DTO를 활용하면 얻을 수 있는 이점]
- Model 그리고 View가 강하게 결합되는 것을 방지할 수 있다
- 도메인 모델은 캡슐화, UI 화면에서만 사용하는 데이터를 선택적으로 전달할 수 있음

도메인 정보를 위부로 노출시키지 않기 위함이라고 생각할 수 있다 
<br> 참고 사이트에서 DTO의 범위, Entity로의 변환에 대해서도 언급되고 있다. DTO의 변환 과정이 Service, Controller 까지 확대되도 되는지에 관한
내용도 있는 것을 확인할 수 있는데, 일단 지금은 DTO를 왜 활용하는가에 대해서만 간략하게 알고 구현으로 넘어가려고 했다
<br> 사실 MVC 패턴이 적용되는 Presentational Layer 이외의 Repository, Service 단까지는 구체적으로 생각해본적이 없기도 했고
<br> 이번 2주차 미션인 자동차 경주 게임에서도 Repo, serivce 단까지 고민한 적이 없을 뿐더라
<br> 미션의 방향에 집중하는 모습보다 계속해서 다른 방향으로 튀어나가려는 모습?? 내가 지금 과설계를 하고 있나?? 라는 공포가 갑자기 엄습했다
<br> 여태까지 내용이 부실하다고만 생각해서 무언가를 만들어나가려고 했다면 오히려 지금은 과하게 설계를 하고 있는지를 의심하게 되었다 

제대로 인지를 제대로 못한 상황인데 DTO, VO를 고민하는게 과연 이 시점이 올바를까 라는 생각도 들었다 

---

## V2 시작
<mark style='background-color: #f6f8fa'>완벽한 구현 << 이번 주차 미션의 목적을 지키려고 노력하자</mark>
<br>
위에서 언급한 "메일에서 확인한 내용을 꼼꼼히 읽어달라는 말"
<br> 이메일에서 언급한 내용을 다시 가지고 와봤다 

- 앞으로 미션을 진행하면서 어려운 부분이 있다면 테코톡을 통해 학습하고 구현하면 좋겠어요.
- 요구사항을 이해하는 게 어려울 수 있지만 주어진 요구사항을 잘 파악하는 것도 좋은 개발자의 역량 중 하나라고 생각합니다. 
- 고민 없이 무작정 질문하거나 다른 사람의 도움을 받기 전에 스스로 고민하고 문제를 해결해 보는 것을 추천합니다
- 함수를 분리하고, 각 함수별로 테스트를 작성하는 것에 익숙해지는 것을 목표로 하고 있어요

[과제 제출 관련 유의사항]
- 이번 주 차 목표를 중심으로 학습하면서 느낀 점을 소감문으로 작성해 주세요
- 학습한 '과정’을 잘 드러내 주세요.

[우테코는 원합니다]
- 고통에 좌절하지 말고 고통을 즐기면서 더 성장하는 여러분이 되기를 기대합니다

<br>
미션을 진행하면서 내가 제대로 지키지 못한 부분이 눈에 선명하게 들어왔다
"함수를 분리하고, 각 함수별로 테스트를 작성하세요"

- <mark style='background-color: #f6f8fa'>함수를 분리해야 한다는 것</mark>
- <mark style='background-color: #f6f8fa'>함수별로 테스트를 작성하라는 것 </mark>
<br>
함수를 분리하라는 것과 함수별로 테스트를 작성하라
<br>
추가적으로 메일에 온 내용 중 다음의 내용이 추가되어 있다
<br>
"세 개의 요구사항을 만족하기 위해 노력한다. 특히 기능을 구현하기 전에 기능 목록을 만들고, 기능 단위로 commit하는 방식으로 진행한다."

- <mark style='background-color: #f6f8fa'>기능을 구현하기 전에 기능 목록을 만들어라</mark>
- <mark style='background-color: #f6f8fa'>기능 단위로 커밋 하라</mark>

위의 사항을 지키기 위해서 미션으로 제공된 기능을 확인하자

```markdown
- 주어진 횟수 동안 n대의 자동차는 전진 또는 멈출 수 있다.
- 각 자동차에 이름을 부여할 수 있다. 전진하는 자동차를 출력할 때 자동차 이름을 같이 출력한다.
- 자동차 이름은 쉼표(,)를 기준으로 구분하며 이름은 5자 이하만 가능하다.
- 사용자는 몇 번의 이동을 할 것인지를 입력할 수 있어야 한다.
- 전진하는 조건은 0에서 9 사이에서 무작위 값을 구한 후 무작위 값이 4 이상일 경우이다.
- 자동차 경주 게임을 완료한 후 누가 우승했는지를 알려준다. 우승자는 한 명 이상일 수 있다.
- 우승자가 여러 명일 경우 쉼표(,)를 이용하여 구분한다.
- 사용자가 잘못된 값을 입력할 경우 IllegalArgumentException을 발생시킨 후 애플리케이션은 종료되어야 한다.
```

쎄한 느낌에, 내가 먼저 구현한 커밋을 확인했다
<br> 분명 나도 기능을 구현하기 전 기능 목록을 만들긴 했지만 기능 단위로 Commit이 올바르게 되었는지 확인해야 했다

<img width="919" alt="image" src="https://github.com/cosyflower/MyStrategy/assets/128453459/8b06acec-e219-482b-adbf-a340921144fe">

~~부끄러움은 내 몫이다~~

<mark style='background-color: #f6f8fa'>기능 단위로 커밋을 한 것도 있고, 없는 것도 있고 뒤죽박죽 섞인 모양을 확인할 수 있었다</mark>
<br> 작은 단위의 프로그램, 그리고 거기에 적용되어 있는 지켜달라는 약속도 제대로 지키지 못하는데 DTO VO를 따질 수 있는 자격이 되는지를 나에게 스스로 질문했다.
<br> 기본을 제대로 잡지 못한 상황에서 이런 식의 발전 방향은 우테코에서 원하는 방향과는 다른 방향이라는 생각이 들었다 

<br> 올바르지 못한 구현이다

제대로 구현하지 못했다는 생각이 들었고 이번에도 코드를 싸-악 갈아 엎었다 


## V2 구현하기 전 기능 목록을 올바르게 작성하자 (READEM.md)
<mark style='background-color: #f6f8fa'>기능 목록부터 올바르게 다시 작성해보자</mark>
<br>

Skeleton Code 그리고 Controller flow를 작성했다. 기능 명세 사항을 읽으면서 Class에 대한 간략적인 구성을 생각하고 정리해둔다
<br> 
마지막으로 Controller flow 에서는 출력 예시 결과를 확인하면서 어떤 방식으로 Controller를 구현할 지 구성했다 

## V2 기능 목록 부터!! 그리고 유의 사항
<mark style='background-color: #f6f8fa'>기능 목록부터 올바르게 다시 작성해보자</mark>
<br>
- 함수를 분리하고, 테스트하자
- 기능 목록을 작성하고, 기능 단위로 커밋을 작성하자 
<br>

함수를 분리하는 것까지는 감이 왔다. 객체지향적으로 코드를 작성해야 하는 것으로 인지했다
**함수를 테스트 해야한다**

### 함수를 테스트 해야 한다라는 말은
<mark style='background-color: #f6f8fa'>테스트 가능한 코드로 작성하라는 말과 같다</mark>
<br>

테스트 한다라는 말은 결과적으로 테스트를 가능한 코드로 작성하라는 말과 같다는 표현이었다
<br>
1주차 미션을 진행하면서 controller test를 어떻게 진행해야 할지 정말 많이 고민했는데 이유가 테스트하기 힘들게 작성하지 않았나라는 생각이 들었다
콘솔로부터 입력을 받고, 입력을 통해 원하는 객체가 올바르게 형성되었는지를 확인하는 테스트 코드는 원활했지만 테스트 하기 이전에 특정한 정보가 존재해야 하는 상황인 경우에는 어떻게 Map<> model에 정보를 넣을지 고민이었다 

<br>
테스트 할 수 있는 코드를 만들자
<br>
<mark style='background-color: #f6f8fa'>테스트 하기 위해선 메서드, 인자, 메서드에서 최종적으로 반환하는 값이 존재해야 한다.</mark>
<br>
상황에 맞게 인자를 구성하고, 구성한 인자를 테스트 대상인 메서드에 전달하고, 메서드에서 반환한 결과가 내가 생각한 결과와 동일한 지 확인해야 했다.

```java
public class RegisterCarNamesController extends AbstractController {
    public static final String RACING_CARS_KEY = "racingCars";
    private final OutputView outputView;
    private final InputView inputView;

    public RegisterCarNamesController(final OutputView outputView, final InputView inputView) {
        this.outputView = outputView;
        this.inputView = inputView;
    }

    @Override
    void doProcess(Map<String, Object> model) {
        outputView.print(model);

        String input = (String) inputView.input(model);
        RacingCars racingCars = new RacingCars(StringToCarList.convert(input));

        model.put(RACING_CARS_KEY, racingCars);
    }
}
```

당장 내가 작성한 Controller 에서 확인 가능한 메서드는 doProcess() 이다. 여기서 중요한 건 반환 타입이 void라 어떤 타입의 객체를 형성하는지 확인이 불가능하다. 

- 확인이 불가능한 상태에서 테스트를 작성하려고 하다보니 내부의 기능을 확인하게 되었고
- 내부의 기능은 외부에 노출되지 않아야 하기 때문에 private 메서드를 사용할 수 밖에 없었고
- Private 메서드를 테스트 하려다 보니 접근제한자를 고민하게 되는 연쇄적인 문제가 발생했던 것이다 

**테스트 코드를 위해서 프로덕션 코드 범위까지 건드리는건 이상하다!**

지금 간단한 프로그램의 기능 명세 사항을 구분해도 많이 등장하는데,, 실무에서 직접 마주보게 되면 중간 중간 테스트 코드의 양도 늘어날 것이 분명하다. 테스트 하기 위해서 프로덕션에서 사용하지 않는 코드를 구현한다면 점점 코드가 스파게티처럼 되지 않을까 하는 생각을 했다
<br>
ex) 생성자 오버로딩을 활용한 경우가 대표적인 예시라고 할 수 있겠다 

첨언하자면, 테스트를 진행할 때는 애매한 상황, 경계에 놓인 값들을 위주로 작성하는 것은 기본이다.
기본기를 잃지 말자 


### MVC 패턴의 의미를 다시 짚어보자 
<mark style='background-color: #f6f8fa'>back to basic 하는 이번 버전의 코드가 되겠다</mark>
<br>
MVC 각각의 역할에 대해서 검색을 해보고 스스로 많이 고민하며 정리한 결과이다. 명확한 정답이라고 할 수는 없지만, 대부분의 많은 사람들이 답해준 결과에서 공통적으로 담긴 내용들만 선별해서 나의 워딩으로 정리를 해보았다.
<br>
테코블 사이트에서 검색하다 나와 같은 고민을 한 사람들에게 주는 선물과도 같은 내용을 확인했다

[고마워요 테코블!](https://tecoble.techcourse.co.kr/post/2021-04-26-mvc/)

#### Controller
<mark style='background-color: #f6f8fa'>View와 Model 사이에서 데이터를 전달해주는 역할</mark>
<br>
검색하면서 정말 많은 사람들이 나와 같은 고민을 하고 있었던 것을 다시 한번 느낄 수 있었다 
<br>
그중에서도 가장 눈에 들어왔던 건 다음의 문장이다 
<br>

**"View에서 Model로 데이터를 전달할 때 어떻게 처리할 지를 생각해볼 필요가 있다"**
<br>

Controller의 역할을 어떻게, 어느 범위로 부여할 지를 먼저 정해두고 시작하라는 것이다. 스스로 구현을 해나가면서 자신의 생각에 맞게 역할을 부여하면 된다는 것이다.
데이터를 전달만 할 수도 있고 처리 및 검증도 할 수 있고, 더 나아가서 게임을 전체적으로 총괄할 지,, 이런 부분들은 자기가 정하는 셈이다. 그것이 개발자의 역할이며, 다른 사람들과 공유하면서 성장하는게 진짜 성장하는게 아닐까라는 생각이 들었다 
<br>

위의 내용을 확인하고 나는 콘솔로 부터 받은 데이터를 따로 처리하고 검증하는 **InputController**를 만들게 되었다
컨트롤러의 역할을 더 구분하고자 했다 

<br>

- 클라이언트의 요청을 받으면 해당 요청에 대한 실제 업무를 수행하는 Model을 호출한다. 
- 클라이언트가 보낸 데이터가 있다면, 모델을 호출할 때 전달하기 쉽게 적절히 가공한다. 
- Model이 업무 수행을 완료하면 그 결과를 가지고 화면을 생성하도록 View에 전달한다. 
- 즉, 클라이언트의 요청에 대해 Model과 View를 결정하여 전달하는 일종의 조정자로서의 일을 한다.
- Controller는 다른 컴포넌트들에 대해 알고 있다. 자기 자신 외에 Model과 View가 무엇을 수행하는지 알고 있다.

#### View
<mark style='background-color: #f6f8fa'>최종 사용자에게 무엇을 화면으로 보여준다</mark>
<br>
최종 사용자에게 무엇을 화면(UI)로 보여준다. 화면에 무엇을 보여주기 위한 역할을 한다
<br>
View 역시도 다른 컴포넌트들에 대해 알지 못한다. 자기 자신이 무엇을 수행하는지만 알고 있다.

#### Model 
<mark style='background-color: #f6f8fa'>어플리케이션이 무엇을 할 지 정의한다</mark>
<br>
Model은 다른 컴포넌트들에 대해 알지 못한다. 자기 자신이 무엇을 수행하는지만 알고 있다

<br>
마지막으로 이렇게 MVC로 구분해서 진행하는 결정적인 이유는 관심사를 분리하기 위함이라는 것까지 알아두면 MVC에 대한 전체적인 개념은 이해했다고 할 수 있다!
철저하게 분리한 만큼 변화가 발생했을 때도 능동적으로 대처할 수 있다!


## V2 구현 
<mark style='background-color: #f6f8fa'>하라는 대로 진행하자</mark>
<br>

```markdown
racingcarv2                     
├─ controller                   
│  └─ RacingCarController.java  
├─ exception                    
│  └─ ErrorException.java       
├─ model                        
│  ├─ Car.java                  
│  ├─ Name.java                 
│  ├─ Position.java             
│  ├─ RacingCars.java           
│  └─ RoundTotal.java           
├─ util                         
│  ├─ converter                 
│  │  ├─ StringToCarList.java   
│  │  └─ StringToNumber.java    
│  └─ RandomGenerator.java      
├─ view                         
│  ├─ InputView.java            
│  └─ OutputView.java           
└─ MainApplication.java         
```


## V2 부족한 점
- 정적 팩토리 메서드 형태를 적용한 생성자를 구현하지 못했다
- 테스트 대상, 명확한 근거를 가지고 선택하기 
- 구현 이후에 기능 구분을 클래스 별로 더 명확하게 구분한 점 (웬만하면 구현 전에 미리 구획화 해두는 것이 좋다)
- git commit 작성할 때 type 더 고민하고 확실하게 방향 정하기 (특히, test 코드 작성 시 feat -> test 로 명시할 것)
- DTO를 적용해보려고 했지만 적용하지 못한 점 
- Controller를 데이터를 전달하는 역할로 제한하려 했지만, 구현하고 나서 확인하니 데이터를 전달하는 것 외에도 전체적인 흐름을 제어하는 역할을 수행하고 있다
    - 데이터를 전달하는 역할만 진행했다면 Game 클래스를 하나 더 형성해서 비즈니스 로직을 다루는 클래스를 하나 더 만드는 방법은 어떤지
    - Service를 활용하는 방식도 괜찮을 듯 하다 (핵심 비즈니스 로직을 관리하는 Service 단)
- Validator, 기본적으로 검증해야 하는 상황은 ....Validator 클래스로 묶는 것도 괜찮을 듯 하다 (단일 검증 책임? 분할 검증 책임!)
<br> (ex) NumberValidator - null, empty 한 상황. 수로 구성되어 있지 않은 경우 (InputView에서 대신 처리한 기능들을 대체하는 방향은 어떤지)

## 2주차 미션을 마치며 
<mark style='background-color: #f6f8fa'>소감문의 내용의 일부를 가지고 왔습니다</mark>
<br>

*이번 주차동안 공부하면서 느낀 것들을 키워드로 생각해보자면 “과설계, 미션의 방향에 관한 이해, 다시 기본으로”입니다*
<br>

*테스트할 때 공통으로 제가 사용하는 클래스, 혹은 모델 내의 클래스 구조를 이번에도 적용하기 위해서 1주 차 미션을 다시 한번 정리하고, 부족한 부분을 보완하며 저만의 생각과 철학을 점진적으로 구체화하자는 목표를 세웠습니다*

독학을 하며 느꼈던 저의 니즈들을 채우고자 우테코에 지원했지만 어느 순간 우테코의 미션에 집중하지 않고 오직 미션에 주어진 <u>프로그램의 구현에만</u> 신경쓰고 있는 자신을 보며 마음을 다시 잡아야겠다는 생각을 많이 했습니다. 1주차 미션의 구현 내용을 토대로, 좋은 것들은 지속적으로 발전시키고 부족한 부분은 채워가면서 매 주차 주어진 목표에 초점을 두고 프리코스를 보내야 겠다는 생각을 했습니다.

*Controller, OutputView, InputView를 모두 인터페이스로 선언한 이후에 출력 예시를 바탕으로 구간을 구분하려 했습니다*
<br>
각각의 공통된 역할을 선언해서 implements 혹은 추상 클래스를 활용하여 구현하려 했습니다. 지난 코드 리뷰 중 전체적인 코드 흐름이 눈에 쉽게 들어와 읽기 편했다 라는 평가가 있어서 택한 방식이었습니다. 

*MVC 패턴을 적용하면서 다시 한번 MVC 각각의 구성 요소들의 역할을 더 명확하게 이해하려 했습니다.*
<br>
MVC 패턴을 1주 차 때도 이번 2주 차 때도 적용했는데, 제대로 인지하지 않은 상황에서 생각하지 않고 임의로 생각한 역할에 맞게 구현하지 않았나 라는 생각도 들었기에 위에서 언급한 MVC 패턴을 다시 공부했습니다.

*또한, 검증의 책임을 단순히 Model에 부여할지 혹은 View에서 input으로 받는 데이터를 먼저 필터링하고 검증을 진행할지에 대해서도 고민했습니다.*
<br>
오픈 커뮤니티에서도 많은 분들이 고민을 겪고 있는 대표적인 문제였습니다. 어플리케이션의 안정성을 우선적으로 고려하여 검증을 2번에 나눠서, 분할해서 검증하는 방식으로 프로그램을 구현했습니다. 

*주 차의 목적인 “함수를 분리하고, 함수별 테스트 작성하기”와 과제 진행 방식에 언급된 “기능을 구현하기 전 기능 목록을 만들고 기능 단위로 커밋하기”를 중점적으로 진행했습니다*
<br>
<br>
<u>V2 버전의 코드를 다시 작성하게 된 이유입니다.</u>

<br>

```markdown
구현하는 과정에서 “기능 명세”를 기준으로 기능을 분리했고, 이를 커밋 단위로 진행하려고 했지만 한 가지 클래스를 생성하고 관련된 테스트를 진행하는 과정에서
서로 다른 기능 명세에 속한 기능에 체크하는 저 자신을 볼 수 있었습니다. 기능 명세를 세분화 하는 것은 좋지만 같은 클래스에 종속되는 내용들을 하나의 클래스로
 묶어야 구현하는데 초점을 더 구체화할 수 있겠다는 생각이 들었습니다. 비록 구현을 진행하는 동안에는 같은 클래스의 기능들이 퍼져 있었던 것이 아쉬웠지만, 
 구현을 마친 이후에 다시 README.md 파일을 수정하면서 어떤 방식으로 세분화 할지를 알 수 있었습니다
```

<mark style='background-color: #f6f8fa'>기본중의 기본이라고 할 수 있겠지만 기능 명세 사항을 읽고 분석하다 보면 여러 갈래로 쪼개지는 것을 확인할 수 있습니다</mark>
<br>

기능을 작게 작게 분리하는 것까지는 좋았지만 코드를 구현하고 README 파일에서 체크를 하려다 보니 서로 다른 명세 사항에 존재하는 기능들을 체크하는 모습을 확인했습니다. 명세 사항별로 구분하는 것이 아닌 클래스 별로, 같은 클래스내에 종속하는 기능들을 함께 묶어줄 수 있도록 작성해야 하는 것을 느낄 수 있었습니다.
<br>

```markdown
함수별 분리하는 연습, 그리고 테스트를 작성하는 것도 진행하면서 여러 고민이 생겼습니다. 테스트는 기본적으로 어떻게 검증을 진행할지와, 테스트하지 
못하는 private 메서드의 경우에는 어떻게 처리해야 할지를 많이 고민했습니다. 추가적으로 프로덕션 코드 그리고 테스트 코드 사이의 연관 관계를 생각하면서 
과연 테스트 코드를 위해 프로덕션 코드 내의 변화를 만들어도 괜찮을까 라는 고민을 많이 했었습니다. 
```
<hr>

```markdown
테스트를 진행하면서 “생성자를 오버로딩하는 방식도 괜찮을까?”라는 고민도 했습니다. 특히 등록된 Car의 Distance(Position) 을 등록 시 0으로 입력하고
 싶어 생성자 2개를 작성했는데 이것이 과연 올바른 방식인지를 생각했습니다. 결과적으로 프로덕션을 위한 테스트를 작성할 뿐, 테스트를 위한 프로덕션을 작성하면
  안 되는 것을 느낄 수 있었습니다. 기능 명세에 따라 작성된 프로덕션 코드임에도 불구하고 테스트 코드를 위한 다른 기능들이 추가된다면 오히려 혼란스러운 
  프로그래밍이 될 것이라는 생각으로 정리할 수 있었습니다.
```

*이번 주차 미션 동안에는 각각의 클래스 단위로 테스트를 구분하고 클래스에 속한 기능들을 테스트하는 코드를 작성했습니다*
<br>

Mockito의 필요성을 아직 느끼지 못해 AssertJ, JUnit5를 활용했습니다. ~~너무 나 자신을 과대평가한 것은 아닌지..?~~

```markdown
이번 주차 미션의 목적에 더 초점을 두려고 했고 생각하는 과정에서 자연스럽게 자신만의 생각과 방식을 결정해 나가는 모습이 우테코에서도 혹은 저도 
프리코스 기간 동안 성취해야 할 또 다른 미션이지 않을까 라는 생각이 들었습니다. “2가지 미션 목표에도 집중하지 못하는데, 과연 실무의 많은 기능 
명세 사항을 제대로 지킬 수 있을까?”라는 결론을 내리면서 다시 한번 전체적인 프리코스의 목적을 되새길 수 있었던 것 같습니다.
```

<mark style='background-color: #f6f8fa'>실무에서는 더 많은 요구 사항, 더 많은 예외와 그리고 예외 처리를 진행해야 하는데. . 이런 작은 프로그램에서 요구하는 사항 조차 제대로 이해하지 못한다면 미래를 그리기 힘든 사람이 될 수 있다는 것을 다시 한 번 느끼며 2주차 미션 회고를 마칩니다</mark>
<br>

긴 글 읽어주셔서 감사합니다!



