## Props

> 모든 컴포넌트 인스턴스에는 각자의 자체 격리된 범위(scope)가 있다.  
> 하위 컴포넌트의 템플릿에서는 상위 데이터를 직접 참조할 수 없는데, `props`를 사용하면 하위 컴포넌트로 데이터를 전달할 수 있다.

#### 하위 컴포넌트에서는 `props` 옵션을 사용해 수신할 것으로 기대되는 `props`를 명시적으로 선언해야 한다.

```js
Vue.component("my-comp", {
  template: "<div>{{ msg }}</div>",
  props: ["msg"],
});
```

```html
<div id="app">
  <my-comp msg="Hello"></my-comp>
</div>
```

> 위처럼 상위 컴포넌트에서 `msg`에 담은 데이터를 하위 컴포넌트의 `msg`로 보내줄 수 있다.  
> 하지만 이 방식은 동적 바인딩은 아니라서, 상위 컴포넌트의 데이터가 변해도 하위 컴포넌트에 반영 되지 않는다.

### 동적 Props

> `v-bind`를 사용하면 부모의 데이터를 동적으로 바인딩해 자식에게 전달할 수 있다.

```html
<div id="app">
  <div>
    <input v-model="parentMsg" />
    <br />
    <child :my-message="parentMsg"></child>
  </div>
</div>
```

```js
Vue.component("child", {
  template: "<div>{{ myMessage }}</div>",
  props: ["myMessage"],
});

const vm = new Vue({
  el: "#app",
  data() {
    return {
      parentMsg: "",
    };
  },
});
```

### 리터럴 VS 동적

```html
<comp some-prop="1"></comp>
```

> 위의 리터럴 방식은 실제 숫자가 아닌 문자열 `"1"`로 데이터를 전달한다.  
> 실제 숫자를 전달하기 위해서는 `v-bind`를 사용하면 된다.

```html
<comp :some-prop="1"></comp>
```

### Props 검증

> 하위 컴포넌트가 상위 컴포넌트로부터 받는 `props`에 대한 요구사항을 지정할 수 있다.

```js
Vue.component("my-comp", {
  props: {
    msg1: {
      type: String, // 기본 타입은 문자열 타입이다.
      default: "Default!",
    },
    msg2: {
      type: [String, Number], // 기본 타입은 문자열이나 숫자 타입이다.
      default: "Default!",
    },
    msg3: {
      type: Object, // 기본 타입은 객체 배열이다.
      default: "Default!",
    },
    msg4: {
      // 유효성 검사
      validator: function (value) {
        return value > 10;
      },
    },
  },
});
```

`type`은 네이티브 생성자 중 하나를 사용할 수 있다.

- String
- Number
- Boolean
- Function
- Object
- Array
- Symbol
  > `props` 유효성 검증이 실패하면 Vue 콘솔에서 경고를 출력한다.  
  > `props`는 컴포넌트 인스턴스가 생성되기 전에 검증되기 때문에 default 또는 validator 함수에서 data, computed, methods와 같은 인스턴스 속성은 사용할 수 없다.
