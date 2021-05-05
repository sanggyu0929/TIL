## `$emit()`

> `$emit()`은 다른 컴포넌트에게 이벤트를 전달하기 위해 사용할 수 있다.  
> 자식 컴포넌트에서 사용자 지정 이벤트를 만들어 부모 컴포넌트에게 전달할 수 있다.

```js
// 하위 컴포넌트
this.$emit("이벤트 명");
```

```html
<!-- 상위 컴포넌트 템플릿 -->
<div id="app">
  <child-component
    v-on:이벤트
    명="상위 컴포넌트의 싱핼할 메서드 명 또는 연산"
  ></child-component>
</div>
```

### 예시

```html
<div id="app">
  <my-comp :my-msg="message" @my-event="updateMessage"></my-comp>
</div>
```

```js
Vue.component("my-comp", {
  template: '<div @click="updateMsg">{{ myMsg }}</div>',
  props: {
    myMsg: String,
  },
  methods: {
    updateMsg() {
      this.$emit("my-event", "Good");
    },
  },
});

const vm = new Vue({
  el: "#app",
  data() {
    return {
      message: "Hello",
    };
  },
  methods: {
    updateMessage(value) {
      this.message = value;
    },
  },
});
```

> 위 코드는 하위 컴포넌트인 `my-comp`에서 `updateMsg()` 메서드가 실행되면 `my-event`라는 이벤트가 발생되고, 상위 컴포넌트의 `v-on` 디렉티브로 이벤트를 받아 `updateMessage()` 메서드를 실행한다.  
> 실행 결과 부모에 있는 `message` 데이터는 `"Hello"`에서 `"Good"`으로 바뀐다.
