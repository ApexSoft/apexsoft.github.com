---
title : 블로그 만들기
tags: ["hexo", "github"] 
---



# Github page와 Hexo 이용, 기술 블로그 만들기



## Git Page

### 1. Github Repository 생성

* https://github.com/
* New Repository, Repository 이름은 **USERNAME.github.io**
* USERNAME 은 Github의 가입시에 사용자의 **username**을 입력한다
* Public / Private 중 Public 선택
* Create Repository 버튼을 통해 Repository 생성
* 확인 -  [https://USERNAME.github.io](https://username.github.io/)




## Hexo

> Hexo는 Jekyll와 함께 대표적으로 정적 페이지를 쉽게 만들 수 있도록 도와주는 서비스이다.
> Hexo의 경우에는 npm을 통해 쉽게 설치가 가능하고 한 줄의 Command Line을 통해 Github에 바로 배포 
> 다양한 플러그인과 테마를 지원하고 있다





### 1. 다운로드

- Node.js
- Git

### 2. 설치

* Hexo

  ```bash node.js
  $ npm install -g hexo -cli
  ```

* git 

  ```bash node.js
  $ npm install hexo-deployer-git --save
  ```



### 3. 블로그 생성

```bash bash 
$ hexo init [폴더명]
$ cd [폴더명]
$ npm install
```



### 4. 설정파일 ( _config.yml ) 수정

> root 디렉토리에 `_config.yml`  파일로, 블로그에 대한 설정 한다 
>
> 문서 - <https://hexo.io/docs/>



#### 기본 설정

* site 정보

  ```bash _config.yml
  title: apexsoft 기술블로그 
  subtitle: 우리모두 master
  description:
  author: Hyosook Kim
  ```

  ​

* URL 정보

  ```bash _config.yml
  url: http://apexsoft.github.io/
  root: /
  permalink: :year/:month/:day/:title/
  permalink_defaults:
  ```

  ​

* Github 정보

  ```bash _config.yml
  deploy:
    type: git
    repo : https://github.com/ApexSoft/apexsoft.github.com.git
    branch : master 
  ```



#### 테마 적용

* 테마 선택 - <https://hexo.io/themes/> 


* git clone

  ```bash bash
  # hexo [폴더/themes]에  다운
  $ git clone https://github.com/ppoffice/hexo-theme-hueman.git themes/hueman
  ```

* _config.yml`  theme 수정

  ```bash
  # Extensions
  ## Plugins: http://hexo.io/plugins/
  ## Themes: http://hexo.io/themes/
  theme: hueman #폴더명과 매칭되어야한다
  ```

* 검색 기능 ([Insight earch](https://github.com/ppoffice/hexo-theme-hueman/wiki/Search#insight-search))를 이용하기 위해서는 `hexo-generator-json-content`를 설치

  ```bash bash
  npm install -S hexo-generator-json-content
  ```

* 테마 폴더 안에 있는 `_config.yml.example`의 이름을`_config.yml`로 수정

* clean

  ```bash bash
  $ hexo clean
  ```

  ​

* http://futurecreator.github.io/2016/06/14/hexo-apply-hueman-theme/

### 5. 포스트 작성

* 새 포스트 만들기

  ```bash bash
  $ hexo new post [post_name]
  ```

  or

  ```bash
  ㄴ source
     ㄴ _posts
            - ##여기에 .md파일 넣기
  ```

* 포스트 제목 및 수정

  ```bash
  ---
  title: "블로그 만들기 "       			     #post 제목
  date: 2017-07-07 00:23:23                     #post 생성 날짜
  tags: ["hexo", "clean-blog", "theme"]         #tags
  cover: /assets/contact-bg.jpg                 #post 커버 이미지
  subtitle: "첫 블로그입니다."        			#post 부제
  ---
  ```

  ​

### 6. 로컬에서 test

```bash bash
$ hexo server
```

- [http://localhost:4000](http://localhost:4000/)



### 7. Github Page Repository에 배포

* 정적 리소스 생성

  ```bash bash
  $ hexo generate
  ```

* 배포

  ```bash bash
  $ hexo deploy
  ```

* 생성 + 배포 한번에

  ```bash bash
  $ hexo deploy --generate
  ```

* 확인 

  <http://apexsoft.github.io/>

  https://github.com/ApexSoft/apexsoft.github.com.git  -master branch 

  ​

### 8. 소스관리

* `master` :  블로그 (html) 파일 , hexo를 통해서  deploy 된 소스
* `soucre` :  hexo 원본 파일들.



### 9. 사용

* `git clone`    > `source` branch  > https://github.com/ApexSoft/apexsoft.github.com.git 
* `.md`  파일 올리기
* `git push ` > `source` branch  > https://github.com/ApexSoft/apexsoft.github.com.git 
* `deploy` 



### 10. 기타

* 테마가 적용 안되는 경우

  ```bash bash
  $ hexo clean
  ```

  * 테마 안에 있는 git 삭제

  ```bash bash
  $ rm -rf .git
  ```


* 배포가 되지 않는 경우 해볼 것들

  * git을 못 찾는다면 `hexo-deployer-git` 설치

  ```bash bash
  $ npm install hexo-deployer-git --save
  ```
  * github 관련 에러 경우

    > http://maxisam.github.io/2016/09/02/Hexo-got-error-on-deploying-to-github/ 블로그 참고

    1) Git Credential Manager for Windows 설치 

    https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases

    2) git bash에서 명령어 실행

    ```bash bash
    $ git config --global credential.helper wincred
    ```

    3) 자격증명 삭제

    제어판 > 사용자계정 > 자격증명 관리자 > windows 자격 증명 > 일반 자격 증명 에서 `github.com` 자격증명을 제거

    `deploy` 혹은 `push`를 할때, 다시 ID&PW를 입력해야 한다.

