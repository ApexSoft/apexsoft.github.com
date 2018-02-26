---
title : Drag and drop
tags: ["vue.js","component"] 
---

## Drag and drop

### Sortable

https://github.com/RubaXa/Sortable

##### Sortable을 vue component로 만든 Draggable

##### https://github.com/SortableJS/Vue.Draggable



### Draggable 

> 직접 구현한 예제 https://codepen.io/anon/pen/dzvzGy?editors=1010



```html html
<head>
  <!-- CDNJS :: Sortable (https://cdnjs.com/) -->
  <script src="//cdnjs.cloudflare.com/ajax/libs/Sortable/1.6.0/Sortable.min.js"></script>

  <!-- CDNJS :: Vue.Draggable (https://cdnjs.com/) -->
  <script src="//cdnjs.cloudflare.com/ajax/libs/Vue.Draggable/2.14.1/vuedraggable.min.js"></script>
</head>
<body>
	<draggable v-model="list2" class="dragArea" :options="secondOption">
		<div v-for="(element, index) in list2" :key="index">{{element.name}}
          <button @click="remove(index)">remove</button>
        </div>
    </draggable>
</body>
```



```javascript vue.js
...
data: {
  firstOption: {
      group: {
        name: 'people',
        pull: 'clone',
        put: false
      },
      sort: false
    },
    secondOption: {
      group: 'people'
    }
}
...
```



#### `option` 속성

| 속성명  | 자세한 속성           | 내용                                      |
| ---- | ---------------- | --------------------------------------- |
| pull | false            | 선택하여 이동하는 드래그앤드롭 안됨                     |
|      | true             | 선택한 객체를 드래그앤드롭으로 이동                     |
|      | clone            | 선택한 객체가 복사되어 드래그앤드롭 가능                  |
| put  | false            | 드래그로 들어온 객체를 현재 목록에 드롭시키지 못함            |
|      | true             | 드래그로 들어온 객체를 현재 목록에 드롭시킬 수 있음           |
|      | array [foo, boo] |                                         |
| sort | true             | 현재 선택한 객체를 현재 리스트 안에서 드래그앤드롭으로 정렬할 수 있음 |
|      | false            | 현재 선택한 객체를 현재 리스트 안에서 드래그앤드롭으로 정렬할 수 없음 |