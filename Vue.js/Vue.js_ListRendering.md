## Vue 리스트 렌더링

### `v-for`와 배열

> `v-for` 디렉티브를 사용하여 배열을 리스트 렌더링 할 수 있다.  
> `v-for` 디렉티브에 `item in items` 형태의 문법을 넘겨줘야 한다.  
> `items`는 원본 데이터 배열이고, `item`은 반복되는 배열의 요소이다.

#### 기본 사용방법

```html
<div id="app">
  <ul class="todos">
    <li v-for="todo in todos">{{ todo.title }}</li>
  </ul>
</div>
```

```js
new Vue({
  el: "#app",
  data: {
    todos: [
      { title: "아침 먹기" },
      { title: "점심 먹기" },
      { title: "저녁 먹기" },
    ],
  },
});
```

위의 예제는 배열을 사용한 기본적인 리스트 렌더링 예제이다.

```html
<div id="app">
  <ul class="todos">
    <li v-for="(todo, index) in todos" :key="index">{{ todo.title }}</li>
  </ul>
</div>
```

```js
new Vue({
  el: "#app",
  data: {
    todos: [
      { title: "아침 먹기" },
      { title: "점심 먹기" },
      { title: "저녁 먹기" },
    ],
  },
});
```

위의 예제와 같이 배열의 몇번째 요소를 렌더링 하고 있는지 확인 하기 위해서는 `(item,index) in items` 문법을 사용하면 된다. 또한, `in` 대신 `of`를 사용할 수도 있다.

> 각 노드에 `key`를 지정해 주게 되면 가상 DOM은 `key`를 추적하여 `key`가 서로 매칭되는 노드를 업데이트 한다.  
> _참고 : `key`는 실제로 렌더링 되지 않는다._

### 배열 변경 감지

> Vue가 배열이 변경 되었는지 감지하여 DOM에 업데이트 하기 위해서는 배열의 메소드들을 사용해야 한다.

#### 변이 메소드

- `push()`
- `pop()`
- `shift()`
- `unshift()`
- `splice()`
- `sort()`
- `reverse()`
  > 위의 배열의 메소드를 사용할 때 Vue는 배열의 변화를 감지하여 DOM을 업데이트 할 수 있다.

#### 배열 대체

> 변이 메소드에서 이야기 한 메소드들은 원본 배열 자체를 변형한다.

- `filter()`
- `concat()`
- `slice()`
  > 반면 위의 메소드들은 원본 배열을 변형하지 않고 항상 새로운 배열을 반환한다.
