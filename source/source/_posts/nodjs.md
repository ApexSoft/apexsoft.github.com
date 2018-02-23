---
title : node.js? npm? cdn? 사용하기
tags : ["apexsoft","node.js","npm"]
---





## javascript 사용

#### 1. CDN

* https://unpkg.com/#/   OR https://www.npmjs.com/
* `dist` 폴더 , `다른이름으로 링크주소 복사`
* `<script > 주소  </script>`



#### 2.npm

* git 다운
* `npm run bundle` or `yarn bundle`
* `dist`  폴더  , 생성된 물리적 파일
* 원하는 프로젝트에 옮기기



## webpack ?

> - 모듈 번들러 
> - 의존성을 가진 모듈들을 다루고 , 그 모듈로부터 정적인 asset을 생성
> - 작동 방법 
>   - 하나의 파일을 진입점으로 지정
>   - 진입점 파일은 트리의 루트가 된다  
>   - `require`에 의해 다른 파일이 트리에 추가 된다 = require으로 명시된 의존성들을 해석하며 의존성 트리를 그린다
>   - webpack명령을 실행하면  , 모든 파일과 모듈은 하나의 파일에 번들로 제공된다



#### 모듈 번들링

> 모듈간의 의존성을 해석하고 , 그걸 바탕으로 정적 에셋을 만드는 과정

#### 모듈 번들러

> * 모듈 번들링을 하는 친구
> * ex ) webpack
> * 거대한 파일들을 여러 파일로 나눠 쓸수있게 해준다.

​

## webpack-dev-server

* 메모리에 bundle 파일을 올려 놓고 변경이 있을때 마다 , live reload를 시킨다
* **webPack.dev.config.js**

- `webpack-dev-server`가 사용할 환경설정에 대해 정의

- `devServer`

  - `host`  : localhost

    - 모든 ip를 사용하는 경우 `0.0.0.0`사용 

  - `port` : 8080

    -   접속 포트 설정

  - `proxy`  : {'**' :"http://localhost:8001"}

    -  프록시 설정 , Springboot 실행되는 url 

    - ```javascript
      axios
            .get(`http://localhost:8001/tester/api/proto/ans/ask/${this.askNo}`)
            .then((res) => {
              }
            });
      ```

    - ​

      ```javascript
        axios
        .get(`/tester/api/proto/ans/ask/${this.askNo}`)
        .then((res) => {
          }
        });
      ```

- 실행

  ```bash bash
  #package.json에 정의된 모듈 설치(node_modules에 다운로드)

  npm install

  #webpack -dev-server 구동
  npm run dev
  ```

  - `npm run`명령 뒤의 스크립트 명(`dev`)는 `pakage.json`에 정의 되어있다



## package.json

- npm 설정을 관리
- 이를 통해 모든 부품이 설치되어 돌아갈 수 있습니다.

### devDependencies

- **lint**
  - 코딩 룰에 위배되는거 체크 해준다
- **pug**
- **babel**
  - Babel은 **Transform Compiler**이다. 
  - 보통 TypeScript, CoffeeScript 같은 Javascript 문법이 아닌 각각의 문법으로 작성된 코드를 Javascript 엔진에서 동작 가능한 코드로 변환하는 역할
  - ES6 -> ES5 transpiler
- **loader**
  - 일종의 함수
  - 마지막 로더는 최종적으로 적절하게 변형된 모듈을 번들 자바스크립트 파일에 넣어주게 된다
  - ex) css 파일 require 하는 경우
    - css 파일을 그대로 자바스크립트에 넣을수 없으니 , 
    - 원래의 css파일과 같은 역활을 할 수 있는 자바스크립트 형태의 무언가를 만들어야 최종 번들에 해당 내용을 포함시킬수 있다. 
    - 이 과정을 일련의 로더 파이프라인이 수행 



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

  * **enty** - 번들의 엔트리 포인트 . webpack은 여러 번들을 생성하는 진입점을 허용하기 때문에 배열이다

  * **output** - webpack의 최종 결과물이 되는 형태를 명시

    * path -  어디에 번들 파일을 위치 시킬 것인지를 지정 ( 빌드 결과물 들어갈 `webpack.config.js`로 부터의 상태 경로 )

    * publicPath -  웹사이트에서 해당 에셋에 접근하기 위해 필요한 경로 

    * filename  

      > * 각 번들 파일의 이름을 지정
      > * `[name]` : `entry`에서의 key 값

  * **Loader** - Loader는 사전에 처리할 작업을 나타내며 css, html, jpg, scss 등의 자산을 하나의 모듈로 취급하며 이러한 파일들을 종속성 그래프에 추가할 때 모듈로 변환한다.

  * **Plug-In** - Plug-In은 일반적인 Compile 또는 모듈 처리에 필요한 작업 및 사용자 정의 기능을 수행하는데 사용한다.

- webpack 명령을 실행하면 , bundles라는 폴더에 `draggabletest.js` `vuejs-test2`파일을 생성한다

- webpack은 `require` 하고있는  파일들 모두 묶어 하나의  번들을 내놓게 된다




## node-moules

- npm이 pakage들을 설치하는 디렉토리 폴더




# 사용

### 설치

- node.js 설치 
  - https://nodejs.org/en/download/current/
- yarn 설치
  - `npm install -g yarn`
    - `-g`는 글로벌 옵션
- Plugins 설치 (선택)
  - vue.js
  - pug

### 실행

* package.json에 정의된 모듈 설치
  * `npm install`
  * 주입 후 빌드  refresh

* webpack -dev-server 구동

  * `npm run dev` 

* springboot  서버 실행

  * 시큐리티 설정에 걸리는 경우 ,  해당 url `.permitAll()` 하기

  ​

### 옮기기

- `npm run bundle`
  - dist 밑에 생기는 파일 복사해서 붙여 넣는다

# 기타

### lint

* 코딩룰 체크 

- 설치
  - yarn 설치 `npm install -g yarn`
  - lint 설치 `npm install -g eslint`
  - pakage.json >> devDependencies >> 추가 
- 사용
  - rule 확인 + fix `yarn lint --fix`
- .eslintrc.js
  - rule 정의







