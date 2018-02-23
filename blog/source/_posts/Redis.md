---
title : REDIS
tags : ["apexsoft","DB"]
---



# REDIS (REmote DIctionary Server)



## key/Value Store

* in memory key value database

* key/value 저장소

  * 특정 키 값에 값을 저장하는 구조

* 메모리에 데이터를 저장

  * 빠른 read /write 속도

  * 전체적인 저장 가능한 데이터의 용량은 물리적인 용량을 넘을수 없음

  * RDB나 NoSQL이 기본적으로 file system에 데이터 저장

    ​

### 유용 사례

- 최신 랭킹이 필요한 경우

  - 많은 데이터 필요 x , 빠른 처리만 필요

- 최신 데이터 간의 비교, 차이계산 경우

  - 최근에 이직 신청을 한 다음 직원은?

  ​

### 저장 구조

* in-mamory + hard disk
  * 빠른데 + 복구도 가능
*  Pub/Sub Model
  * 분산 처리
* Replication Topology(Master-Slave <- Query Off Loading, Sharding)
  * read/write 성능 향상

    ​

### 저장 형태

* 다양한 data set 제공

  * 다양한 집합set 연산 가능 -> 데이터 저장

* 키 값에 다양한 데이터 타입을 매핑 시킬수 있음
* 다양한 테이터 타입을 지원
  - 복잡한 구조를 저장 가능
    ​

### 관리 정책

#### Persistence(지속성)

* disk에 저장 가능, shutdown 후에도 데이터 보존 가능

  > 서버가 shutdown된 후 restart되더라도, disk에 저장해놓은 데이타를 다시 읽어서 메모리에 Loading

* 데이터 저장 방식

  * RDB[snapshotting]
    * 순간적으로 메모리에 있는 내용을 DISK에 전체를 옮겨 담는 방식
  * AOF[Append On File]
    * 모든 write/update 연산 자체를 모두 log 파일에 기록하는 형태이다

#### Expiation

* 데이터 유효기간 설정 가능 (데이터 생명주기를 정해서 일정 시간이 지나면 자동으로 삭제 되게 한다)

* 내부 정책 

  * Active

    * 데이터 접근할 때 유효기간 체크

  * passive

    * 주기적으로 키를 100개 랜덤 뽑아 체크

    * 랜덤이라 체크 안된 garbage 잔존가능

      >  expired time이 지난 후 클라이언트에 의해서 접근 되지 않은 데이타는 Active 방식으로 인해서 지워지지 않고 Passive 방식으로 지워져야 하는데, 이 경우 Passive 방식의 경우 전체 데이타를 scan하는 것이 아니기 때문에

  ​



