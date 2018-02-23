---
title : webpack
tags: ["node.js", "npm", "apexsoft"] 
---



# 모듈화

## 1.스코프 (Scope)

- 모든 모듈은 자신만의 독립적인 실행 영역이 있어야 한다
- 전역변수와 지역변수를 분리하는 것이 중요

## 2.  정의 

- `exports` 객체 이용

## 3. 사용

- 모듈 사용은 `require` 함수 사용





# webpack

* 모듈 번들러 

* 의존성을 가진 모듈들을 다루고 , 그 모듈로부터 정적인 asset을 생성

* 하나의 파일로 js파일을 번들할수있다

* 작동 방법 

  > * 하나의 파일을 진입점으로 지정
  > * 진입점 파일은 트리의 루트가 된다  
  > * `require`에 의해 다른 파일이 트리에 추가 된다 = require으로 명시된 의존성들을 해석하며 의존성 트리를 그린다
  > * webpack명령을 실행하면  , 모든 파일과 모듈은 하나의 파일에 번들로 제공된다




### 로더

* 일종의 함수
* 마지막 로더는 최종적으로 적절하게 변형된 모듈을 번들 자바스크립트 파일에 넣어주게 된다
* ex) css 파일 require 하는 경우
  * css 파일을 그대로 자바스크립트에 넣을수 없으니 , 
  * 원래의 css파일과 같은 역활을 할 수 있는 자바스크립트 형태의 무언가를 만들어야 최종 번들에 해당 내용을 포함시킬수 있다. 
  * 이 과정을 일련의 로더 파이프라인이 수행 

### 모듈 번들링

- 모듈간의 의존성을 해석하고 , 그걸 바탕으로 정적 에셋을 만드는 과정

### 모듈 번들러

- 모듈 번들링을 하는 친구

- ex ) webpack

- 거대한 파일들을 여러 파일로 나눠 쓸수있게 해준다.

  ​

  ​


## webpack.config.js

- webpack을 설정한다

  ```javascript
  var path = require('path')

  module.exports = {
   entry: {
          'vuejs-test2': path.join(__dirname, '/src/vuejs-test2.js'),
          'draggabletest': path.join(__dirname, '/src/draggabletest.js')
      },
    output: {
      path: path.join(__dirname, '../src/main/resources/static/js/bundles'),
      publicPath: '/js/bundles',
      filename: '[name].js'
    }
  }
  ```

  * enty - 번들의 엔트리 포인트 . webpack은 여러 번들을 생성하는 진입점을 허용하기 때문에 배열이다

  * output - webpack의 최종 결과물이 되는 형태를 명시

    * path -  어디에 번들 파일을 위치 시킬 것인지를 지정 ( 빌드 결과물 들어갈 `webpack.config.js`로 부터의 상태 경로 )

    * publicPath -  웹사이트에서 해당 에셋에 접근하기 위해 필요한 경로 

    * filename  

      > * 각 번들 파일의 이름을 지정
      > * `[name]` : `entry`에서의 key 값

- webpack 명령을 실행하면 , bundles라는 폴더에 `draggabletest.js` `vuejs-test2`파일을 생성한다

- webpack은 `require` 하고있는  파일들 모두 묶어 하나의  번들을 내놓게 된다


### webpack 로더

- `require`를 이용하여 , `.css`  와 `.html` `.png`등을 불러올수있다

  ​

## package.json

- npm 설정을 관리
- 이를 통해 모든 부품이 설치되어 돌아갈 수 있습니다.

## node-moules

- npm이 pakage들을 설치하는 디렉토리 폴더






###  

# 모듈화

## 1.스코프 (Scope)

* 모든 모듈은 자신만의 독립적인 실행 영역이 있어야 한다
* 전역변수와 지역변수를 분리하는 것이 중요

## 2.  정의 

* `exports` 객체 이용

## 3. 사용 

* 모듈 사용은 `require` 함수 사용

