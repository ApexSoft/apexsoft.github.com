---
title : vuex 상용
tags : ["vuex ","저장소", "vue.js"]
---





# vuex

> 상태관리 패턴  + 라이브러리
>
> 모든 컴포넌트에 대한 중앙 집중식 저장소 역롹 

## 상태관리 패턴 

* 상태 :  data
* 뷰 : template
* 액션 :  매소드 ( 뷰에서 사용자의 입력에 따라서 상태를 변경 )





## 사용

스토어를 외부에서 사용하려면, 모듈로 export 를 해준다
엔트리 포인트에서 , main.js 에서

스토어를 가져온다 (importfh)

루트 인스턴스 에서 , 스토어 객체를 넘겨준다

어플리케이션에서 vuex객체를 사용할수 있다





## 상태 State

* 
* state 값 자겨오기 

this.$sotre.state.isAddBorad



### mapState 헬퍼

* 배열 형태 사용 ( 매핑 된 계산된 속성의 이름이 상태 하위 트리 이름과 같을 때 문자열 배열을 `mapState`에 전달할 수 있습니다.) 

  ```js
  const Counter = {
    template: `<div>{{ count }}</div>`,
    computed: {
      count () {
        return this.$store.state.count
      }
    }
  }
  ```

  ```js
  import {mapState} from 'vuex'    ///vuex에서 mapState 가져오기
  computed: mapState([
    // this.count를 store.state.count에 매핑 합니다.
    'count'
  ])
  ```

  ```js
  import {mapState} from 'vuex'    ///vuex에서 mapState 가져오기
  computed:{
  ...mapState(['count'])
  }
  ```






## 변이 mudations 

> 저장소의 실제로 상태를 변경하는 유일한 방법 
>
> 무조건 동기적 이여야 한다  >> 대부분 상태 변경
>
> 비동기 (axios) 같은 경우 , action에서 



```js
const store = new Vuex.Store({
  state: {
    count: 1
  },
  mutations: {
    increment (state) {
      // 상태 변이
      state.count++
    }
  }
})
```

```js
store.commit('increment')
```



* 정의  mudations 
* 실행 > store에 commit함수  

## mapMutations 헬퍼

```js
import { mapMutations } from 'vuex'

export default {
  // ...
  methods: {
    ...mapMutations([
      'increment' // this.increment()를 this.$store.commit('increment')에 매핑합니다.
    ]),
    ...mapMutations({
      add: 'increment' // this.add()를 this.$store.commit('increment')에 매핑합니다.
    })
  }
}
```




