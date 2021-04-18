## Vue.js 기본 형태

기본 형태는 Vue 인스턴스를 생성하여 내부에 `el` 속성과 `data` 속성을 넣는 것이다.

```html
<script>
  var app = new Vue({
    el: "#app",
    data: {
      message: "Hello Vue.js!",
    },
  });
</script>
```
