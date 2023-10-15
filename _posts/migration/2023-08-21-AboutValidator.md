---
layout: single
title: "[23.08.21] Validator 관련 고민"
categories:
    - beartoblog # category 일치했는지 확인하기 
tags:
    - 'OffTheRecord' # tag도 마찬가지로 같이 띄울 수 있다 
    - 'Validator'
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
# [Day 23] 상품명, 상품 정보, 가격에 대해서 
#우테코 #3주차 #23.08.21
### 기존에 진행했던 방식으로 이번엔 ProductList 정보를 받는 과정을 생각해보자

### 고민 1 . productList를 받는 과정을 먼저 생각해보자면 
-> productList는 사실상의 일급 컬렉션 역할을 수행한다 ( List<Product> 형태 )
-> setProductLIst() 메서드 내에서 new productList()의 인자로 정보를 전달함으로써 검증을 진행할 지
혹은 이전에 검증을 마친 product 들을 List 형태로 저장해두고, 저장된 변수를 인자로 전달할 지 고민이다

### 결론 분리하자
입력으로 받는 상품 리스트 
그리고 구매할 당시에 입력하는 상품을 검증하는 것을 각각으로 구분해서 생각을 해보자

### 입력으로 받는 상품 리스트를 검증해보자 

#### 생성자 관련 주의 사항
-> 생성자에서 기본적으로 검증을 진행한 다음에 자신의 필드에 맞게 저장하는 순서로 진행하고 있다
-> 자신의 필드에 맞게 저장하려고 할 때 타입 간 불 일치 하는 상황이 있다면 Converter를 적용하려고 생각
```java
private final List<Product> productList;

// 인자와 관계 X(끊음), 내부 요소만 같은 주소값을 유지한다
public ProductList(String productList) {
    new ProductListValidator(productList);
    this.productList = Converter.getProducts(productList);
} 
```
여기서 중요한 점은 저장해야 할 필드는 List<Product> 형태 반면 입력된 정보는 String이라는 점이다.
기본적으로 검증할 때 필요한 정보는 String 정보가 되겠다. 

-> 검증을 진행하고 Converter를 활용해서 정보를 변환한 상황이 되겠다 
-> getProducts 는 String 형태로 전달된 정보를 활용해서 각각의 상품 정보를 추출해야 한다

### ProductListValidator 설정
```java
private final String productList;

public ProductListValidator(String productList) {
    this.productList = productList;
    isNullOrEmpty();
    isValidatedProductList();
    isDuplicatedProductList();
}

// 검증 메서드
// 검증하면서 예외가 발생하면 throw 해주면 된다
public void isNullOrEmpty() {
    if( productList == null || productList.isEmpty() ) {
        throw new IllegalArgumentException(Constants.ERROR_PRODUCT_EMPTY_OR_NULL_INPUT);
    }
}

public void isValidatedProductList() {
    if( Arrays.stream(productList.split(";"))
            .filter((input)-> Constants.PRODUCT_PATTERN.matcher(input).matches())
            .count() != productList.split(";").length ) {
        throw new IllegalArgumentException(Constants.ERROR_WRONG_PRODUCT_INPUT);
    }
}

public void isDuplicatedProductList() {
    if( (!isNotDuplicatedProductList()) ) {
        throw new IllegalArgumentException(Constants.ERROR_WRONG_PRODUCT_INPUT);
    }
}

```

-> 각각의 검증과 관련해서 하나의 메서드로 구분해서 작성했다 

### 고민 2 - Product 생성자
```java
private final String name;
private final int price;
private final int quantitiy;

public Product(String name, int price, int quantitiy) {
    this.name = name;
    this.price = price;
    this.quantitiy = quantitiy;
}
```
-> validate() 하는 과정도 마찬가지로 필요하다 
-> 인자 정보를 전달 받을 때 String[] 형태의 정보로??

### 최종 코드 구현 및 나의 생각 정리
```java
public static ProductList setProductList() {
    try {
        return new ProductList(InputView.inputProductList());
    } catch (IllegalArgumentException e) {
        System.out.println(e.getMessage());
        return setProductList();
    }
}
```

```java
//ProductList.class
public ProductList(String productList) {
    new ProductListValidator(productList);
    this.productList = Converter.getProducts(productList);
}

//ProductListValidator.class
public ProductListValidator(String productList) {
    this.productList = productList;
    isNullOrEmpty();
    isValidatedProductList();
    isDuplicatedProductList();
}

```

-> ProductList를 형성할 떄도 검증의 과정이 필요하다.
-> validator를 호출하는 방향으로 구현했다 
-> 검증 시 예외가 발생 가능한 경우로 구분하고 각각을 메서드로 정의했다

### ProductList 관련 테스트 코드 작성하기 
테스트 코드 작성시 각각의 상황과 관련해서 구분해서 작성하는 방향으로 진행하기 
1. 상품명 작성 시 규칙을 제대로 지키지 않은 경우
   -> 필드를 부족하게 작성한 경우
   -> 각각의 필드에 맞지 않는 문자열을 입력한 경우
   -> ‘,’ 를 구분자로 활용하지 않은 경우 .. 
2. 중복된 상품명이 존재하는 경우 


### 또 다른 고민 - 검증 2번 하는데요?
ProductList는 Product로 구성된 List. 그러면 Product를 add() 하는 과정에서도 검증이 발생하게 되는데? 
-> ProductList는 검증할 이유가 없을 지도? 어차피 내부에서 진행하기 때문 
-> 중복되는 경우가 어떤 경우가 있는지도 살펴보기 

ProducListValidator, ProductValidator 간 상속이 가능하다고 생각
Product가 부모, ProductList는 중복 여부만 추가해주면 되겠다 

### 또 다른 고민 2 - divideIntoProducts + registerProduct
의 과정을 하나의 과정으로 묶을 수는 없을지도 고민해 볼 사항이 되겠다 
-> 가독성을 다시 생각해보니 굳이 또 하나로 합치는게 도움이 되는 걸지도 생각해보게 되었다
-> 더불어 divideIntoProducts 하는 과정을 상품명 중복 검증의 경우에도 동일하게 진행하는데, 어떻게 리팩토링 할 지도 생각해볼 필요가 있겠다 
( divide는 코드가 중복되고 있는 상황이기에 Util.class에 넣어도 괜찮겠다는 생각이 들었다 )


<br>
***
    
    진정한 경쟁력은 자신의 가치를 공유하는 것


[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}