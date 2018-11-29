---
title : vee-validate
tags : ["vue.js","component"]
---



## vee-validate

vue에서 validation 수행을 도와준다. 

[공식사이트](http://vee-validate.logaretm.com/) 

## 사용방법

HTML, NPM 방식 두가지 있음

[공식사이트 - Get started](https://baianat.github.io/vee-validate/guide/getting-started.html#installation) 

#### 기본 validate 설정

```html html
<input v-validate="'required|email'" 
       :class="{'input': true, 'is-danger': errors.has('email') }" 
       name="email" type="text" placeholder="Email">
```

#### 에러메세지 출력 

```html html
<div class="has-icon has-icon-right">
	<i v-show="errors.has('email')" class="fa fa-warning"></i>
	<span v-show="errors.has('email')" 
          class="invalid-feedback">{{ errors.first('email') }}</span>
</div>
```

* `fa`, `fa-warning`으로 아이콘 출력 가능 ([icons 참조](http://fontawesome.io/icons/))



### 속성

#### v-validate

* `v-validate` 속성에 rule 을 지정

* 여러가지 rule 입력 가능

  ```html html
  <input v-validate="'required|min:6|max:16'"> 					// 1
  <input v-validate="{ rules: { required: true, min:6, max:16}}">	// 2
  ```

  **`1`방법에서 rule을 여러개 입력하는 경우, 반드시 큰 따옴표 안에 작은 따옴표로 감싸준다.**

* 주요 v-validate 값 예제 : https://jsbin.com/siqodemose/4/edit?html,js,output

  ​					(이메일, 비밀번호(대,소문자,특수문자), 전화번호, 웹사이트)

#### name

* 필수 속성
* id 처럼 쓰이는 유니크한 속성

#### data-vv-as

* error 메시지 출력할 때 나오는 필드명 (다국어 처리가 필요하면, 다국어 처리된 데이터를 바인딩 해야 함)

#### v-bind:class

* class를 동적 바인딩

* `errors.has('field')`로 해당 필드에 에러가 있는지 판단

  ```html html
  <input v-validate="'required|email'" 
         :class="{'form-control': true, 'is-invalid': errors.has('userId')}"
  ```

  > Rendering Errors : `errors`를 통해 에러가 있는지, 어떤 에러인지 알아 볼 수 있다.
  >
  > - `has('field')`: 해당 필드에 에러가 있는지
  > - `first('field')`: 해당 필드의 첫번째 에러 메시지 가져오기
  > - `all()`: 해당 필드의 모든 에러 메시지 가져오기
  > - `collect('field')`:
  > - `any()`:


### 경고 메시지

#### 다국어

validate/index.js

```javascript javascript
import Vue from 'vue'
import VeeValidate from 'vee-validate'
import validationKoMessages from 'vee-validate/dist/locale/ko.js'

const validate = {
    locale: Vue.i18n.locale(),
    dictionary: {
        ko: validationKoMessages
    }
}
```

기본으로 영문 경고메시지를 띄운다. `vee-validate`에서 제공하는 다른 언어 경고메시지가 있으니, 필요한 것을  import 하여 사용한다. (설치된 패키지에 포함되어 있음)

#### 커스텀

Dictionary를 변경

제공되는 다국어 메시지 외에 사용자정의 validate 에 대한 메시지나 다른 문구를 넣고싶은 경우에 사용한다.

```javascript vue.js
created() {
  let dict = {
    en: {
      custom: {
        userId: {
          required: () => 'User ID is empty.',
          email: () => 'User ID must be email.'
        }
      }
    },
    ko: {
      custom: {
        userId: {
          required: () => '아이디가 비어 있습니다.',
          email: () => '아이디는 email 형태여야 합니다.'
        }
      }
    }
  }
  this.$validator.setLocale('ko');
  this.$validator.updateDictionary(dict);
}
```

### 저장버튼에 validate 

```javascript javascript 
this.$validator.validateAll().then((result) => {
        if (result) {
          alert('From Submitted!');
        } else {
          alert('Correct them errors!');
        }
      });
```

