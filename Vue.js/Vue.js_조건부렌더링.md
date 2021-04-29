## Vue 조건부 렌더링

### v-if

> `v-if` 디렉티브는 조건에 따라 블록을 렌더링하기 위해 사용된다.  
> 블록은 디렉티브의 표현식이 `true` 값을 반환할 때만 렌더링된다.

```html
<div id="app">
  <h1 v-if="ok">Yes</h1>
</div>
```

```js
new Vue({
  el: "#app",
  data: {
    ok: true,
  },
});
```

### v-else

> `v-else`디렉티브는 `v-if`디렉티브와 함께 사용 가능하다.

```html
<div id="app">
  <h1 v-if="ok">Yes</h1>
  <h1 v-else>No</h1>
</div>
```

```js
new Vue({
  el: "#app",
  data: {
    ok: true,
  },
});
```

### `<template>`와 `v-if`로 조건부 그룹 만들기

`v-if`는 디렉티브이기 때문에 하나의 엘리먼트에 추가되어야 한다.  
하지만 HTML에 실제로 렌더링 되지 않는 태그인 `<template>`를 사용하면 각각의 엘리먼트에 `v-if`를 사용하지 않고 조건부 그룹을 만들어 렌더링을 사용할 수 있다.

```html
<div id="app">
  <template v-if="ok">
    <h1>Title</h1>
    <p>Paragraph 1</p>
    <p>Paragraph 2</p>
  </template>
</div>
```

```js
new Vue({
  el: "#app",
  data: {
    ok: true,
  },
});
```

### `key`를 이용하여 재사용 가능한 엘리먼트 제어

> Vue는 효율적인 렌더링을 위해 때때로 처음부터 렌더링하는 것이 아닌, 기존의 엘리먼트를 다시 사용한다.

```html
<div id="app">
  <div>
    <template v-if="loginType === 'username'">
      <label>사용자 이름</label>
      <input placeholder="사용자 이름을 입력하세요" />
    </template>
    <template v-else>
      <label>이메일</label>
      <input placeholder="이메일 주소를 입력하세요" />
    </template>
    <button @click="changeLoginType">로그인 유형 변경</button>
  </div>
</div>
```

```js
new Vue({
  el: "#app",
  data: {
    loginType: "username",
  },
  methods: {
    changeLoginType() {
      if (this.loginType === "username") {
        this.loginType = "email";
      } else {
        this.loginType = "username";
      }
    },
  },
});
```

> 위 코드에서 `loginType`이 바뀌어도 사용자가 입력한 내용이 지워지지 않는다.  
> Vue는 엘리먼트를 재사용하여 `<input>` 자체가 대체되지 않고 `placeholder`만 변경된다.  
> 이때 `key`속성을 사용하여 별개의 엘리먼트인 것을 명시하면 Vue는 엘리먼트를 재사용하지 않고 완전히 대체하여 렌더링 한다.

```html
<div id="app">
  <div>
    <template v-if="loginType === 'username'">
      <label>사용자 이름</label>
      <input placeholder="사용자 이름을 입력하세요" key="username-input" />
    </template>
    <template v-else>
      <label>이메일</label>
      <input placeholder="이메일 주소를 입력하세요" key="email-input" />
    </template>
    <button @click="changeLoginType">로그인 유형 변경</button>
  </div>
</div>
```

### v-show

> `v-show` 디렉티브를 사용하여 조건부 렌더링을 사용할 수 있다.

```html
<div id="app">
  <h1 v-show="ok">Yes</h1>
</div>
```

```js
new Vue({
  el: "#app",
  data: {
    ok: true,
  },
});
```

> `v-show`는 DOM에 항상 그려진다.  
> `v-show`에 `false`가 넘겨지면 `display:none`이 되어 DOM에는 있지만 화면에 나타나지 않는 상태이다.  
> `v-show`는 `<template>`를 지원하지 않는다.

### `v-if` VS `v-show`

> `v-if`디렉티브를 사용하면 엘리먼트의 이벤트 리스너와 자식 컴포넌트들이 DOM에 제거되거나 삽입되는 진짜 조건부 렌더링이다.  
> 반면 `v-show`는 DOM에 항상 삽입되고 `display` style을 통해 화면에 그려지거나 그려지지 않는 조건부 렌더링이다.  
> `v-if`는 토글 비용(화면에 그려지거나 그려지지 않는데 사용되는 비용)이 높고, 초기 렌더링 비용이 낮다.  
> `v-show`는 토글 비용이 낮고, 초기 렌더링 비용이 높다.
