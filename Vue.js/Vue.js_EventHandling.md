## Vue 이벤트 핸들링

### 메소드 이벤트 핸들러

> 대부분의 이벤트 핸들러의 로직은 복잡하기 때문에 `v-on`에 JavaScript로 넘겨주기 어렵다.  
> `v-on`에 `methods`의 함수를 넘겨주는 형태로 구현 하는 것이 좋다.

```html
<div id="app">
  <button v-on:click="greet">Greet</button>
</div>
```

```js
new Vue({
  el: "#app",
  data: {
    name: "Vue.js",
  },
  methods: {
    greet: function (event) {
      // 메소드 안에서 사용하는 this 는 Vue 인스턴스를 가리킨다
      alert("Hello " + this.name + "!"); // event 는 네이티브 DOM 이벤트이다
      if (event) {
        alert(event.target.tagName);
      }
    },
  },
});
```

> `v-on`은 `click` 이벤트가 발생하면, `methods`에 정의한 `greet` 함수를 실행시킨다.

### 인라인 메소드 핸들러

> 메소드 이름을 `v-on`에 직접 바인딩 하는 대신 인라인 JavaScript를 사용하여 `methods`의 함수를 호출할 수 있다.

```html
<div id="app">
  <button v-on:click="say('hi')">Say hi</button>
  <button v-on:click="say('what')">Say what</button>
</div>
```

```js
new Vue({
  el: "#app",
  methods: {
    say: function (message) {
      alert(message);
    },
  },
});
```

> `v-on` 이벤트 리스너에서 `methods`에 정의된 함수를 직접 호출 할 수 있다.

### 이벤트 수식어

> 이벤트 핸들러 내부에서 종종 `event.preventDefault()` 나 `event.stopPropagation()`를 호출할 때가 있다.  
> Vue에서도 `preventDefault` 나 `stopPropagation`을 사용해야 할 때가 있다.  
> 그때 이벤트 핸들러 내부에서 이벤트 객체를 사용할 수도 있지만 `v-on` 이벤트 리스너에서 사용할 수 있다.

- `.stop`
- `.prevent`
- `.capture`
- `.self`
- `.once`

```html
<!-- 클릭 이벤트 전파가 중단된다 -->
<a v-on:click.stop="doThis"></a>

<!-- 제출 이벤트가 페이지를 다시 로드 하지 않는다 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 수식어는 체이닝 가능하다 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 단순히 수식어만 사용할 수 있다 -->
<form v-on:submit.prevent></form>

<!-- 이벤트 리스너를 추가할 때 캡처모드를 사용한다 -->
<div v-on:click.capture="doThis">...</div>

<!-- event.target이 엘리먼트 자체인 경우에만 트리거를 처리한다 -->
<div v-on:click.self="doThat">...</div>
```

> 이벤트 수식어를 사용한 순서대로 적용되기 때문에 여러개의 수식어를 사용할 때 수식어 사용 순서를 고려해야 한다.  
> 즉 `@click.prevent.self`를 사용하면 클릭 이벤트가 발생 했을 때 모든 엘리먼트의 기본 동작을 막을 수 있지만,  
> `@click.self.prevent`는 엘리먼트 자체의 기본 동작만 막을 수 있다.

#### `.once`

```html
<!-- 클릭 이벤트는 최대 한번만 트리거 된다 -->
<a v-on:click.once="doThis"></a>
```

> `.once` 수식어는 컴포넌트 이벤트에서도 사용할 수 있다.

#### `.passive`

```html
<!-- 스크롤의 기본 이벤트를 취소할 수 없다. -->
<div v-on:scroll.passive="onScroll">...</div>
```

> 지정한 이벤트 핸들러에서 `event.preventDefault()`를 호출하지 않는 다는 것을 브라우저에 알리는 이벤트 수식어이다.
