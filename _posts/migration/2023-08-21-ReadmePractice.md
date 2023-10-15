---
layout: single
title: "[23.08.21] README.md 파일 연습하기"
categories:
    - beartoblog # category 일치했는지 확인하기 
tags:
    - 'OffTheRecord' # tag도 마찬가지로 같이 띄울 수 있다 
    - 'README'
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
# [Day 22] activate() 관련 README.md 연습
#우테코  #4기 #3주차 #23.08.21
## 프로그램 명세 사항 - 사용자로 부터 투입 금액 입력부터 진행
* 사용자가 투입한 금액으로 상품을 구매할 수 있다.
* 남은 금액이 상품의 최저 가격보다 적거나, 모든 상품이 소진된 경우 바로 잔돈을 돌려준다.
* 잔돈을 반환할 수 없는 경우 잔돈으로 반환할 수 있는 금액만 반환한다.
  * 반환되지 않은 금액은 자판기에 남는다.


## 투입 금액 입력 받기 및 세팅 - 실질적인 구현 순서를 작성한다고 생각
- [x] 사용자로부터 투입할 금액을 입력 받고 세팅합니다 
- [x] “투입 금액을 입력해주세요” 메세지를 출력한다
- [x] 투입 금액을 입력 받는다
- [x] 입력을 돈으로 세팅해야 한다 (예외처리한다)
  - [x] [**예외**] 투입한 금액이 최저 금액보다 낮은 경우
  - [x] [**예외 처리**] 에러 메세지를 출력합니다
  - [x] [**예외 처리**] 투입 금액을 다시 입력 받는다 
- [ ] 입력한 문자열에서 투입한 금액을 추출한다  
- [ ] 투입한 금액을 저장합니다 


### 투입 금액 입력 받기 
기본적으로 투입한 금액의 조건을 살피기 전에, 입력한 문자열이 수로 입력이 되어 있는 상태인지를 항상 확인해야 한다고 했었다 

### 투입 금액 관련 Class 하나 만들기 - 해당 클래스 내 조건을 검증(Money.class)
```text
Money 클래스를 만든 것도 결국 primitive 한 Int를 숨기는 과정이라고 생각하자.
일종의 Wrapping 한다고 생각하기 
```

### InputMoneyValidator
-> null, empty한 경우 (아무런 값도 입력되지 않은 상황) 
-> 수로 입력이 되어있는지 확인하기 ( ^[0-9]*$ 형태인지 확인하기 )
	-> 수로 입력되어 있으나 0으로 시작하는 경우 
```java
public class InputMoneyValidator {

    private final String money;
    public InputMoneyValidator(String money) {
        this.money = money;
        validateInputMoney();
    }

    private void validateInputMoney() {
        if (money == null || money.isEmpty()) { // null || isEmpty
            throw new IllegalArgumentException("[ERROR] 아무것도 입력되지 않았습니다. 다시 입력해주세요");
        }

        if(!Constants.NUMBER_PATTERN.matcher(money).matches()) { // 수로 구성된 문자열이 아닌 경우
            throw new IllegalArgumentException("[ERROR] 숫자를 입력하지 않았습니다. 다시 입력해주세요");
        }

        if (IntStream.range(0, 1).boxed().anyMatch((num) -> money.charAt(num) == '0')) {
            throw new IllegalArgumentException("[ERROR] 0으로 시작하는 숫자입니다. 다시 입력해주세요");
        }
    }
}
```

-> 검증하는 역할을 수행하는 InputMoenyValidator()
-> 검증시 확인할 조건들을 각각의 경우로 구분 지었다.
-> If 조건들을 하나의 메서드로 정의하고 이를 생성자 내에서 validateInputMoney() 에서 모두 진행하는게 아니라 각각의 검증을 독립적인 메서드 호출로 구분해도 되겠다 라는 생각이 든다 

### 항상 검증 조건을 작성했다면 테스트 코드도 작성하기

View 관련 결과를 가지고 테스트 코드를 작성하기!
```java
@ParameterizedTest
@NullAndEmptySource
@ValueSource(strings = {"0-91", "012", "250"})
void testInputValidator(String test) {
    Assertions.assertThatThrownBy(() -> new MoneyValidator(test))
            .isInstanceOf(IllegalArgumentException.class)
            .hasMessageStartingWith("[ER,R]");
}

```

-> 예외 상황 별로 테스트 코드를 구분하는게 더 좋다는 생각이 들었다 (각각을 구분하면 더 다양한 경우에 대한 대비가 가능하다고 생각했기 때문) 
-> hasMessageContaining() 으로만 확인하고 있는데 이 부분을 더 고민해봐야 겠다 

*(InputController - InputView 로 부터 사용자의 입력을 받아야 하는 상황)*

## Money - MoneyValidator 완료, InputView 구성하기
*InputView - 소개 맨트 작성하고, 사용자로부터 입력을 받는다. 입력 받은 문자열을 반환한다*
```java
public static String inputUserMoney() {
    System.out.println(Constants.INPUT_CLIENT_MONEY_MESSAGE);
    return Console.readLine();
}
```
-> 소개 멘트만 작성했고
-> 사용자의 입력을 반환하는 형태라고 할 수 있다  

### InputController - Money money 정보가 필요한 상황, InputController에게 요청
InputController - 사용자의 입력을 받으면 반환해야 하는 타입의 클래스 내 생성자에서 검증까지 모두 진행해야 한다. 검증 중간에 발생하는 예외와 관련해서도 처리할 책임을 가지고 있다 
```java
public static Money setUserMoney() {
    try {
        return new Money(InputView.inputUserMoney());
    } catch (IllegalArgumentException e) {
        System.out.println(e.getMessage());
        return setUserMoney();
    }
}
```
 
구조 유의하기 
-> 원하는 데이터로 return , 생성자 인자로 InputView로부터 전달받은 데이터를 받아야 하는 상황
-> 예외가 발생하는 경우에 재귀를 활용해서 다시 입력을 받을 수 있도록 진행함 

### 최종적으로 MachineController는
입력된 데이터, 검증까지 마무리한 데이터를 받을 수 있는 상황이다 
```java
Money money = InputController.setUserMoney(); // 정보 저장까지 진행 완료
```

정보를 입력받고 - 예외 처리 - 검증된 데이터를 InputController 부터 받는 과정이 굉장히 복잡하다는 걸 체감할 수 있는 상황이다

## 데이터를 입력 받는 과정의 전체적인 로직을 작성 완료
최저 금액보다 낮은 경우에도 에러 처리를 해야 한다
-> 최저 금액에 대한 정보를 받아야 한다 
-> 최저 금액에 대한 정보를 받은 상황에서 검증해야 한다 

### new Money(String, int minPrice)
생성자 오버로딩을 적용하자. minPrice 까지 인자로 전달한다면? 이 때는 새로운 검증을 진행!
```java
public Money(String money, int minPrice) {
    new UserMoneyValidator(money, minPrice);
    this.money = Converter.toInt(money);
}
```

-> 검증하는 클래스만 달라졌다 (추가로 minPrice에 대한 정보를 넘겨주는 것 까지 확인할 수 있다)

userMoneyValidator를 하나 더 형성해서, 기존의 moneyValidator 검증을 그대로 진행을 하고
(어차피 기존의 validator는 수 관련해서 검증을 할 때마다 반복해야 하기 때문에 상속)
기존의 검증 + 추가적인 검증을 진행하기 

-> 최저 금액보다 낮은지를 확인하면 되겠다 

```java
public class UserMoneyValidator extends MoneyValidator{
    private final int minPrice;

    public UserMoneyValidator(String money, int minPrice) {
        super(money);
        this.minPrice = minPrice;
        isRightRange(minPrice);
    }

    private void isRightRange(int minPrice) {
        // super() 하면서 검증된 money 정보가 저장된 것을 알 수 있다
        if (Converter.toInt(money) < minPrice) {
            throw new IllegalArgumentException(Constants.NOT_IN_RANGE_MESSAGE);
        }
    }

    // UserMoney 관련 로직 작성하기
}
```

### 최저 금액 조건까지 반영하기
```java
public static Money setUserMoney(int minPrice) {
    // refactor : int minPrice 인자로 전달
    try {
        return new Money(InputView.inputUserMoney(), minPrice);
    } catch (IllegalArgumentException e) {
        System.out.println(e.getMessage());
        return setUserMoney(minPrice);
    }
}


// MachineController.class
// 최저 금액 구하는 로직 필요(ProducList)
Money money = InputController.setUserMoney(100); 
```

-> 기존에 아무런 정보를 전달할 필요가 없었지만, 상품의 최소 금액을 전달해야 하는 상황
-> 임의로 100을 넣었다

### 테스트 코드 작성해보기 
@CsvSource에 대해서 알아보자 ( 복수의 인자로 진행을 해야 하는 상황 )

- values = 
- delimiter = ‘:’ ( default 는 콤마로 되어 있다 )

데이터를 value로 전달한 상황, 하나의 묶음을 “” 로 작성해주면 된다. 원하는 타입을 명시해서 인자로 작성해주면 되겠다 

#### CsvSource - value, delimiter 작성하기
```java
@ParameterizedTest
@CsvSource(value = {"250:1000", "20:200"}, delimiter = ':')
void valid_Input_Money_With_MinPrice(String money, int minPrice) {

    Assertions.assertThatThrownBy(() -> new Money(money, minPrice))
            .isInstanceOf(IllegalArgumentException.class)
            .hasMessageStartingWith("[ER.]");
}
```

-> value 형태로 데이터를 전달해주고
-> 분류할 delimiter 형태도 작성해줘야 한다
그러면 250 1000 형태로 구분이 되는데 이때 원하는 타입은 인자에서 명시해주면 되겠다 
*~250을 String 형태로 인식하고, 1000은 int 형태로 인식한다고 생각하면 되겠다* 

### AssertJ 관련 인사이트 
[Introduction to AssertJ](https://www.baeldung.com/introduction-to-assertj)
-----
---
## 기존 작성했던 Code 리팩토링을 진행해보자! 
### [Rewind] README.md 파일을 작성할 때 ==세팅(예외 처리) -> 명세 사항== 
기본적으로 세팅 그리고 예외 관련해서 작성하고 이후에 명세 사항를 고려해야 한다
간단하게 생각하면 basic 한 검증 이후에 specified 한 검증을 해야 한다는 것이다 

### 세팅 - 수(문자열 관련 - Money 세팅 (추가적인 규칙, specified validation 필요)
이 때 네이밍 항상 유의할 것 (객체 기준의 네이밍을 진행할 것) 
-> 기본 numberValidation이 Money를 세팅할 때도 활용될 수 있다는 것 ( MoneyValidator )
-> 공통적인 검증이 필요하다면? - extends 상속 개념을 활용할 수 있다 ( UserMoneyValidator )
Money 클래스에서도 필드를 int 형 하나만 유지하고 있는 상황 (그래도 포장하는 모습을 볼 수 있다) 
-> int 형태이면서도 특별한 규칙에 대해 검증이 가능한 클래스가 바로 Money 라고 할 수 있겠다 

### 세팅 - 이름(문자열 관련) - 상품 세팅 (Product)
우선 이름에 대한 기본적인 검증을 해야 한다 - NameValidator 
-> null, isEmpty()
-> 문자가 아닌 다른 경우로 구성된 문자열의 경우

그리고 나서 상품에 대한 검증을 진행하게 된다 - ProductListValidator
상품 - 상품명, 가격, 수량
상품명 - 이름 세팅 관련 + 중복 되었는지 확인하는 로직이 필요하다 
가격 - 돈 세팅 관련(예외 처리 포함) - moneyValidator 
수량 - 수(number) 세팅 관련(예외 처리 포함)  - NumberValidator 필요 

가장 먼저 할 일은 명세 사항을 읽으면서 기본적으로 필요한 validator 그리고 필요한 타입(원시적인 값들도 모두 포장해달라고 했었다) 예상을 좀 해두고 진행하는 것이 좋다 
---

## 자판기에 금액을 투입, 동전 변환하는 과정
- [ ] "자판기가 보유하고 있는 금액을 입력해 주세요."을 출력해야 한다.
- [ ] 보유금액 입력을 받아야 한다.
- [ ] 입력을 돈으로 세팅해야 한다
- [ ] 문자열에서 돈을 추출한다
- [ ] 자판기 보유 금액을 저장한다 


<br>
***
    
    진정한 경쟁력은 자신의 가치를 공유하는 것


[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}