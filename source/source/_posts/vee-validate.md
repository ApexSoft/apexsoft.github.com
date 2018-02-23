---
title : vee-validate
tags : ["vue.js","component","apexsoft"]
---



## 몇가지 사전 체크사항

### &lt;label&gt;, &lt;input&gt; and `id`, `name` attribute

- `<label for="">`의 대상은 `input`의 `id`
- VeeValidate에서 validation 대상은 `input`의 `name`으로 `errors.has('name')`와 같이 사용
- 그러므로 `input`은 `id`, `name`을 모두 명시해 주는 것이 좋음

### Migrating to Bootstrap 4

#### Form Group

`label`과 `input`을 한 줄에 배치하려면 class에 `"row"`를 추가

#### Label

`control-label`은 더이상 사용 불가능하며 오른쪽 정렬도 해주지 않음

`col-form-label`을 사용하고 정렬은 `text-*`를 사용

```html html
<label for="username" class="col-form-label text-right">아이디</label>
```

#### Input

`form-control`을 필히 명시

validation에 대한 bootstrap 클래스는 `is-invalid | is-valid`

```html html
<input id="username" class="form-control is-invalid">  <!--invalid인 경우-->
```



# vee-validate

vue에서 validation 수행을 도와준다. 

공식사이트 : http://vee-validate.logaretm.com/

## 사용방법

### html

```html html
<!-- 기본 vue.js -->
<script src="https://unpkg.com/vue"></script>
<!--vee validate-->
<script src="https://unpkg.com/vee-validate@2.0.0-rc.13"></script>
<script>
        Vue.use(VeeValidate);
</script>
```

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
* 아이콘을 input과 함께 표시해주기 위해 `div`에 `has-icon` 클래스를 추가
* 해당 클래스에 대한 스타일은 vee-validate 예제 페이지를 참조하여 `apex-web-base.css`에 추가



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



### 경고 메시지 커스텀

Vue 생성시 Dictionary를 변경

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
