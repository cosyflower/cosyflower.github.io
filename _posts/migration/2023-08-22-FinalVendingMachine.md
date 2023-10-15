---
layout: single
title: "[23.08.22] 프리코스 대비 - 자판기 미션 최종"
categories:
    - beartoblog # category 일치했는지 확인하기 
tags:
    - 'OffTheRecord' # tag도 마찬가지로 같이 띄울 수 있다 
    - 'VendingMachine'
toc: "true"
toc_sticky: "true"

date: 2023-08-22
last_modified_at: 2023-08-22
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
# [Day 24 08.22] 자판기 마무리까지!!
#우테코# #23.08.22 #4기
## 자판기를 끝장내는 날 
### 최저 금액 구하기 in ProductList
```java
public int getMinPrice() {
    return productList.stream()
            .min(this::compare)
            .get().getPrice();
}

private int compare(Product p1, Product p2) {
    return p1.getPrice() - p2.getPrice();
}
```

-> Comparator를 위한 메서드 정의 이후
-> min() 그리고 stream 을 활용해서 minPrice를 반환하는 메서드를 정의했다 

### 테스트 코드 작성 관련해서 
```java
@ParameterizedTest
@CsvSource(value = {"[사이다,1000,20];[콜라,200,1]:200",
        "[사이다,1000,20];[콜라,20000,1]:1000",
        "[사이다,1500,20];[콜라,20030,1]:1500"}, delimiter = ':')
void get_min_price(String str, int result) {
    ProductList productList = new ProductList(str);
    int minPrice = productList.getMinPrice();
    Assertions.assertThat(minPrice).isEqualTo(result);
}

//MachineController.class 수정 
Money money = InputController.setUserMoney(productList.getMinPrice()); // 상품 최저 금액

```
-> CsvSource 를 활용해서 작성했다 - 항상 value, delimiter 명시하는 것 잊지말기! 
-> setUserMoney(int) 오버로딩 활용한 메서드 정의, 최소 금액을 전달함으로써 검증하는 과정에서 범위에 적합한지를 검사하게 될 것이다 

*투입 금액이 상품의 최저 가격보다 작은 경우에는 다시 입력받는 방향으로 진행함*

---
그전에 다음의 예외를 고려하지 않은 것을 확인했다
상품 가격은 100원부터 시작하며, 10원으로 나누어떨어져야 한다
-> ProductValidator 에서 해당 책임을 처리해야 한다 
-> 각각의 필드 중 가격 필드에서 해당 책임을 처리해야 하기 때문에 ProductPriceValidator에서 진행 

### Product.class 내부의 검증을 진행하는 단계에서
각각의 필드에서도 검증하는 과정이 필요했다. 각 필드별 validator로 책임을 분산했다 
- ProductNameValidator
- ProductPriceValidator
- ProductQuantityValidator - 사실 수량을 0으로 넣는 것도 가능한 상황이라고 할 수 있으나, 일반적인 상황이라고 할 수 없어서 기본적으로 MoneyValidator를 따라가는 방향으로 진행했다 

```java
private final String name;
private final int price;
private final int quantitiy;

public Product(String[] values) {
    // String으로 입력된 문자열
    validate(values);
    this.name = values[0];
    this.price = Converter.toInt(values[1]);
    this.quantitiy = Converter.toInt(values[2]);
}

private void validate(String[] values){
    new ProductNameValidator(values[0]);
    new ProductPriceValidator(values[1]);
    new ProductQuantityValidator(values[2]);
}
```

### setOrderProduct()
Client가 주문할 상품을 입력 받는 InputController의 역할이다 
이 때 협력해야 할 관계는 vendingMachine 으로 잡았기 때문에 해당 클래스를 형성해보자 

---
자판기(VendingMachine) 그리고 Client
현재 CoinGroup, ProductList, Money 를 형성한 상황이다. 이 때 Client 에서 입력한 금액과 상품명을 토대로 **자판기와 Client 간의 새로운 협력 관계 상황이 발생했다** 

### 물론 각각의 타입과 직접적인 협력을 맺는 것도 좋지만 
일일이 하나하나 하는 것은 오히려 더 많은 책임을 부과하는 것이다 
CoinGroup, ProductList, Money는 결과적으로 자신이 어떻게 생성되는지와 자신과 연관된 로직을 부여한 상황. Client와 협력을 맺기 위해서 새로운 클래스를 하나 더 만들자

#### 복잡한 상황에서는
상위 클래스 혹은 인터페이스를 규정해서 새로운 협력 관계를 얻을 수 있도록 했다
VendingMachine, 상위의 3가지 클래스를 모두 포함하고 있는 클래스를 하나 형성하자 
 

## 세팅을 모두 진행한 다음에
세팅을 마친 각각의 데이터들을 하나의 클래스로 모으는 작업을 진행했다. 결과적으로 execute()의 과정에서 입력된 값들을 처리하는 다른 클래스를 하나 더 만들었다고 생각하면 되곘다. 이전의 클래스들은 세팅과 연관된 작업을 진행했다면, 이번에 형성한 상위 클래스(VendingMachine)은 입력한 값들을 토대로 데이터를 세팅하고 실질적인 거래 행위가 이뤄진다고 생각하면 되겠다 


## VendingMachine - 자판기 
```java
public class VendingMachine {

    private final ProductList productList;
    private final CoinGroup coinGroup;
    private final Money machineMoney;

    public VendingMachine(ProductList productList, CoinGroup coinGroup, Money machineMoney) {
        this.productList = productList;
        this.coinGroup = coinGroup;
        this.machineMoney = machineMoney;
    }

    // 상품명 찾기 ( execute() 과정에서 구매하려고 하는 상품이 존재하는지 확인하기
    // 이럴 떄도 방어적 복사를 해야하는지?? 아니면 그럴 필요 없이 바로 사용해도 되는 것인지?
    // 예외처리 위치도 생각해보기

    // ProductList에 협력을 요청한다
    public Product findProduct(String productName) {
        return productList.findProduct(productName);
    }

}
```

-> orderProduct를 입력하게 되면 해당 상품이 존재하는지를 확인해야 하는데
-> findProduct()가 해당 역할을 수행하게 된다 

## ==고민 - findProduct() 조회 하는 메서드도 방어적 복사??==



### 상품 판매 관련 메서드 정의 ( VendingMachine.sellProduct(Product) )
-> findProduct() 으로 반환한 Product 정보를 인자로 전달합니다
-> Product 내 quantity 값에서 1을 뺍니다 
	-> [**예외**] quantity가 0 인 경우
	-> [**예외 처리**] “[ERROR] 해당 상품이 소진되었습니다. 다른 상품을 골라주세요” - 에러 메세지
	-> [**예외 처리**] 다시 상품을 입력 받는다 -> setOrderProduct() 에서 해야하는 일이겠군!!

### setOrderProduct() -> findProduct(String)
해당 문자열의 이름과 같은 상품이 존재하는지 확인한다
상품의 수량이 1 이상인지 확인한다 

#### 기존의 findProduct(String) 에서는 상품명과 동일한 상품을 탐색하는 것에 불과
이제 해당 상품이 존재하지 않은 경우와 그리고 quantity가 1보다 작은 경우에 관한 예외처리를 진행해보자

리팩토링 이전의 코드 (상품명이 존재하는지만 확인했다면)
```java
public Product findProduct(String productName) {
    return productList.stream()
            .filter((product) -> product.getName().equals(productName))
            .findFirst()
            .orElseThrow(() -> new IllegalArgumentException(Constants.ERROR_NOT_EXISTING_PRODUCT));
}
```

리팩토링 이후의 코드 (수량이 0인 경우에 대해서도 예외 처리를 진행했다)
```java
public Product findProduct(String productName) {
    Product foundProduct = productList.stream()
            .filter((product) -> product.getName().equals(productName))
            .findFirst()
            .orElse(null);

    if (foundProduct == null) {
        throw new IllegalArgumentException(Constants.ERROR_NOT_EXISTING_PRODUCT);
    }

    if (foundProduct.getQuantity() == 0) {
        throw new IllegalArgumentException(Constants.ERROR_SOLD_OUT_PRODUCT);
    }

    return foundProduct;
}

```

### 올바른 상품명 입력 완료!! -> vendingMachine에서 판매 처리해야 한다 

*==final 관련해서, 값의 변동이 존재하는 필드에 관해서는 사용이 불가능하다. 해당 값이 수정될 것이기 때문에 quantitiy 혹은 userMoney에는 final 필드를 붙여선 안 된다==* 

- [ ] 해당 Product 에서 수량을 1을 차감한다
- [ ] userMoney에서 product의 가격 만큼 차감한다 

```java
vendingMachine.sellProduct(orderedProduct);

public void sellProduct(Product orderedProduct) {
    // 존재하고 수량이 1 이상인 상품명 orderedProduct
    // 수량을 줄여야 하고
    orderedProduct.minusQuantity();
    // userMoney 역시 상품의 가격만큼 차감해야 한다
    userMoney.subtractPrice(orderedProduct.getPrice());
}

public void minusQuantity() {
    this.quantity -= Constants.QUANTITY_ONE;
}

public void subtractPrice(int price) {
    this.money -= price;
}

```



## 잔돈 반환
* 남은 금액이 상품의 최저 가격보다 적거나, 모든 상품이 소진된 경우 바로 잔돈을 돌려준다.
* 잔돈을 반환 할 수 없는 경우에는 가능한 만큼만 진행하기 

### vendingMachine.finish() 조건 (반환해야 하는 조건)
- 남은 금액이 상품의 최저 가격보다 작은 경우 
- 모든 상품이 소진된 경우

```java
public boolean finish() {
    // 잔돈을 반환해야 하는 상황이다
    // 1. 남은 금액이 상품의 최저 금액보다 작은 경우
    // 2. 상품이 모두 소진된 경우
    return lowerThanMinPrice() && checkProductQuantity();
}

```

```java
private boolean lowerThanMinPrice() {
    if(userMoney.getMoney() < productList.getMinPrice() ) {
        return true;
    }

    return false;
}


private boolean checkProductQuantity() {
    return productList.getProductList()
            .stream()
            .anyMatch((productInfo) -> productInfo.getQuantity() == 0);
}

```


### if(!vendingMachine.finishi()) - 반환하지 않고 계속해서 상품명을 물어보는 상황
```java
if(!vendingMachine.finish()) {
    // 끝내야 하는 경우가 아니라면 남은 금액만 출력하면 된다
    OutputView.printRemainingMoney(vendingMachine.getRemainingUserMoney());
    execute();
}
```
-> 남은 userMoney 출력한다
-> userMoney.getMoney() 를 출력하게 되고, 반복하게 된다 by Recursion

계속해서 상품명을 물어보고 차감하고 남은 금액을 알려주게 된다 

## returnChange() - 최소한의 동전만 사용해야 한다
vendingMachine.finish() 인 상황이라면 returnChange() - 잔돈을 반환해야 한다 

### 반환 조건 
잔돈은 최소의 동전 (다시 말해, 큰 단위의 동전들을 우선적으로 교환해줘야 한다)
잔돈을 반환하지 못한다면? 가능한 금액까지만 반환한다 
---
## ==고민!==
```java
public List<Coin, Integer> checkCoinGroup() {

}

public ChangesCoinGroup checkCoinGroup() {

}
```

-> 간단하게 만들고 싶다면 기존의 CoinGroup 을 활용하는게 더 빠를 것이다
-> 하지만 확장성의 측면에서는 반환하는 CoinGroup과 연관 지어 ChangesCoinGroup 이라는 새로운 클래스를 정의하는 것이 추후의 확장에 있어서 더 좋은 방법일까?? 

### 반환하려면 현재 CoinGroup 그리고 남은 userMoney 간의 협력이 필요한 상황이다 
userMoney.getPrice() 와 CoinGroup 간 연관 관게를 생각해야 한다 

```java
private void returnChange() {
    // 잔돈을 반환하는 상황
    // vendingMachine에게 잔돈 반환에 대한 협력 요청(userMoney 제공)
    // 정보를 받아서 출력하는 역할만 수행하면 된다
    OutputView.printRemainingCoinGroup(vendingMachine.checkCoinGroup());
}


public LinkedHashMap<Coin, Integer> checkCoinGroup() {
    int remainedMoney = userMoney.getMoney();
    LinkedHashMap<Coin, Integer> coinAmount = coinGroup.getCoinAmount();
    LinkedHashMap<Coin, Integer> remainedCoinAmount = new LinkedHashMap<>();
    // 잔돈 반환해야 하는 상황
    for (Coin coin : coinAmount.keySet()) {
        Integer remainedAmount = coinAmount.get(coin); // 유지하고 있던 개수
        int requiredAmount = remainedMoney / coin.getAmount();
        if( remainedAmount < requiredAmount){
            requiredAmount = remainedAmount;
        }
        remainedCoinAmount.put(coin, requiredAmount);
        remainedMoney = userMoney.getMoney() - coin.getAmount() * requiredAmount;
    }
    return remainedCoinAmount;
}


public static void printRemainingCoinGroup(LinkedHashMap<Coin, Integer> checkCoinGroup) {
    System.out.println(Constants.MACHINE_FINAL_COINS_MESSAGE);
    for (Coin coin : checkCoinGroup.keySet()) {
        System.out.println(coin.getAmount() + Constants.MACHINE_REMAINING_COINS_PREFIX
                + checkCoinGroup.get(coin) + Constants.MACHINE_REMAINING_COINS_SUFFIX);
    }
}

```

-> Wrapping의 문제점 발생
-> LinkedHashMap<Coin, Integer> 형태가 드러나 있는 상황이다 
-> 부모 생성자 호출시 오버로딩을 활용하자!!


### 예외 - 반환하지 못하는 상황  
- 남은 금액이 자판기 내 금액보다 큰 경우 
- 동전으로 표현이 불가능한 경우 

-> 반환할 때 가장 큰 단위서부터 진행
-> 단위로 나눌 때 몫이 0일 때 까지 진행하고, 남은 금액은 그 다음 단위에서 나눗셈 연산 진행
-> 반복하면 결과적으로 표현이 가능한 애들만 반환하게 되는 형태가 된다

<br>
***
    
    진정한 경쟁력은 자신의 가치를 공유하는 것


[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}