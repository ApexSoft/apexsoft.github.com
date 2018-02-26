# apexsoft.github.com
apexsoft 기술블로그 글 작성에 관한 개요입니다.  자세한 내용을 사이트 글 을 참고 해주세요



## 브런치 설명 



### source

* 기본 브런치

* 원본 파일 관리 (`.md`원본 문서 관리)

  `push`를 톻해서 직접 관리한다

### master

* `hexo deploy`를 통해 올라온 파일

  직접 push 하지 않는다



## 사용

1. clone

   `git clone  https://github.com/ApexSoft/apexsoft.github.com.git`

   ​

2. 문서 작성 (.md 파일 헤더부분)

   ```bash 
   ---
   title : 
   tags : ["name"]
   ---
   ```

3. `source / source/_post/`에 공유할 `.md`파일 넣기

   ​

4. `hexo deploy --generate`

   ​

5. `git commit & push` `origin/source`





