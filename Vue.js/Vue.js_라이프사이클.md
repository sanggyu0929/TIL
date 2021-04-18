## Vue 라이프사이클

> 어떤 Vue 인스턴스나 컴포넌트가 생성될 때,  
> 미리 사전에 정의된 몇 단계의 과정을 거치게 되는데 이를 **라이프사이클(lifecycle)** 이라 한다.  
> 즉, Vue 인스턴스가 생성된 후 우리 눈에 보여지고, 사라지기까지의 단계를 일컫는다.

![Vue lifecycle](https://t1.daumcdn.net/cfile/tistory/99E0014A5BC4942D18)  
Vue 인스턴스는 크게 **생성(create)** 되고, DOM에 **부착(mount)** 되고, **업데이트(update)** 되며, **없어지는(destroy)** <U>4가지 과정</U>을 거치게 된다.

## Vue 라이프사이클 훅(Hook)

### beforeCreate

```js
const vm = new Vue({
  el: "#app",
  data: {
    msg: "Hello Vue!",
  },
  beforeCreate() {
    console.log("beforeCreate!", this.msg); //Undefined
  },
});
```

> **beforeCreate** 훅은 컴포넌트가 DOM에 추가되기도 전에 발생한다.  
> `this.$el`및 `data, methods`에도 접근할 수 없다.

### created

```js
const vm = new Vue({
  el: "#app",
  data: {
    msg: "Hello Vue!",
  },
  created() {
    console.log("created!", this.msg); //Hello Vue!
  },
});
```

> **created** 훅에서는 `data`를 반응형으로 추적할 수 있으며 `computed, methods, watch` 등을 접근할 수 있다.  
> 하지만 아직 DOM에는 추가되지 않은 상태이다.  
> `data`에 접근이 가능하기 때문에 초기에 `data`를 세팅하거나  
> 이벤트 리스너를 이 단계에서 선언하는 것이 가장 적절하다.

### beforeMount

```js
const vm = new Vue({
  el: "#app",
  data: {
    msg: "Hello Vue!",
  },
  beforeMount() {
    console.log("beforeMount!");
  },
});
```

> **beforeMount** 훅은 DOM에 부착하기 직전에 호출되는 훅이다.  
> 가상 DOM이 생성되어 있으나 실제 DOM에 부착되지는 않은 상태이다.

### mounted

```js
const vm = new Vue({
  el: "#app",
  data: {
    msg: "Hello Vue!",
  },
  mounted() {
    console.log("mounted!");
  },
});
```

> **mounted** 훅은 일반적으로 가장 많이 사용하는 훅이다.  
> 가상 DOM의 내용이 실제 DOM에 부착되고 난 이후에 실행된다.  
> `this.$el, data, computed, methods, watch` 등 모든 요소에 접근이 가능하다.

### beforeUpdate

```js
const vm = new Vue({
  el: "#app",
  data: {
    msg: "Hello Vue!",
  },
  beforeUpdate() {
    console.log("beforeUpdate!");
  },
});
```

> **beforeUpdate** 훅은 `data`의 값이 변해서 DOM에도 그 변화를 적용시키기 직전에 호출되는 훅이다.

### updated

```js
const vm = new Vue({
  el: "#app",
  data: {
    msg: "Hello Vue!",
  },
  updated() {
    console.log("updated!");
  },
});
```

> **updated** 훅은 가상 DOM을 렌더링 하고 실제 DOM이 변경된 이후에 호출되는 훅이다.  
> 변경된 값들을 DOM을 이용해 접근하고 싶다면, **updated** 훅이 가장 적절하다.

### beforeDestroy

```js
const vm = new Vue({
  el: "#app",
  data: {
    msg: "Hello Vue!",
  },
  beforeDestroy() {
    console.log("beforeDestroy!");
  },
});
```

> **beforeDestroy** 훅은 해당 인스턴스가 해체되기 직전에 호출된다.  
> 이 단계에서는 이벤트 리스너를 해제하는 등 인스턴스가 사라지기 전에 해야할 일들을 처리한다.

### destroyed

```js
const vm = new Vue({
  el: "#app",
  data: {
    msg: "Hello Vue!",
  },
  destroyed() {
    console.log("destroyed!");
  },
});
```

> **destroyed** 훅은 인스턴스가 해체되고 난 후에 호출된다.  
> 해체가 끝난 이후에 실행되기 때문에 인스턴스의 속성에 접근할 수 없다.
