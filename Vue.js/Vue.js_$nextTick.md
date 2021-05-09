## `$nextTick`

> Vue에서 데이터와 UI를 건드려야 하는 상황에 DOM을 못 찾는 상황이 생긴다.  
> DOM이 완성되기 전에 호출을 하려고 하는 상황이기 때문이다.  
> 모든 데이터 처리가 비동기 처리되는 JavaScript의 특성 때문에 DOM이 갱신되기 전 탐색하는 상황이 나오게 된다.

```html
<div id="example">{{ message }}</div>
```

```js
var vm = new Vue({
  el: "#example",
  data: {
    message: "123",
  },
});
vm.message = "new message"; // 데이터  변경
vm.$el.textContent === "new message"; // false
Vue.nextTick(function () {
  vm.$el.textContent === "new message"; // true
});
```

> 위 코드처럼 데이터를 변경한 후 값을 비교해보면 `false` 값이 나온다.  
> `nextTick`은 DOM이 업데이트를 마칠 때까지 기다린 후 호출되기 때문에 `true` 값이 나온다.

### `$nextTick()`과 `async/await`

> `$nextTick`은 promise를 반환하므로, async/await 문법을 사용하여 똑같은 동작을 수행할 수 있다.

```js
methods: {
  updateMessage: async function () {
    this.message = '갱신됨'
    console.log(this.$el.textContent) // => '갱신 안됨'
    await this.$nextTick()
    console.log(this.$el.textContent) // => '갱신됨'
  }
}
```

### Reference

https://kr.vuejs.org/v2/guide/reactivity.html#%EB%B9%84%EB%8F%99%EA%B8%B0-%EA%B0%B1%EC%8B%A0-%ED%81%90
