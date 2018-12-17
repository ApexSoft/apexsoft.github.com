---
title : Node - MongoDB 간단 프로젝트
tags : ["Node", "MongoDB"]
---

## Node - MongoDB 간단 프로젝트

```
Mongoose는 ODM(Object Data Mapping) library이다. Java기반의 Hibernate, iBatis 등의 ORM(Object Relational Mapping)과 유사한 개념이다.

몽고디비를 로컬에 설치하지 않아도 클라우드 서비스로 개발할 수 있다.
```

1. 프로젝트부터 만들자. 프로젝트 경로 폴더를 만들고 아래와 같이 터미널에 실행하자.

   ```react
   npm init -y //기본 설정으로 프로젝트 생성
   ```

2. 모듈을 준비하자.(body-parser, express, mongoose, ejs, dotenv를 일단 추가해주자.)

   ```
   npm install body-parser express mongoose ejs dotenv
   ```

3. 디비를 만들자. 위에 설명한 것처럼 클라우드 서비스로 생성할 수 있다.

   [디비만들기1](http://dreamholic.tistory.com/98?category=773188)

   [디비만들기2](http://dreamholic.tistory.com/99?category=773188)

   ```
   GUI도구인 compass나 robomongo를 쓰면 편하게 디비에 접속, 관리할 수 있다.
   ```

4. 준비가 끝났으면 환경설정파일과 서버파일부터 만들어보자.

   환경설정 파일은 아래와 같다. URI 정보는 디비만들기1 링크를 참고한다.

   ```
   // 파일명은 없고 .env 확장자만 달아서 생성한다.
   PORT=3000
   MONGO_URI=mongodb://사용자명:비밀번호@mlab에서 생성한 주소.mlab.com:포트/디비명
   ```

   서버는 평범하게 app.js로 생성했다. 일단 이만큼이 기본이다.

   터미널에 node app.js 를 입력해서 서버를 시작해보자.(종료할 때는 컨트롤+C를 입력하고 y를 입력해준다.)

   디비연결메시지, 서버시작 메시지를 봤다면 연결테스트는 끝났다.

   ```react
   // app.js
   var express = require('express');
   var env = require('dotenv').config();
   var app = express();
   var router = express.Router();
   var mongoose = require('mongoose');
   var bodyParser = require('body-parser');
   
   app.use(bodyParser.json());
   app.use(bodyParser.urlencoded({ extended: true }));
   app.use(router);
   
   mongoose.Promise = global.Promise;
   
   // 윗부분까지는 기본설정 부분이다.
   
   // 디비 연결부분이다. 성공메시지로 연결을 확인했다.
   mongoose.connect(process.env.MONGO_URI)
       .then(() => console.log('successfully connnected to mongodb!'))
       .catch(e => console.log(e))
   
   // 서버시작
   app.listen(process.env.PORT || 3000, () => {
       console.log('server start!');
   });
   ```

5. 연결테스트까지 완료하고 준비가 끝났다면 이제 CRUD를 해보자.

   아이디와 이름을 가지는 스키마를 만들겠다.

   ```react
   // user.js
   var mongoo = require('mongoose');
   var UserSchema = new mongoo.Schema({
       userid: String,
       username: String
   });
   
   module.exports = mongoo.model('user', UserSchema);
   ```

   ```react
   // app.js의 기본설정 부분에 추가하자.
   var User = require('./user');
   ```

6. 이제 유저를 추가해보자. 유저를 추가할 수 있는 간단한 인풋이 있는 화면을 ejs로 만들어보겠다.

   views라는 폴더를 생성하고 그 안에 만들어주었다.

   ```ejs
   // ./views/main.ejs
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
       <title>Mongoose test</title>
   </head>
   
   <body>
       <form action="/add" method="POST">
           <input name="id" type="text" />
           <input name="name" type="text" />
           <input type="submit" value="send" />
       </form>
   </body>
   
   </html>
   ```

   ```
   ejs에 대해 몇 가지만 적어보겠다.
   1. html의 기본적인 문법은 같다.
   2. css코드를 별도로 분리해서 개발하고 싶다면
   	css코드를 <style></style>로 감싼 ejs파일을 생성하고
   	헤드부분에
   	<%include css파일.ejs%>
   	이렇게 추가해주자.
   	확장자가 css인 파일을 추가하는 법은 못 찾겠다. js도 마찬가지.
   3. js코드를 분리하고 싶을 때도 마찬가지다.
   	<script></script>로 감싼 ejs파일을 생성하고
   	위와 같은 방식으로 바디의 아랫부분에 추가해준다.
   ```

7. 화면을 뿌려보자.

   ```react
   // app.js 에 아래 코드를 추가하자.
   // 메인 화면을 렌더링한다.
   router.get('/', (req, res) => {
   	res.render(__dirname + '/views/main.ejs');
   });
   ```

   서버를 재시작하고 localhost:3000/ 에 들어가보자.

   텍스트 입력칸 2개와 버튼 하나가 화면에 나올 것이다.

8. 화면이 나왔으니 유저를 추가해보자.

   화면코드에서 눈치 챘겠지만 버튼을 누르거나 엔터를 치면 아이디와 이름이 디비에 추가되도록 할 것이다.

   ```react
   // app.js 에 아래 코드를 추가하자.
   // 유저를 추가한다.
   router.post('/add', (req, res) => {
       User.create({
           _id: req.body.id,
           first_name: req.body.name
       }, (err, user) => {
           if (err) return res.status(500).send('fail!');
           res.status(200).redirect('/');
       });
   });
   ```

   위에서 나오는 User가 아까 생성했던 스키마인 그 녀석이 맞다.

   body-parser를 사용했기 때문에 input에 넣은 id와 name의 값을 가져와 설정할 수 있다.

   유저를 추가하고 에러메시지가 나오는지 새로고침이 되는지 확인해보자.

9. 새로고침이 되었다면 유저가 추가된 것이다. compass, robomongo, mlab페이지 등을 통해 확인해보자.

   정상적으로 추가된 것이 확인되었다면 전체 유저 리스트를 가져와서 뿌려보자.

   ```ejs
   <!-- ./views/user.ejs -->
   <!-- 화면은 이렇게 정의한다. -->
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
   </head>
   
   <body>
       <table>
           <th>id</th>
           <th>name</th>
           <% for(var i=0; i < users.length; i++) { %>
               <tr>
                   <td>
                       <%= users[i].userid %>
                   </td>
                   <td>
                       <%= users[i].username %>
                   </td>
               </tr>
               <% } %>
       </table>
   </body>
   
   </html>
   ```

   ```react
   // app.js 에 아래 코드를 추가하자.
   router.get('/getuser', (req, res) => {
       User.find((err, users) => {
           if (err)
               return res.status(500).send('fail!');
           res.status(200).render(__dirname + '/views/user.ejs', { users: users });
       });
   });
   ```

   서버를 재시작하고 localhost:3000/getuser 에 들어가보자.

   main.ejs 화면을 통해 추가한 목록이 잘 나오면 성공이다.

10. 메인화면에 유저목록을 함께 출력하고 유저가 추가되면 업데이트되도록 바꿨다.

   main.ejs에서 목록을 추가할 부분에 아까 ejs 설명에 적은 것 처럼

   ```ejs
   <%include user.ejs%>
   ```

   위의 코드를 추가해주면 된다.

   나는 폼태그의 바로 아래에 추가했다.

   ```ejs
   <body>
       <div id="root"></div>
       <form action="/add" method="POST">
           <input name="id" type="text" />
           <input name="name" type="text" />
           <input type="submit" value="send" />
       </form>
   
       <%include user.ejs%>
   </body>
   ```

   이렇게 되는 것이다.

   그러면 이제 유저목록과 함께 메인화면이 나오게 된다.

   메인화면을 출력하는 서버코드도 살짝 변경하였다.

   ```react
   // app.js
   router.get('/', (req, res) => {
       User.find((err, users) => {
           if (err)
               return res.status(500).send('fail!');
           res.status(200).render(__dirname + '/views/main.ejs', { users: users });
       });
   });
   ```

   서버를 재시작해서 확인해보자.

11. 한명의 유저를 조회해보자.

    ```react
    // app.js에 아래 코드를 추가하자.
    // 유저 조회
    router.get('/:id', (req, res) => {
        User.findById(req.params.id, (err, user) => {
            if (err)
                return res.status(500).send('조회 실패');
            if (!user)
                return res.status(404).send('유저 없음');
            res.status(200).send(user);
        });
    });
    ```

    서버를 재시작하고 아래와 같이 입력하면 한명의 유저 정보가 출력된다.

    오브젝트아이디는 디비에서 직접 확인해서 붙여넣는다.

    ```
    localhost:3000/오브젝트아이디
    ```

12. 삭제와 수정은 아래의 코드를 참고하면 된다.

    ```react
    // User 삭제
    router.get('/del/:id', (req, res) => {
        User.findByIdAndRemove(req.params.id, (err, user) => {
            if (err)
                return res.status(500).send('del fail');
            res.status(200).redirect('/');
        });
    });
    
    // User 수정
    router.post('/update/:id', (req, res) => {
        User.findByIdAndUpdate(req.params.id, req.body, { new: true }, (err, user) => {
            if (err)
                return res.status(500).send('update fail');
            res.status(200).redirect('/');
        });
    });
    ```

    수정을 위한 화면과 삭제버튼은 만들어서 사용해보자.

