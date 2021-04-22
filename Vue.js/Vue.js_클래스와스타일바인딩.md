## Vue 클래스 바인딩

### 객체 클래스 바인딩

> 클래스를 동적으로 바인딩하기 위해서는 `v-bind:class(:class)`를 사용한다.

```html
<div :class="{ active: isActive, 'text-danger': hasError }"></div>
```

> `:class`에 객체를 넘겨주어 여러 클래스를 바인딩 할 수 있다.  
> `isActive`가 `true`, `hasError`가 `false`일 때, `<div class="static active"></div>`가 렌더링 된다.  
> `hasError`가 `true`가 되면 `<div class="static active text-danger"></div>`가 렌더링된다.

- `data`를 통한 바인딩

```html
<div :class="classObject"></div>
```

```js
data : {
	classObject: {
		active : true,
		'text-danger' : false,
	}
}
```

- `computed`를 통한 바인딩

```html
<div :class="classObject"></div>
```

```js
data: {
	isActive: true, error: null
},
computed: {
	classObject: function () {
		return {
			active: this.isActive && !this.error,
			'text-danger': this.error && this.error.type === 'fatal'
		}
	}
}
```

### 배열을 통한 클래스 바인딩

```html
<div :class="[activeClass, errorClass]"></div>
```

```js
data: {
	activeClass: 'active',
	errorClass: 'text-danger',
}
```

### 컴포넌트를 통한 클래스 바인딩

```html
<div id="app">
  <Child class="baz boo"></Child>
</div>
```

```js
const Child = {
  template: '<div class="foo bar">Child</div>',
};
new Vue({
  el: "#app",
  components: {
    Child,
  },
});
```

> 위의 예제에서 `<Child />`는 `<div class="foo bar baz boo">`로 렌더링 된다.

### 객체를 통한 인라인 스타일 바인딩

> `v-bind:style(:style)` 을 통해 객체를 바인딩 할 수 있다.  
> 속성 이름에는 camelCase와 kebab-case를 사용할 수 있다.

```html
<div v-bind:style="styleObject"></div>
```

```js
data: {
  styleObject: {
    color: 'red',
    fontSize: '13px',
  }
}
```

> 객체에 직접 바인딩하여 더 간결하게 만들 수 있다.  
> 클래스 바인딩과 마찬가지로 객체를 반환하는 `computed`도 적용이 가능하다.
