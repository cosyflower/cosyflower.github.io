---
layout: single
excerpt: "Practicing Markdown for blogging"
title: "About markdown"
categories:
    - 'skeleton'
tags:
    - ['markDown']
toc: "true"
toc_sticky: "true"

date: 2023-04-07
last_modified_at: 2023-04-07
published: True

#  bundle exec jekyll serve - test 하는 방법 
---
### 개행 : \<br>
### 중첩된 구조 : 스페이스 바 2번씩으로 조절해주면 된다

### 밑줄을 그으려면 : \<u> \</u> 해주면 된다 
### 강조 텍스트 : \**
### 기울이기 텍스트 : \*
### 강조 + 기울이기 텍스트 : \***
### 취소하기 : \~~ 여기에 문장을 작성해주고 \~~ 해주기 
### 인라인 코드 : 문장을 작성하고 중간에 코드형식으로 표현해주기 \₩ 로 마무리해주기


### 링크만 있는 Link
```html
<https://www.naver.com>
```
<https://www.naver.com>

### 링크설명 그리고 링크 주소 : \[링크 설명](링크의 주소 부분)

### 동일 파일 내 헤더 부분으로 이동하기
**[설명어](문단 주소 구간에다가 복사해서 붙여넣기)**

설명어 부분이 우리가 클릭할 때 보여지는 구간이 되겠다 
복사해서 붙여넣는 구간은 규칙을 지켜야 한다
- 특수 문자를 제거해야 하고 
- 공백을 '-' 로 변경해줘야 하고 + 대문자는 소문자로 변경해줘야 한다. 

### 인용문은 \> 로 표현해주고,ㄹ \> 의 개수
가 많을 수록 안에서 더 인용해준다고 생각하면 된다. 

```html
<cite> --- 태그와 {% raw %}{{: .small}}{% endraw %}를 함께 써서 인용문 출처도 남겨보자
```
<cite> --- 태그와 {% raw %}{{: .small}}{% endraw %}를 함께 써서 인용문 출처도 남겨보자

### checklist는 '-' 그리고 '[]'로 표현할 수 있다. 
체크하려면 '[]'안에다가 X 표시해주면 되고
### 구분선은 '***' 혹은 '---'로 표현이 가능하다 

### 테이블 만들기
```html
|**제목**|레이팅|감상평|
|:---:|---:|---|
|복수는 나의 것|⭐⭐⭐⭐⭐|내가|
|올드 보이|⭐⭐⭐⭐⭐|좋아하는|
|친절한 금자씨|⭐⭐⭐⭐⭐|박찬욱 영화!|
```

|**제목입니다**|col1|col2|
|:---:|---:|---|
|복수는 나의 것|⭐⭐⭐⭐⭐|내가| <- 각 row에 작성하기
|올드 보이|⭐⭐⭐⭐⭐|좋아하는| <- 각 row에 작성하기
|친절한 금자씨|⭐⭐⭐⭐⭐|박찬욱 영화!| <- 각 row에 작성하기

### Toggle 버튼 만들기
```html
<details>
<summary>Toggle Button에 표시될 내용들</summary>
<div markdown="1">       

😎숨겨진 내용😎

</div>
</details>
```

### 올라가는 버튼 만들기

```html
<a href="#" class="btn--success">Success Button</a>
```html

<a href="#" class="btn--success">Success Button</a>

[Default Button](#){% raw %}{: .btn .btn--primary }{% endraw %}
