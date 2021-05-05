## `slot`

> 컴포넌트를 사용할 때, HTML 엘리먼트와 같이 컴포넌트에 콘텐츠를 전달해야 할 때가 있다.  
> 이때 `slot`을 사용하면 된다.

- Slot content

```html
<div id="app">
  <my-comp>Hello Slot!</my-comp>
</div>
```

```js
Vue.component("my-comp", {
  template: "<div><slot></slot></div>",
});
```

- Named Slots
  > 부모 컴포넌트에서 자식 컴포넌트로 여러개의 하위 엘리먼트를 넘겨줄 때 이름이 있는 `<slot>`을 사용하여 특정 위치를 지정할 수 있다.

```html
<div id="app">
  <my-comp>
    <div slot="slot1">Hello Slot!</div>
    <input type="text" />
  </my-comp>
</div>
```

```js
Vue.component("my-comp", {
  template: '<div><slot name="slot1"></slot></div>',
});
```

> 위 코드는 name이 `slot1`인 Hello Slot!만 화면에 표시된다.  
> `input` 태그는 이름이 없기 때문에 화면에 표시되지 않는다.

- Default Slot Content

```html
<div id="app">
  <my-comp></my-comp>
</div>
```

```js
Vue.component("my-comp", {
  template: "<div><slot>대체 콘텐츠</slot></div>",
});
```

> `#app` 컴포넌트의 하위 엘리먼트가 제공되지 않는다면, 기본 값으로 `"대체 콘텐츠"`가 화면에 보이게 된다.

### `slot-scope`

> `slot-scope`에 구조분해 문법이 사용 가능하다.

```html
<div id="app">
  <my-comp>
    <template slot-scope="myProps"> {{ myProps.mySlotData }} </template>
  </my-comp>
</div>
```

```js
Vue.component("my-comp", {
  template: '<div><slot my-slot-data="Hello Slot!"></slot></div>',
});
```

> 구조분해 문법을 사용하여 더 간결한 코드를 작성할 수 있다.

### `slot`을 사용한 객체 바인딩

```html
<div id="app">
  <my-comp>
    <template slot-scope="{ mySlotData }"> {{ mySlotData }} </template>
  </my-comp>
</div>
```

```js
Vue.component("my-comp", {
  template: '<div><slot :my-slot-data="message"></slot></div>',
  data() {
    return {
      message: "Hello Slot~?",
    };
  },
});
```

> `slot-scope`에 객체 데이터를 사용하여 `data`에 있는 `message` 값을 넣어줄 수 있다.
