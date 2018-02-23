---
title : pug
tags : ["apexsoft","templete "]
---



#pug

> templete 확장을 가능하게 하는 언어




## 사용

### 공통

* .pub 파일 
* html에서 닫는 태그가 없다
* 들여쓰기한 이후에 공백까지 태그로 된다
* 태그 속성은  괄호( ) 사용
* DialogFormBase.pug

```javascript pug
form
  div(class="form-group")
    label(for="title" class="form-label") Title
    textarea(v-model.lazy="element.title" class="form-control" name="title")
  block custom
```

### 사용

```html html
<template lang="pug">
  include DialogFormBase.pug
</template>
```

### 사용 , 확장

```html html
<template lang="pug">
  extends DialogFormBase.pug
  block custom
    div(class="form-group")
      label(for="placeholder" class="form-label") Input place holder
      input(v-model.lazy="element.placeholder" class="form-control" name="placeholder")
</template>
```



## Mixins

>  Mixins는 Vue 컴포넌트에 재사용 가능한 기능을 배포하는 방법이다.
>
> 얼핏 보면 extends와 유사하게 보일 수가 있다.
>
> 캡슐화 및 공통된 기능을 분리시켜 코드 재사용성을 높혀준다.
>
> 오버라이딩 기능도 사용할 수 있어 커스텀 및 확장에 용이하다.



- extends: 유사한 기능의 컴포넌트들을 추상화 하여 상위 컴포넌트를 만들고 차이가 있는 기능들을 하위 컴포넌트에 구현한다.
- mixins: 서로 다른 기능의 컴포넌트에 동일한 기능을 배포하는 방법으로 예를 들면 로깅 기능을 aspect 단위로 추가하는 것을 들 수 있다.