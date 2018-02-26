---
title : @RequestBody
tags : ["apexsoft","java","springboot"]
---



## Get

* URL에 데이터를 담아 전송하며 1차원 데이터밖에 담지 못한다(2차원 배열, 객체속 객체 등등은 불가능하다.) 
* 따라서 검색조건 수준의 데이터를 담는게 옳바르다

## Post

* POST 방식은 Request 의 Body에 데이터를 담는데 이 경우 JSON, 다차원 데이터를 담을 수 있다. 객체속 JSON 리스트라던지 여러가지 데이터가 가능하다. 



# @RequestBody

## @RequestBody를 사용할 경우, 반드시 POST 방식



### 사용하지 않는 경우

* query parameter, form data를 object에 맵핑한다.

```
키1=데이터1&키2=데이터2
```



### @RequestBody 사용 하는 경우

*  body에 있는 data를 HttpMessageConverter를 이용해 선언한 object에 맵핑한다.


* body영역의 모양을 json과 같이 converter가 변환할 수 있는 형태로 전달해야하며 다음과 같은 모양이다. 

```json
{ "키1" : "데이터1", "키2" : "데이터2" }`
```





## 여러 타입의 객체 사용



### 1.

* 보내기

```js
 axios.post(this.memberView + '/checked', {
                user: {userId: checkedId},
                project: {projectCode: this.projectCode}
            })
```



* 받기

```java
@ResponseBody
@PostMapping("/checked")
public  boolean  checked(@RequestBody Member1 member1) {
List<Member1> list=member1Repository.findByUser_UserIdAndProject_ProjectCode(
  member1.getUser().getUserId(), member1.getProject().getProjectCode());
 return list.isEmpty();
    }
```



### 2.

* 보내기

```js
 axios.post(this.memberView + '/checked', {
                userId: checkedId,
                projectCode: this.projectCode
            })
```



* 받기

```java
@ResponseBody
@PostMapping("/checked")
public  boolean  checked(@RequestBody Map<String,String>map) {
List<Member1> list=member1Repository.findByUser_UserIdAndProject_ProjectCode(
  map.get("userId"), map.get("projectCode"));
return list.isEmpty();
    }
```

